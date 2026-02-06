# HTB — Starting Point [TIER 0] — "Redeemer"

`made on February 3, 2025`

For our last free Tier 0 box, we will take a look at the Redis service.

Redis is a powerful, open-source, in-memory data structure store used widely as a database, cache, and message broker. It keeps frequently used information in RAM (your computer's fast memory), so everything loads almost instantly.

It's mainly used to:

* **Speed up websites** (by temporarily storing often-requested data)
* **Remember user actions during their visit**
* **Enable real-time updates**

In short, Redis is the turbo boost that cuts out unnecessary waiting.

Okay, now, let's take a look at our exercise together!

## 1. HOST STATUS
We have now gotten into the habit of pinging to confirm the connection to the target machine. Of course, it responds. This means that our VPN connection to the machine is working. We can now move on to the next step.

<p align="center">
    <img src="https://github.com/user-attachments/assets/90fea70b-d417-4216-bd08-83803f50c6da" width="600" />
</p>

The Time To Live is 63, which very often results in a Unix-based machine, i.e. Linux.

## 2. SCAN
Since we know that the exercise focuses on the Redis service, we just had to find out which port Redis was based on and scan that (6379). This saves us from scanning all 65,535 ports and wasting time (and triggering the IDS in the process, haha).

<p align="center">
    <img src="https://github.com/user-attachments/assets/1d0ef9ce-70e4-40bc-97db-8c2fcbec76ba" width="600" />
</p>

As we can see, the Redis service is indeed open. We can then begin the intrusion.

## 3. Pre-exploitation
After a quick Google search, I saw that for access the Redis interface, we must connect using the command: `redis-cli -h [ip_address] -p 6379`

`-h` followed by the specific target IP address indicates which machine we want to connect to, and `-p`, as you may have guessed, specifies the port number used by Redis.

That's gives on the screen :

<p align="center">
    <img src="https://github.com/user-attachments/assets/027f08b8-a6e9-48a8-9929-e7ee0c2fbefb" width="600" />
</p>

Okay, we are connected to the Redis interface. What we can do now is retrieve information about the Redis server. To do this, simply entering the command `info` will give us our answers :

<p align="center">
    <img src="https://github.com/user-attachments/assets/7cb74819-c95e-412a-a719-eb83c16e2c51" width="400" />
</p>

The information shared is lengthy; we have details on **memory**, **persistence**, and other statistics. So I'm only going to show the section that interests us here. And that's the last section, called "**Keyspace**".

<p align="center">
    <img src="https://github.com/user-attachments/assets/343f939f-9c20-4c1f-87d4-1c0e1d2f4880" width="400" />
</p>

## 4. Exploitation
Now we need to see how to display these four keys. After a quick Google search, I found that to display them, all I had to do was enter the command:

* `keys *`

This listed all the keys present on the server.

<p align="center">
    <img src="https://github.com/user-attachments/assets/f8742ed5-d830-4c6a-80b2-abbcfee496e3" width="400" />
</p>

## 5. Data recovery
As we can see, one of the keys contains the flag we are looking for to validate this exercise. The syntax to retrieve this key is as follows:

* `get "[key_name]"`

<p align="center">
    <img src="https://github.com/user-attachments/assets/0554f158-f36f-4181-adab-ea024fedf1b8" width="400" />
</p>

And that's it! We have recovered the flag and validated the exercise.