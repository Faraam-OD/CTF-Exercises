# HTB — Starting Point [TIER 0] — "Fawn"

`made on November 30, 2025`

For this second introductory exercise on pentesting, we will look at the use of FTP.

## 1. Host status
First, let's see if the connection to the target IP is working by sending a ping.

<p align="center">
    <img src="https://github.com/user-attachments/assets/8439ec78-87d4-43db-ab04-8c7a7289cbcf" width="600" />
</p>

Okay, as we can see, all of our return packets (pong) have responded. So we can continue.

## 2. Scan
Now, let's run a Nmap scan on the target IP

<p align="center">
    <img src="https://github.com/user-attachments/assets/54d4369c-8faa-4f1e-a638-c4bdc4559559" width="600" />
</p>

We can see that port **21** (FTP) is open. And that the OS on which the machine runs is Unix-based.

*(But what is FTP ? ─ It's the File Transport Protocol. It is an old protocol that allows (even though it is no longer used) files to be transferred between two computers on a network. It uses a client-server model)*

Now, we want to know how to access to this machine and get the flag.

For that, we need to know how to access with FTP protocol. For this, we will need to install FTP on our machine if it is not already installed. For this, it's quite simple, you'll need to run the following command : `sudo apt install ftp`

## 3. Pre-exploitation
Now, we need to know how to use FTP protocol and access to the flag

For knowing what options uses, we can write `ftp -?`. And one option is particularly interested for us, it's the `-a` option that use anonymous login. Because we won't even have to enter a username (in this case "anonymous" and a password). *That is a misconfiguration of FTP who his services allows an anonymous account to access the service like any other authenticated user. Once the username "anonymous" entered (in the case we don't add the "-a" option when connecting, we can add absolutely any passwords because the service will ignore the password for that specific account).*

So, the commande will be this : `ftp -a 10.129.1.14`

<p align="center">
    <img src="https://github.com/user-attachments/assets/c7cdd0f6-b3bc-4535-9f9c-88216ae91009" width="400" />
</p>

## 4. Exploitation
Now entered, the first things we can do, is a simple linux command ; `ls` to show whether files or folders are present there.

<p align="center">
    <img src="https://github.com/user-attachments/assets/e4e7c3b6-64f1-4e6d-b5d5-5d24b322f1ad" width="600" />
</p>

Okay! We can see that the flag is there already! But that's all? We just have to concatenate (cat) the file and we'll have the flag!…

But nah, on FTP, the `cat` command doesn't exist. So we need to know how to open the content of this file. For this, we simply gonna use the `help` command to know what and which command write to obtain what we want.

So:

<p align="center">
    <img src="https://github.com/user-attachments/assets/63e068ae-a391-438d-b886-37a8fbcb8628" width="600" />
</p>

The command `get` can be what we're searching for. Because let us remember that FTP is a file Transfer before all. So, for discover the content of the flag, we need to Transfer the file with the `get` command on our machine, to after, open it.

Let’s see!

<p align="center">
    <img src="https://github.com/user-attachments/assets/469e4d4d-b69e-45df-942b-8a0b69ff8b7c" width="600" />
</p>

## 5. Data recovery
Find and open the content of the flag in our machine

Now, we exit the FTP access simply with `exit`, and we will check whether the transferred file is on our machine and, if so, open it. To easily locate where the file is located, we just need to run the following `find` command : `find / -name flag.txt 2>/dev/null`

*(2>/dev/null is used to avoid search results for which permission is not granted)*

<p align="center">
    <img src="https://github.com/user-attachments/assets/06bf5fed-612a-4fb8-946a-d147d31762da" width="400" />
</p>

Okay! He's simply in the **/home** directory. Now, we can finally concatenate our file! :

<p align="center">
    <img src="https://github.com/user-attachments/assets/b11e7fe4-104b-4e0b-92ac-b55aac40a068" width="400" />
</p>

Here’s the flag!