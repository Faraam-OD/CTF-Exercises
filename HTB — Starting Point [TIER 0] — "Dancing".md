# HTB — Starting Point [TIER 0] — "Dancing"

`made on December 21, 2025`

We're back with our third box, but this time focused on a Windows protocol: **SMB**.

SMB stands for **Server Message Block** on Windows, and **Samba** on Linux environment, and operates on port 445.

SMB is a network communication protocol used for sharing files, printers, and other resources between computers on a network. It allows applications to read and write to files on remote servers, facilitating resource access and inter-process communication.

So, let’s dive into our box!

## 1. HOST STATUS
First of all, after we're connected to HTB's IP target, we need to make sure that the IP is up. We should get into the habit of sending a ping to be sure before we start.

<p align="center">
    <img src="https://github.com/user-attachments/assets/86d7d245-b4cd-42e5-88f7-0240ee8bc6bc" width="600" />
</p>

Okay, perfect, and we can see that the TTL (Time To Live) is 127, which is typically the TTL for Windows machines. Let's continue.

## 2. SCAN
What we need to do now, is to scan the target IP to discover what ports are open. Nmap are still our best friend for this. Let's bring him up :

<p align="center">
    <img src="https://github.com/user-attachments/assets/d24a51c4-f43d-4655-a808-4526b52b06be" width="600" />
</p>

We can see that port 445, which is used for **SMB**, is open. We can now begin the intrusion stage.

## 3. Pre-exploitation
To access the SMB connection, we need to use the **smbclient** command. By simply entering this command, we can see the smbclient usage commands displayed on the screen.

<p align="center">
    <img src="https://github.com/user-attachments/assets/04809c88-7c06-4096-ab35-c84d7abd2a5f" width="600" />
</p>

We can't see well on the picture, but the command we are interested in here is the one boxed in red, namely the **-L** command for "**list**".

So, to access the content, we will use the following command; (and as you can see, we used the "**-N**" option. This option makes the SMB protocol vulnerable because it allows you to connect to the service under "**Anonymous**" status, enabling you to connect **without a password**.)

<p align="center">
    <img src="https://github.com/user-attachments/assets/b32c902c-4b4c-4ee2-b64b-4f4acc9cfcfb" width="600" />
</p>

## 4. Exploitation
But now, how do we navigate between those files to know where is hiding our flag? To do this, we had to do some research on SMB syntax, particularly regarding navigation. To do this, simply type: **smbclient \\\[target_IP]\\[directory]**

And we must do this on each of the directories present in order to find the one that contains files.

As we can see in the screenshot, the first three folders are inaccessible. Unlike the fourth one...

<p align="center">
    <img src="https://github.com/user-attachments/assets/1712893f-62a2-4313-a7e1-2f80244cfc4b" width="600" />
</p>

So we finally have access to the directory! We have Amy.J and James.P.

And as can be seen above, the flag was located in the James.P directory. To do this, as indicated, we had to use the "**get**" command to transfer the file to our machine. Now, the last thing we need to do is open the file on our machine to find out the flag.

## 5. Data recovery

Now, all we have to do is find our downloaded file on our desktop simply by using the 'ls' command. Very often, the downloaded file is automatically placed in the "Desktop" folder.

<p align="center">
    <img src="https://github.com/user-attachments/assets/ab756fe3-a639-42b3-8d75-95550548aa9e" width="600" />
</p>

Here’s the flag!