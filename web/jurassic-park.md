---
grand_parent: Categories
parent: Web
title: Jurassic Park
nav_order: 1
---

# Jurassic Park

```
Dr. John Hammond has put together a small portfolio about himself for his new theme park, Jurassic Park. Check it out here!
```

## Challenge

> TL;DR: Classic `robots.txt` warmup challenge.

Visiting the challenge site, we are greeted with a simple page with nothing dynamic to try.

<img src="images/jurassic-1.png">

Since this was likely intended, we can always try to look for the `robots.txt` to see if there are any "hidden" directories.

<img src="images/jurassic-2.png">

Sure enough, a directory `/ingen/` existed. Browsing to it, we see the flag itself:

<img src="images/jurassic-3.png">

Flag: `flag{c2145f65df7f5895822eb249e25028fa}`
