+++
title =  "I Hacked My Wi-Fi"
+++

<h1> <span style="color:#da1953">I Ha</span>cked My WiFi </h1>

June 27, 2020

---

<h2> <span style="color:#da1953">Ind</span>ex </h2>

- [Requirements](#REQ)
- [Find wireless interface name](#INTFACENAME)
- [Kill interfering processes](#KILLINTFACEPROC)
- [Enable monitor mode](#ENMONMOD)
- [Discover Access Point](#DISCACCPOINT)
- [Save data to file](#SAVEFIL)
- [Deauthentication](#DEAUTH)
- [Crack the password](#CRACKPSW)

---

During the lockdown I was so bored that I decided to bring my 9 years old pc back to life. I opted for Debian as the operating system due to the very minimal system specifications, and therefore perfect for my case. After a painstakingly long time taken for the installation of Debian, I decided to try to crack my WI-FI just to tinker a maybe due to a little bit of nostalgia, and little just to test my Wi-Fi security, (Note all commands launched from now on need root privileges. To get the privileges just type `su –` and enter the password to become root.)

<h2 id=REQ> <span style="color:#da1953">Ste</span>p 0: Requirements </h2>

I need to install Aircrack-ng to perform the attack and JTR (John The Ripper) to perform brute force cracking,unless I am in Kali Linux I will install by typing `apt install aircrack-ng` and for JTR I suggest to use the one installed on Kali Linux that works out of the box.

<h2 id=INTFACENAME> <span style="color:#da1953">Ste</span>p 1: Find wireless interface name </h2>

To find the name of the wireless interface I run `iwconfig`.

![iwconfig](/ihackedmywifi/iwconfig.png)

but any other commands for networking will work fine, such as <code>ifconfig</code> (which is deprecated now use <code>ip address</code> / <code>ip add</code> / <code>ip a</code>).

![ip a](/ihackedmywifi/ipa.png)

I do not know why but, in my case, I have a very strange name (wlp2s0b1) I would have expected to see something like wlan0.

<h2 id=KILLINTFACEPROC> <span style="color:#da1953">Ste</span>p 2: Kill interfering processes </h2>{

Before enabling monitor mode, we need to kill interfering processes.

To check which process might interfere run `airmon-ng check`.

![airmon-ng check](/ihackedmywifi/check.png)

To kill the interfering processes run `airmon-ng check kill` or kill them manually.

![airmon-ng check kill](/ihackedmywifi/checkkill.png)

<h2 id=ENMONMOD> <span style="color:#da1953">Ste</span>p 3: Enable monitor mode </h2>

Monitor mode allows a computer with a wireless network interface controller to monitor all traffic received on a given wireless channel.

To enable monitor mode type `airmon-ng start wlp2s0b1`.

![start wlan](/ihackedmywifi/startwlan0.png)

Now a new name has been assigned to the interface (wlp2s0b1mon) and from now on I will use that.

<h2 id=DISCACCPOINT> <span style="color:#da1953">Ste</span>p 4: Discover Access Point </h2>

To discover surrounding access point type airodump-ng wlp2s0b1mon`.

![airodump vlan](/ihackedmywifi/airodumpvlan0.png)

Now we will start to catch all the wireless packets and gather data from the networks.

From this step onward we need to remember the victim (me) Wi-Fi channel, in my case is 1.

<span style="color:#FFC107">This terminal must never be closed as it will be used to find out if we have successfully established the 4-way handshake which contains the password hash for authentication.</span>

<span style="color:#FFC107">The next step will be done in another window.</span>

<h2 id=SAVEFIL> <span style="color:#da1953">Ste</span>p 5: Save data to file </h2>

To save data in files we need to use the same command we use in step 4 with a different option.

`airodump-ng -c [channel] –bssid [bssid of victim wifi] -w [path to write files] wlp2s0b1mon[interface]`

![save file](/ihackedmywifi/savefilecap.png)

The result of the command will be something like this.

![save file](/ihackedmywifi/safilecap1.png)

And it will also create files on the given path (in my case the current directory).

![save file](/ihackedmywifi/savefilecap2.png)

<span style="color:#FFC107">Same as for step 4 I leave the window open and the next operations will be done in a further third window.</span>

<h2 id=DEAUTH> <span style="color:#da1953">Ste</span>p 6: Deauthentication </h2>

The goal of this phase is to disconnect all the devices connected to the Wi-Fi so that when they reconnect, they will send the password under hash signature to the router and then we could capture it in order to crack it.

The channel used is the same as the previews one where the victim is (1).

To do so the command is `aireplay-ng –deauth 1 -a [victim BSSID] wlp2s0b1mon`.

![deauthentication](/ihackedmywifi/deauth1.png)

It will establish the handshake alongside the hash of the password and same in the file previously set.

On my first try even if everything went well for some reason Aircrack-ng didn’t find the handshake in the .cap file so just to be sure I tend to repeat this step few times.

If we correctly establish the handshake, I will see it in the window where I executed<br>
`airodump-ng -c [channel] –bssid [bssid of victim wifi] -w [path to write files] wlp2s0b1mon[interface]`

![check handshake](/ihackedmywifi/checkhandshake.png)

Sometimes you might get a message where the network interface and the victim’s Wi-Fi are in different channel, don’t panic just run the command again and again until you get it!

![channel](/ihackedmywifi/differentchannels.png)

You might never get the handshake containing the hash if no devices are connected! Don’t lose your hope. In this case you need to wait until someone comes and hopefully connects to the Wi-Fi.

<h2 id=CRACKPSW> <span style="color:#da1953">Ste</span>p 7: Crack the password </h2>

There are few methods to crack the password the first method I tried is the dictionary attack, to perform it execute<br>
`aircrack-ng -b [victim BSSID] -w [wordlistpath] [path to .cap file]`


I created a tiny wordlist containing my password for the testing purpose, in real world scenario I would use good wordlists, not necessarily big but good and more than one probably.

The .cap file is automatically created on a given path to save the files in step 5.

![cracked](/ihackedmywifi/cracked.png)

What if the password is not in the wordlist? I have to try different type of attacks like brute force.

In order to do the brute force attack I mooved to my kali linux because it has JTR (John The Ripper) installed properly, which is my favourite cracking	program, and with all its feature which inclide the cracking of wpa keys.	

In order to let JTR to be able to crack a WPA handshake I need to convert the .pcap file to a proper format, the first thing is to convert the pcap file into a .hccap file, todo so we will use aircrack-ng: `aircrack-ng [.pcap file] -J [filename]`

![pcap2hhcap](/ihackedmywifi/pcap2hccap.jpg)

Now I will convert the .hccap file into a a file that JTR can understand and crack:<br>
`hccap2john [.hccap file] > [filename]`

At this point we can use any mode JTR has to craack the password:<br>
`john [optional mode] [file]`

![john the ripper](/ihackedmywifi/jtr.jpg)

To see all the modes avalaible look the manual of JTR.
