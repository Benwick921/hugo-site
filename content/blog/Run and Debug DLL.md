+++
title =  "Run and Debug DLL"
+++

<h1> <span style="color:#da1953">Run</span> and Debug DLL </h1>

Jul 27, 2020

---

<h2> <span style="color:#da1953">Ind</span>ex </h2>

- [Introduction](#INTRO)
- [Run DLL](#RUNDLL)
- [Debug DLL](#DBGDLL)

---

<h2 id=INTRO> <span style="color:#da1953">Int</span>roduction </h2>

A DLL is a library that contains functions/code and datato to be used by more than one program at the same time, unlike normal programs it does not contain a **main** function therefore it does not have an entry point for execution.

But there are various reasons why to execute a DLL for example to solve a CTF, to analyze a DLL that a malware has dropped or to understand how it works.

<h2 id=RUNDLL> <span style="color:#da1953">Run</span> DLL </h2>

To run any DLL I have to use *rundll* program in my case im using `rundll32` because the DLL is x86.
So in order to run a DLL I have to execute the command `rundll32 hellow-world-x86.dll,#2` where **#2** is the number of exports.

After the execution a popup with the message *Hello world* will appear.

![](/rundebugdll/1.jpg)

If a different number of exports is given the DLL will continue executing with an error message as long as I dont press *"ok"* on the error message, but in case the number of exports is unknows I always put a high number to execute it.

![](/rundebugdll/2.bmp)

<h2 id=DBGDLL> <span style="color:#da1953">Deb</span>ug DLL </h2>

In order to dynamically debug the DLL im going to use **IDA Free** and as I see trying to run it as usual doesent work at all.

![](/rundebugdll/3.JPG)

Now to run and debug the DLL properly I open two IDA windows, one with the DLL in static analysis and another in dynamic analysis running the DLL via `rundll32` program in IDA.

Now I open another IDA window and open `rundll32` which in the path `C:\Windows\SysWOW64\rundll32.exe` to dinamically analyse my DLL and leave the other IDA window instatic analisys in background (for now).

![](/rundebugdll/4.JPG)

If this error message appears press *"Yes"*, it means I have to choose a different path to save the IDA databases about the future analysis and I usually choose my Desktop.

![](/rundebugdll/5.JPG)

At this point I have to tell the `rundll32` loaded in IDA to execute my `hello-world-x86.dll`.

![](/rundebugdll/6.jpg)

and a window will pop up where I will put the parameters that `rundll32` take which are the name of the DLL to run and its paramenter similarly to when I executed in the shell, but with the only difference that I have to put the full path of the DLL.

![](/rundebugdll/7.jpg)

Once set the parameters I have to set the debugger in order to stop at each load and unload of library in this way as soon as my DLL is loaded the process will stop without continuing to go on, at that point I can begin to analyze the DLL code.

![](/rundebugdll/8.jpg)

At the *"Debugger setup"* windows I have to check *"Suspend on library load/unload"* in *"Event"* section and *"Library load/unload"* in *"Logging"* section.

![](/rundebugdll/9.jpg)

By enabling logging on load/unload operation I can see what libraries are loading and unloading and when my DLL is being loaded.
Now I start debugging pressing the play button.

I can see the libraries start loding and each time a library is loaded it stops so I have to keep pressing play every time untill my library (`hello-world-x86.dll`) is loaded.

![](/rundebugdll/10.JPG)

After quite a lot my DLL get loaded.

![](/rundebugdll/11.jpg)

Now to see at what address the library is loaded I have to look to the *"Modules List"* window, if the windows is not there u can open it.

![](/rundebugdll/12.jpg)

In my case the library has been loaded at **73670000**.

![](/rundebugdll/13.JPG)

If ASLR is on at every run the DLL will be loaded in a different address so in order to match the address from the IDA window of static analysis (which starts at **10001000**) with the dinamyc analysis one

![](/rundebugdll/14.jpg)

I have to rebase the IDA window in static analysis in order to let it start from **73670000** instead of **10001000**.

![](/rundebugdll/15.jpg)

![](/rundebugdll/16.jpg)

The rebased program address are now changed.

![](/rundebugdll/18.jpg)

At this point I am stoppped right after the dinamyc IDA window loaded my DLL, I select any line of code and press *"G"* to jump in a specific address. The address where I wanto to jump is the one I found after rebasing my DLL in stacic view of IDA which is **73671000** and I will jump in the desired portion of the code I want to debug.

![](/rundebugdll/17.JPG)

In this way I can find by using the static view any portion of the code of the DLL, put a breakpoint, jumping there and debug by executing it step by step.
