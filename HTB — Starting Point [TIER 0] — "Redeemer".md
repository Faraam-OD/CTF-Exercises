# HTB — Starting Point [TIER 0] — "Redeemer"

`made on February 3, 2025`

For our last free Tier 0 box, we will take a look at the Redis service.

Redis is a powerful, open-source, in-memory data structure store used widely as a database, cache, and message broker. It keeps frequently used information in RAM (your computer's fast memory), so everything loads almost instantly.

It's mainly used to:

* Speed up websites (by temporarily storing often-requested data)
* Remember user actions during their visit
* Enable real-time updates

In short, Redis is the turbo boost that cuts out unnecessary waiting.

Okay, now, let's take a look at our exercise together!

## 1. HOST STATUS
We have now gotten into the habit of pinging to confirm the connection to the target machine. Of course, it responds. This means that our VPN connection to the machine is working. We can now move on to the next step.