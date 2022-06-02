+++
title = "University CTF"
+++

<h1> <span style="color:#da1953">Uni</span>versity course's web CTF </h1><br>

---
<h2 id=LV1> <span style="color:#da1953">Ind</span>ex </h2>

- [Introduction](#INTRO)
- [Password validation](#LV1)
- [Stop!](#LV2)
- [Password verification](#LV3)
- [Secure Browser](#LV4)
- [Level 5](#LV5)
- [Your personal secret](#LV6)
- [Password protected](#LV7)
- [Your persona secret pt.2](#LV8)
- [Password protected pt.2](#LV9)
- [Bytestream](#LV10)
- [Brutus system](#LV11)
- [Level 12](#LV12)
- [Bash Envirorment](#LV13)
- [Level 14 (updating...)](#LV14)
- [Level 15 (updating...)](#LV15)

---

<h2 id=LV1> <span style="color:#da1953">Int</span>roduction </h2>

---

<h2 id=LV1> <span style="color:#da1953">Lev</span>el 1 </h2>

The URL of the first level was given as the starting point:

`http://eth-lab.di.uniroma1.it:55001/eishohwohpahxooy/`

As stated during the Web Security Challenges lectures, the first thing to do when trying to hack a web page is to actually use the web page as it is suppose to be used. So, in other words, to simply do what the web page asks you to do. 

Therefore, we try to log in inserting random username and password, as requested from the web page itself.

![](/writeups/unictf/image18.png)

As expected we receive an error:

![](/writeups/unictf/image28.png)

Then, let's try to dig furthermore inspecting the web page's source code.

![](/writeups/unictf/image63.png)

As We can see in the form above that on clicking *Submit* we actually call a function named *verify*.

So, we start looking for a function called *verify* in the Console section (right click -> inspect element).

![](/writeups/unictf/image43.png)

As we can see from the picture above, we can find the function *verify*. Now let’s jump into the definition of the function, to check in detail what the function is supposed to do. 

![](/writeups/unictf/image64.png)

We can see in the `if` condition highlighted in red, the password and the username needed in order the access the web page.

![](/writeups/unictf/image86.png)

---

<h2 id=LV2> <span style="color:#da1953">Lev</span>el 2 </h2>

Once solved the Level 1, the URL of the second level is found:

`http://eth-lab.di.uniroma1.it:55043/zeitaeveishiidef`

This is how the Level 2 look like:

![](/writeups/unictf/image67.png)

In this level there is only the possibility to insert a password, there is no username. So, let's try to insert a random password.

![](/writeups/unictf/image72.png)

Well, wrong password! As done in the previous level, we try to look further by analyzing the source code.

![](/writeups/unictf/image70.png)

Reading the first lines we can clearly see that there is a function implementation, the function seems to encrypt the text inserted in the password field, with MD5 function. The first idea is to decrypt what seems to be a ciphertext in the `if` condition. 

After using numerous MD5 online decrypted without success, we decide to keep on reading the source code. While having a closer look at it, we noticed two images references in the inspector section: one was a reference to the picture in the home page "kitten.jpg" and the other one was a picture with a hidden parameter "srct.png".

Putting the cursor on top of the reference *scrt.png* a window pops up with a text.

![](/writeups/unictf/image77.png)

The text on the picture was the right password to insert in order to solve the level.

---

<h2 id=LV3> <span style="color:#da1953">Lev</span>el 3 </h2>

As usual, in the previous level we found the link to access the next one:

`http://eth-lab.di.uniroma1.it:55208/bahjeighahveerae/cgi-bin/index.php`

As before, as a first step, we try to follow the natural instructions of the web page itself, this time trying to insert username and password. We decided to try with some random and basic combination of username and password (e.g. *admin:admin*).

As we expected, the received the following error page:

![](/writeups/unictf/image73.png)

So, let us dive in the source code once again.

![](/writeups/unictf/image75.png)

In the source code, we found a hidden parameter with a *False* value so we can proceed by changing the value from False to True, and submit the form.

![](/writeups/unictf/image78.png)

After applying the above-mentioned changes, we finally obtaine the page with the URL of the next level.

![](/writeups/unictf/image80.png)

---

<h2 id=LV4> <span style="color:#da1953">Lev</span>el 4 </h2>

This is the URL for the Level 4:

`http://eth-lab.di.uniroma1.it:55192/ogheucaiheikohhi`

![](/writeups/unictf/image82.png)

This level consist in verifying our browser in order to have access.

![](/writeups/unictf/image84.png)

Only connections from *Kevin Browser Rocks* are accepted.

The thing we had to do is to pretend to be using the browser *Kevin Browser Rocks* by changing the headers in our browser. In order to do that we can use an extension (**Simple Modify Headers**, on Firefox) that modifies the header, and we set up to do it during the requests.

![](/writeups/unictf/image87.png)

As we can see we modify our browser `user-agent` to *Kevin Browser Rocks*.

![](/writeups/unictf/image89.png)

Nice! Now the page accepts only connections from Russian (.ru) websites. We have our extension and we can also use it to simulate Russian connection by changing our browser referrer.

![](/writeups/unictf/image89.png)

By applying this new change, we can finally get the URL to access the new level.

![](/writeups/unictf/image90.png)

---

<h2 id=LV5> <span style="color:#da1953">Lev</span>el 5 </h2>

This is the URL obtained to access the fifth level:

`http://eth-lab.di.uniroma1.it:55051/iengohquoochieza/`

![](/writeups/unictf/image47.png)

The first thing we do is to analyze the source code.

![](/writeups/unictf/image49.png)

*“Never show secret.txt to the users”*, this caught our attention so we search for the file called: *secret.txt*, in the current web directory. As we know the URL is nothing else than a path to file in a webserver, so we added *secret.txt* to the urn to the URL in order to find it.

![](/writeups/unictf/image51.png)

At this point we need to find the secret at *cgi-bin/getsecret.js* and refer ourselves as *di.uniroma1.it/supersecurepage*, which can be done with the Firefox extension as done in the previous levels.

![](/writeups/unictf/image53.png)

After having done this, we were able to find the URL to the next level. 

![](/writeups/unictf/image55.png)

---

<h2 id=LV6> <span style="color:#da1953">Lev</span>el 6 </h2>

The URL for the level 6 obtained by solving the level 5:

`http://eth-lab.di.uniroma1.it:55005/oaxiweitheerohra`

![](/writeups/unictf/image57.png)

Here we have applied the usual method of trying one of the most common combination username and password (admin:admin).

![](/writeups/unictf/image59.png)

Digging in the source code and reading it did not reveal anything. So, we turn our attention to the URL, and we find a reference to a php script with the field *uid* exposed *userinfo.php?uid=0*.

![](/writeups/unictf/image60.png)

The field is set to *0* which is our current user’s ID, so we try to change it with 1 and we were sent to another we page, Angelo's web page. 
Then we started to change the value of uid until we found the user with the secret at *uid=6*.

![](/writeups/unictf/image61.png)

---

<h2 id=LV7> <span style="color:#da1953">Lev</span>el 7 </h2>

The URL found by solving level 6:

`http://eth-lab.di.uniroma1.it:55215/shieduekecometha/`

![](/writeups/unictf/image62.png)

As stated in the picture in order to log in we need an e-mail and the username.

![](/writeups/unictf/image24.png)

So, we try a fake and random email and a random string as password. At that point, we notice that the site check if the username is really an e-mail just by checking if the username string contained the character *@*.

![](/writeups/unictf/image26.PNG)

We can try to insert any kind of random email for instance *admin@admin* or even *teacher@something* but we always received the same kind of message.After having tried some standard types of email, we thought that we could try by inserting a real teacher’s email address.

Our first attempt was to try with course main teacher's email but it was not the right solution. Then we tried again with our laboratorys teacher's  email and finally that one was the key solution for the next level because we were able to log in as a teacher and consequently obtain the link for the next level.

![](/writeups/unictf/image29.png)

![](/writeups/unictf/image31.png)

---

<h2 id=LV8> <span style="color:#da1953">Lev</span>el 8 </h2>

Let’s start with the URL obtained from the previous levels:

`http://eth-lab.di.uniroma1.it:55493/zangiepaegaizeex/cgi-bin/index.php`

![](/writeups/unictf/image33.png)

Our first attempt is as usual the standard combination of *admin:admin* as username and password.

![](/writeups/unictf/image35.png)

And we notice a code in the URL which should be the ID of the current user.

![](/writeups/unictf/image37.png)

We try to figure it out why the current user (admin) has that precise value, and we also notice that the string *admin* and the string *nqzva* had the same length, so we started to match the characters from the first string with the ones from the other string hence *a=n*, *d=q*.

We immediately notice that the distance between the characters was 13, so we try to ROT13 the string *admin* and the result string was *nqzva*.

After many random tries, our attention was captured by the sentence *“Page created by MessyAdmin”* present in the first page of the level.

So, we decide to ROT13 the string *messyadmin* which result in *zrfflnqzva* which has been copied and pasted to the URL instead of *nqzva* and we ended up to the MessyAdmin’s page where we found the link to the next level.

![](/writeups/unictf/image38.png)

![](/writeups/unictf/image39.png)

---


<h2 id=LV9> <span style="color:#da1953">Lev</span>el 9 </h2>

URL obtained from the 8th level: 

`http://eth-lab.di.uniroma1.it:55413/eereezeighohfeim`

![](/writeups/unictf/image40.png)

The first thing we do was to try the *admin@admin:admin* username and password combination but without success. Then we investiga the source code looking for some information and we find a comment that said *“Never show the sessions.txt file”*.

![](/writeups/unictf/image2.png)

As usual we proceede to change the URL trying to open the *sessions.txt* file.

![](/writeups/unictf/image4.png)

After having seen the information in this file, we immediately understand what we have to do because we already know about attack where if you can steal a user session you can log in as that user.

While this session is saved in the cookie, we proceeded to open the cookie and change the value. To obtain the cookie we had to log in as guest user.

![](/writeups/unictf/image6.png)

Once in the page, we check if we received the cookie.

![](/writeups/unictf/image8.png)

We notice that the value of this cookie is different from the value found in the *sessions.txt* file.

![](/writeups/unictf/image10.png)

So, we proceede to change it, and our new cookie was:

![](/writeups/unictf/image12.png)

After reloading the page, we end up is the administrator’s page logged as him, where we can find the link for the next level.

![](/writeups/unictf/image14.png)

<h2 id=LV10> <span style="color:#da1953">Lev</span>el 10 </h2>

The link obtained from level 9:

`http://eth-lab.di.uniroma1.it:55255/leighaghuuzasaex/`

![](/writeups/unictf/image15.png)

As usual we tried the same combination (admin:admin) without any success.

Then we try many random combinations of usernames and password: for instance, we used some teacher’s usernames just in case we could get it correct, but they failed every time.

The last attempt is to proceed to analyse the source code of the web page where we find the following script:

![](/writeups/unictf/image16.png)

Inside the script there is a variable called *password_hashes* and seems to contain the correspondent encrypted password for each user.

![](/writeups/unictf/image17.png)

The first thing that came into our mind was MD5, so we proceeded to decrypt the hash with an online tool *haskiller.co.uk* (this site does not exit any more). It resulted to be a very good website where it is possible to encrypt and decrypt by using various algorithms.

In addition, you can also download their wordlist in case you need to proceed with an offline hash cracking.

![](/writeups/unictf/image66.png)

Obviously we take the hash of the user *admin* and try to log in with the new credential *admin:qwertyuiop* and we succeeded to proceed to the next level.

![](/writeups/unictf/image68.png)

But it does not end here because after decrypting the hash we notice that the function *checkPassword* does not decrypt the user input in order to access the admin page.

So, we tried to reverse the function in order to understand its logic.

![](/writeups/unictf/image69.png)

The function follows these steps:

1. Retrieve the values from the form and hash the given password.
2. It checks if the given user as input in the login form is in the dictionary “password_hashes”, if not it gives error.
3. If the user exists, it checks the computed hash with the stored hash, if they don’t match it gives error.
4. If also the hash matches, it generates the link for the next level by hashing again the input hash and taking the initial 8 characters so.

Just in case we are lucky to decrypt the hash we did the script process in order to solve the level.

![](/writeups/unictf/image71.png)

In fact, we can access the right page by adding *62aa4dcf.html* as the script is doing.

![](/writeups/unictf/image74.png)

---

<h2 id=LV11> <span style="color:#da1953">Lev</span>el 11 </h2>

We started from the following URL:

`http://eth-lab.di.uniroma1.it:55025/eepugeighovoorou/`

![](/writeups/unictf/image76.png)

The first attempt is to use few commonly used numbers such as *0000*, *12345*, *1337* but without any success.

As usual, we proceede to analyze the source code where we find a script like the previous levels and our attention was caught by a function called *checkPassword*.

![](/writeups/unictf/image79.png)

As we can see the `if` statement checks if the number is between 1 and 1000000 excluded, if it is *NaN* (empy form) and if it has at least six digits.

So, we supposed that a valid code could have been a number between 1 and 999999. Then the function hashes the code with MD5 with the salt *localsalt* and checks if the result hashing is equal to *4d1ea4c067daa4dec768540bbcfe80b2*.

The first idea was to decrypt the hash to retrieve the right value but due to the lack of online tool we proceeded to hash with salt all the passwords from 1 to 99999 and check which one matched the string: *“4d1ea4c067daa4dec768540bbcfe80b2”*.

In order to do it we write a python script.

![](/writeups/unictf/image81.png)

And this is the result produced by the script.

![](/writeups/unictf/image83.png)

As expected, the code works fine.

![](/writeups/unictf/image85.png)

---

<h2 id=LV12> <span style="color:#da1953">Lev</span>el 12 </h2>

The URL obtained from level 11:

`http://eth-lab.di.uniroma1.it:55528/ithochexephizoof`

![](/writeups/unictf/image65.png)

In this case, there is no form or text box where to write so we proceede by analyzing the code where, as usual, we find a script and we focused on a portion of the code.

![](/writeups/unictf/image44.png)

Here, we can see that the script creates a new link concatenating two string to complete the URL.

These strings are: *“cgi-bin/users.php”* and *“?filter=”*, after which a value is concatenated, but we don't know which kind of value could follow the string.

We decide to copy and paste the strings to the URL to complete it ourselves and appending something in order to execute an XSS since it was a JavaScript.

![](/writeups/unictf/image45.png)

We try several times but for some reason no one of our attempts work (in addition, we are not really good in JavaScript!).

Then we noticed what the home page was prompting: *daemon*, *root*, *mysql*, things that reminded us of Linux users so we tried to execute a simple Linux command instead of a JavaScript one.

![](/writeups/unictf/image46.png)

Once find the files in the directory we can try to open *secretusers.txt* with the command `cat`.

And the file contain the link for the next level.

![](/writeups/unictf/image48.png)

--

<h2 id=LV13> <span style="color:#da1953">Lev</span>el 13 </h2>

The starting point was the URL obtained from the previous level:

`http://eth-lab.di.uniroma1.it:55277/neifeesuopheeghu/`

![](/writeups/unictf/image50.png)

The first thing we do is to write something in the text box to see what happens and we try many different kinds of values to check how well it validates the input.

![](/writeups/unictf/image52.png)

As usual we proceede to analyze the code in search of information or scripts to reverse. In fact we find a script, and in particular we focus out attention on the function “getenv”.

In addition, we see the sanitize function on the user input which removes the illegal character from the input: that was the reason why it does not generate any kind of error.

![](/writeups/unictf/image54.png)

Also, here we can see the making of the URL like the previous levels so we attempted the same method as in the level 12 without any success.

![](/writeups/unictf/image56.png)

The response was -*“no variable found”* and also when we put an input it prints a *TESTENV* which recall something similar to the bash environment variable so we decide to do few researches to see if there were any vulnerability with the bash in the past or something similar.

![](/writeups/unictf/image58.png)

The first thing we find is something called “Shellshock”. The document explain what and how to exploit this vulnerability providing the string to use in order to execute remote shell commands.

The string is: `() { :;}; echo “NS:” $(</etc/passwd)`.

Digging more in the topic we can find a [pdf](https://owasp.org/www-pdf-archive/Shellshock_-_Tudor_Enache.pdf) where the shellshock vulnerability was explained alongside with its syntax.

![](/writeups/unictf/image41.png)

So again, we try to remake the right link appending *cgi-bin/env.php?filter=* and try to copy and paste the string suggested but for some reason no one of the two strings is working.

![](/writeups/unictf/image42.png)

During the laboratory lesson we have been suggested by the teacher to use **Burp** so we try again with burp.

First thing we do is to copy and paste the payload found on the internet on the link like we did with the browser but without any success.

![](/writeups/unictf/image22.jpg)

After few researches and random tries we figure out that we have to encode few characters and substitute the spaces with *+*.

So we encoded the “:” and “;” with “%3a” and “%3b” following the guide in this link, so our resulting payload was `()+{+%3a%3b}+/bin/ls` but still did not work for some reason.

![](/writeups/unictf/image23.jpg)

Then we remembered, after a lot of struggle, a file called *“user.php”* on the level 12 which has a particular comment.

![](/writeups/unictf/image25.jpg)

The referrer was disabled for that level and maybe it is enabled in this one, so we tried to add the referrer with our level URL.

![](/writeups/unictf/image27.jpg)

Which works perfectly, and we succeeded to list the directory content.

The next step is to read the *secret4uou0.txt* with the command `cat` so we send the payload with a different command `/bin/cat+secret4uou0.txt` where we find the link for the next level.

![](/writeups/unictf/image30.jpg)

---

<h2 id=LV14> <span style="color:#da1953">Lev</span>el 14 </h2>

The starting point was the URL obtained from the previous level:

`http://eth-lab.di.uniroma1.it:55424/aetiasaeghongohx`

At the beginning of this level we have no idea what to do, we try to register a user, we try to log in as *admin:admin* but nothing, then we remember our Lab class on XSS attack and we try to do it but without success.

Only after few days later we had a class on SQL Injection then we tried to do so.

First of all, we had to find where the vulnerability was, it could be in a form, since it is very common to find them there, or we could perform an injection from the URL.

We checked all the forms by writing inside the “ ’ ” character to see if we would get any query error, and we found it on the page “new user” on the field “username”.