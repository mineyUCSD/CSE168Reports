# Lab Report 1
## Tutorial for incoming 15L students about how to log into a course specific account on ieng6  

There are three steps  

* **Installing VScode**
*  **Remotely Connecting**
*  **Trying Some Commands**

I will go down the list

---

# Installing VScode

If you are on a lab computer VScode should already be installed, but if you are using a personal computer without it
you must download the application

Luckily, it is straightforward

Step 1: Go to Visual Studio Code Website [https://code.visualstudio.com/](https://code.visualstudio.com/)

Step 2: Download whatcha need for your OS

---

After it is installed, open the application, it should look something like

![image](https://user-images.githubusercontent.com/130080241/230698448-c1a15408-50d0-4394-a36b-6253b17c3c62.png)

---

# Remotely Connecting

The point of this section is to connect to a remote computer by way of the Internet

To connect to the ieng6, you must also access your cs15l account and change the password.

## CSE15L Account

Follow this link to access you cse15L account [Account Lookup](https://sdacs.ucsd.edu/~icc/index.php)

In this page, enter your UCSD username and PID
![image](https://user-images.githubusercontent.com/130080241/233241452-92551f6f-78ab-4c47-86f9-626c26516829.png)

---
It should take you to a page like this

![image](https://user-images.githubusercontent.com/130080241/233242068-008c6505-4523-487f-9573-42e7a986f6a6.png)

Inside the gray box is your username. Remember it, write it down, maybe even copy and paste it to a file and for safe keeping. You will need to refer to it both when reseting your password and then in connecting to the remote server.

---

From the new page, select the Global Password Change tool

![image](https://user-images.githubusercontent.com/130080241/233242589-cd8233c3-99ef-438a-897d-8ce8fc324aed.png)

---

Then Proceed to the Password Change tool 

![image](https://user-images.githubusercontent.com/130080241/233242720-dfd750f5-3a50-4d15-8e16-62bbb56aaae6.png)

---

Enter your cs15L username! After you enter it, you should recieve an email to your UCSD email containing a link that will direct you to where you change your password

![image](https://user-images.githubusercontent.com/130080241/233242812-a3bfad3d-9254-41a7-833f-c57273b44e5c.png)

---

Finally, enter a new password, and make sure it is good, and make sure you remember it!

![image](https://user-images.githubusercontent.com/130080241/233243723-d8584343-7b16-415d-b344-69738680b11a.png)

Assuming you followed the steps correctly, it is probable that you reset your password and now have access to your CS15L account!!!!
**Congratulations.** 😄

---

## Git

Next, make sure to download git for Windows if you are on Windows and do not have it installed

---

[git for Windows](https://gitforwindows.org/)

![image](https://user-images.githubusercontent.com/130080241/230443663-d46e105a-a958-42d5-8f5d-e96547fc7b4f.png)

---

Once installed, use the git bash terminal in VScode

Set Bash terminal as default in VScode following these [instructions](https://stackoverflow.com/a/50527994)

Open a terminal in VScode using the shortcut ```` Ctrl or Command + ` ```` , type in the command `#ssh cs15lsp23zz@ieng6.ucsd.edu` , replacing `zz` with the two letters in your username

Since this is the first time sshing into the server, you should get a message like this

```
ssh cs15lsp23zz@ieng6.ucsd.edu
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 

```
Just have some faith, type 'yes', press enter

Then, the terminal will prompt you for a password. You cannot see the password as you enter it in, so maybe copy and paste it in. The final interaction should look something like this after inputting the correct password for your account: 

![image](https://user-images.githubusercontent.com/130080241/230698149-b227a1fb-34b6-463b-bcf4-ca4ac7095b2c.png)


At this point, you have succesfully remotely connected to the server!!! :joy:

---

# Trying Some Commands


There are tons of commands! Here are some of the ones I know and have tested so far

* `ls` - Lists Directory contents
* `pwd` - Prints Working Directory
* `cd` - Changes Directory
* `..` - Goes to Parent Directory, or the one outside current directory
* `cat` - prints out contents of file, can be more than one and doesn't need to be .txt
* `mkdir` - makes a directory
* `touch` - has some commands and can be used to make files
* `nano` - file editor

Here is a reference for more commands: [https://github.com/trinib/Linux-Bash-Commands](https://github.com/trinib/Linux-Bash-Commands)

---
## Playing with Commands

---

### File Stuff

So, I started out using `ls` to see what is in my current path

![image](https://user-images.githubusercontent.com/130080241/230699080-2fcccf46-4847-4db1-851d-52012d800b0f.png)

It is this thingy called perl5, and I want to know what that is, so I try to `cat` it

![image](https://user-images.githubusercontent.com/130080241/230699121-dfd82796-5c19-49ce-895f-20f157219a08.png)

Apparently it is a directory! 😺 Um, I guess I will `pwd`

![image](https://user-images.githubusercontent.com/130080241/230699198-3b30ad95-1e38-4e19-a4d6-eacb69802ce3.png)

That is my current working directory; Ima add a file in cs15lsp23et using `touch -m` and then `ls` to show it was created

![image](https://user-images.githubusercontent.com/130080241/230699257-5304d416-4a74-4ff2-9571-4ebe61c6d995.png)

Now I want to add some text to the `helloWorld.txt` file. To do this, I used a command called `nano`. It opens a text editor looking thingy.

![image](https://user-images.githubusercontent.com/130080241/230699465-85ef6a24-66a9-40b3-bcac-f300424df902.png)

I added in `Hello World!` to the file and saved it, and then `cat`ed it to see if it worked properly!

![image](https://user-images.githubusercontent.com/130080241/230699510-9ff5fcbf-b5a9-4d4b-9e40-b8ab744b41de.png)

![image](https://user-images.githubusercontent.com/130080241/230699527-4dcd50dc-0f45-43a2-be28-ceda73cae69d.png)

Great Success!!! 🥳🥳🥳

---

### Directory Stuff

I take a step out of the home directory using the command `cd ..` and then print the working directory using `pwd`

![image](https://user-images.githubusercontent.com/130080241/230699698-5354d45b-9c0b-407a-af5a-1116149836ff.png)

And time to see what is in this path ... using `ls`

![image](https://user-images.githubusercontent.com/130080241/230699784-304a2562-cd3f-40c3-abc4-a49e3e925f90.png)

***Wow!*** It is all of the users in the class, at least I suspect. I underlined my user, in there rests helloWorld.txt!

*So.....* I tried to `cd` into another person's directory to see what files they had, but

![image](https://user-images.githubusercontent.com/130080241/230699872-0bd69551-e73c-4018-b2a5-66e171751722.png)

PERMISSION DENIED

Oh well, I'll keep to my own files. I return to home directory using `cd ~`. I want to see what is in perl5, so I `ls`. Barren! Ima add a directory called stuff using `mkdir`

![image](https://user-images.githubusercontent.com/130080241/230700237-c69b1655-2ebc-4200-99c5-a8931aa3bb1f.png)


ummm, so now there is stuff in perl5. I have played with all of the commands I know. I think this is sufficient. Thus, `exit`

![image](https://user-images.githubusercontent.com/130080241/230700205-1eab0e5e-efc9-4bbe-bab1-755d98944d5d.png)

---




































