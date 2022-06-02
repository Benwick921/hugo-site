+++
title =  "Manual Unpacking UPX and MPRESS"
+++

<h1> <span style="color:#da1953">Man</span>ual Unpacking UPX and MPRESS </h1>

Jul 23, 2020

---

# Index

- [Introduction](#INTRO)
- [Packing Indicators](#PACIND)
- [Manual Unpacking UPX](#MANUNPACUPX)
- [Manual Unpacking MPRESS](#MANUNPACMPRESS)

---

<h2 id=INTRO> <span style="color:#da1953">Int</span>roduction </h2>

> *"Packing is a technique to hide the original code of a program through one or more layers of compression and/or encryption.*

> *Used by malware writers to make static analysis harde, to hide from certain antivirus products via polymorphism (diversity), as packers are used to shrink benevolent programs, they cannot be banned!*

> *In-depth analysis of packed malware usually starts in a debugger: in other words, we must unpack the sample…"*

The tools I am going to use are:

- PEStudio
- Detect It Easy
- IDA (Free)
- Scylla

<h2 id=PACIND> <span style="color:#da1953">Pac</span>king Indicators </h2>

Before doing unpacking I have to understand if the binary is packed or not and to do this I will use two tools in particular, **Detect It Easy** and **PEStudio**.

I load the binary with **Detect It Easy** and I see what information it gives to me.

![](/upxmpress/image15.png)

**Detect It Easy** tells me that it is packed with **UPX** and it also tell the version (3.93), another useful information is the number of sections, to check it is accuracy I also check entropy.

![](/upxmpress/image17.png)

I check it to be sure that it’s packed, sometimes it could show that the binary is not packed but it has a high level of entropy which is a good indication of packing.

I also need to check the type of the binary (**H**-hexadecimal key in the main window of **Detect It Easy**), even if I know it, I have to be sure.

(**MZ**) These two characters indicate that the binary is a **PE** (Portable Executable) but they might get changed by the attacker, in this case by viewing the number of next bytes I can detect if it’s really a **PE** or not.

![](/upxmpress/image32.png)

Now I go to **PEStudio** to see what information I can collect and if it also confirms that it is packed.

The first thing I am going to check is the size of the binary to get an idea of ​​who am I dealing with.

If the file is very large it cannot have few imports while for a small file it is plausible but it is not said therefore not to trust is better.

![](/upxmpress/image14.png)

Here, in addition to the file size, I also see the entropy (7,114) which is very high equal to **Detect It Easy** and therefore it seems that it is packed. I also have the signature confirming that it is packed with UPX.

Now I check the sections, in particular *"Virtual-Size"* and *"Raw-Size"* of the sections. if at last in one of them the difference is so high it’s a good indicator of packing.

If at least one section has a very high entropy then it is another good indicator of packing (MAX-Entropy: 8), also if at least one section has **WX** (Writable and Executable) permission is also an indicator of packing.

![](/upxmpress/image4.png)

Now I check the imports, if the imports are so few it’s a good indicator of packing, if *“GetProcess”* and *“LoadLibraryA”* are the only imports shown in the PEStudio then it is sure that the binary is packed.

![](/upxmpress/image31.png)

In this case I have too few imports, there are cases where only the two imports mentioned above are shown. 

At last I search the strings in search of the packer’s name, to make the search easier I ordered the strings in descending order.

![](/upxmpress/image18.png)

Now that I am sure that the binary is packed I will show how to unpack in the two cases where it is packed with MPRESS and the case where it is packed with UPX.

For the first part I used a packed binary with UPX but the results of **PEStudio** and **Detect It Easy** would be almost identical if the file had been packed with MPRESS.

<h2 id=MANUNPACUPX> <span style="color:#da1953">Man</span>ual Unpacking UPX </h2>

To do the unpacking I use **IDA**, any version is fine in my case it is **IDA Free** and I load the binary as **PE**.

![](/upxmpress/image25.png)

Once the binary is loaded, **IDA** warns me that some imports are not visible and that **IAT** (Import Address Table) is located outside the memory range and this further confirms that the binary is packed.

![](/upxmpress/image20.png)

To unpack **UPX** I have to look for a *"tail jump"*, it is called *"tail jump"* because it is usually at the end of the program. This jump has a peculiarity therefore jump from one section to another and therefore it is a very long jump.

![](/upxmpress/image13.png)

Here I have a jump in the **UPX1** section which goes to another section and jumps to address **402284**.

![](/upxmpress/image22.png)

In fact I see that the address **402284** is in the **UPX0** section and there are no other jumps of this type so I can conclude that I have found the tail jump.

At this point I put a breakpoint at address **402284** and run the binary and this message confirms once again that the binary is packed.

![](/upxmpress/image26.png)

Select *“yes”*.

After the execution the code has changed, now I can see the code that was hidden / compressed inside it.

![](/upxmpress/image11.png)

I am on a *"call"* statement, where I should really be. At this point I can use both the address of the jump instruction (**402284**) and the address to which it jumps (**402558**) as **OEP** (Original Entry Point) and in both addresses they work fine.

In order to unpack I use **Scylla** and in the **OEP** field I write one of the two addresses.

__**During these operations I must leave IDA running in debug I cannot close it.**__

1. I select the process of IDA running the sample.
2. I insert in the OEP field the address found on IDA.
3. Click “IAT Autosearch”

And it would successfully find the start address and the size. ***If not it is a good practice to to restart every time Scylla because its buggy***.

![](/upxmpress/image10.png)

At this point I can get the imports simply by clicking *"Get Imports"*.

![](/upxmpress/image30.png)

84 imports were found, since I own the unpacked binary I can double check if the found imports are correct.

![](/upxmpress/image19.png)

In fact **PEStudio** tells me that the unpacked binary has 84 imports so my process has been successful.

To create the unpacked binary, I click on *"Dump"* and save the file.

![](/upxmpress/image34.png)

Now just I click on *"Fix Dump"* and choose the dump created previously to create the unpacked binary.

![](/upxmpress/image29.png)

To make a further check, I load the new binary with **PEStudio**.

![](/upxmpress/image9.png)

Here I can see the difference between the original packed binary and the unpacked binary created by me.

The first thing I notice is the size of my file is much larger, which I expected, while the imports of my binary are 0 but this is not a problem because it is a problem during the creation of the new binary with **Scylla** , as long as **Shylla** has found the imports correctly there are no problems even if **PEStudio** does not show them, lastly I see that there are many more strings than before.

And this concludes the manual unpacking of a packed binary with **UPX**.

<h2 id=MANUNPACMPRESS> <span style="color:#da1953">Man</span>ual Unpacking MPRESS </h2>

The identification of a packed binary with **MPRESS** is identical to that of **UPX** shown above. Loading the binary with **IDA** tells me directly that maybe it is packed.

![](/upxmpress/image2.png)

Once the binary is loaded I should be faced with a *pusha* instruction, if this were not the case, just select the start function and put a breakpoint.

![](/upxmpress/image21.png)

Now I run the binary paying particular attention to the *Stack View* window (down right corner window).

![](/upxmpress/image5.png)

I step over once and notice that the addresses on the stack have changed.

![](/upxmpress/image7.png)

Now the stack points to start, I step over until I come back again on the start, since the start on the stack appears twice once at **9FF64** and once at **9FF68**.

In my case it was enough for me to do *Step Over* twice.

![](/upxmpress/image1.png)

Note that I started from *pusha* instruction at **4512D7** and now I am at **4512DE**.

Now I right click on the stack address **19FF64** and follow in hex dump.

![](/upxmpress/image36.png)

The *Hex View-1* window will change and a byte will be highlighted.

![](/upxmpress/image16.png)

Now I select the four bytes (DWORD) starting from **D7** and put a breakpoint on it which will be a hardware breakpoint with read and write permission (WR), the permissions **WR** will be set automatically but it is possible to view the breakpoint and modify it but in this case is not needed.

![](/upxmpress/image3.png)

Now I run the binary with the *Play* button and I will hit the hardware breakpoint.

![](/upxmpress/image28.png)

and **IDA** will detect that **RIP** point is not in a defined address same as for **UPX**.

![](/upxmpress/image8.png)

Upon pressing *Yes* the code will change and I’m suddenly in a *call* instruction and I step into, **IDA** will tell me again the same message about **RIP** pointing in an undefined address.

I can’t use the address of *call* instruction (402BA6) as I did for **UPX** but I have to use the address pointed by the *call* instruction (401B54).

![](/upxmpress/image24.png)

And the address **401B54** is my **OEP** which I will use in **Scylla** to unpack it.

Once found the **OEP** the unpacking process will be identical to **UPX** but for completeness I rewrite it anyway.

Remember to restart **Scylla** every time because it’s buggy. Also here I can’t close the **IDA** process which is in debugging.

In order to unpack I follow the same steps as for **UPX**.

1. I select the process of **IDA** running the sample.
2. I insert in the **OEP** field the address found on **IDA**.
3. Click *“IAT Autosearch”*

---

And it would successfully find the *start* address and the size.

![](/upxmpress/image23.png)

At this point we can get the imports simply by clicking *"Get Imports"*.

![](/upxmpress/image6.png)

68 imports were found, since I own the unpacked binary also for this I can double check if the found imports are correct.

![](/upxmpress/image35.png)

In fact **PEStudio** tells me that the unpacked binary has 68 imports so my process has been successful.

To create the unpacked binary, click on *"Dump"* and save the file.

![](/upxmpress/image12.png)

Now just click on *"Fix Dump"* and choose the dump created previously to create the unpacked binary.

![](/upxmpress/image33.png)

To make a further check, I load the new binary with **PEStudio**.

![](/upxmpress/image27.png)

Here I can see the differences between the original packed binary and the unpacked binary created by me.

Much like **UPX**, even here the same values change even if the change is not much.

The unpacked version with **Scylla** has 0 imports, same as the **UPX** it’s not a problem as long as during the process **Scylla** found all the imports.

This conclude the manual unpacking of binaries packed with MPRESS.

