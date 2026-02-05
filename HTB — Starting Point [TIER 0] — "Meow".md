# HTB — Starting Point [TIER 0] — "Meow"

`made on October 27, 2025`

Let's begin with our first exercise provided by HackTheBox! The process will be organized into steps that I will detail and accompany with screenshots showing how to put the actions into practice.

## 1. Establishing VPN connection
First, we connect to the VPN server provided by HackTheBox to perform the exercise under the specified conditions.

<p align="center">
    <img src="https://github.com/user-attachments/assets/4e2fa560-e3a7-4c5c-b266-11609d3f8991" width="600" />
</p>

## 2. Host status
Once we know the target's address (10.129.177.205), we will first run an Nmap scan. And we're gonna search if the target host is up or down with the -sn option.

<p align="center">
    <img src="https://github.com/user-attachments/assets/311aec59-bbc9-4fbe-9a05-01819fb13407" width="600" />
</p>

## 3. Scan
After we saw that the host is up, we can proceed to the port scan. With now the -sV option.

<p align="center">
    <img src="https://github.com/user-attachments/assets/e2b17f1e-004c-46c5-bde5-fdc7ecb03ff8" width="600" />
</p>

## 4. Pre-exploitation
Once we knew the open's port, we can do something. And for this case, the Telnet's port is open. After a quick research for how using the telnet protocol (I didn’t learn that protocol yet), we can simply access it with the command "telnet [target_IP]".

<p align="center">
    <img src="https://github.com/user-attachments/assets/93d1a89d-321e-4578-b61c-6cba6adc2029" width="600" />
</p>

## 5. Exploitation
Now, we face a authentification. Most of the time, the login can be root, or admin. Let's try root for login :

<p align="center">
    <img src="https://github.com/user-attachments/assets/afcd0a70-2790-470c-bf4d-f0d3eced85d3" width="600" />
</p>

## 6. Data recovery
It worked! Now, what we will do after entering the machine through the Telnet port is to run an 'ls' command to list the items present. And so we see the txt file named: **flag.txt** in the screenshot below.

<p align="center">
    <img src="https://github.com/user-attachments/assets/20254f90-9d23-4fa7-8466-348c8da707fb" width="600" />
</p>

And that’s it! We've just found the flag that we were looking for: **b40abdfe23665f766f9c61ecba8a4c19**