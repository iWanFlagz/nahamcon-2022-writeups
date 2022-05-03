---
grand_parent: Categories
parent: Mobile
title: OTP Vault
nav_order: 1
---

# OTP Vault

```
I created my own vault application to store my secrets. It uses OTP to unlock the vault so no one can steal my password!
```

## Challenge

> TL;DR: React native mobile app, can further decompile `index.android.bundle` to get app source.

<img src="images/otp.png"><br>

Examining the source code of the APK with `JADX`, we can see multiple references to `com.facebook.react` indicating that this is a mobile app built with the React Framework.

<img src="images/otp-1.png"><br>

Unzip the APK file and extract the `assets/index.android.bundle` file. We can further decompile this file using [react-native-decompiler](https://github.com/richardfuca/react-native-decompiler) to retrieve the source code of the app.

<img src="images/otp-2.png"><br>

After decompiling, navigate to the output folder and we can see many `.js` files being generated. The file of interest here is `396.js`, containg our OTP secret and `getFlag` function:

```js
    function O() {
    let n;
    module7.default(this, O);
    (n = b.call(this, ...args)).state = {
      output: 'Insert your OTP to unlock your vault',
      text: '',
    };
    n.s = 'JJ2XG5CIMFRWW2LOM4';
    n.url = 'http://congon4tor.com:7777';
    n.token = '652W8NxdsHFTorqLXgo=';

    n.getFlag = function () {
      let module7;
      let o;
      return regeneratorRuntime.default.async(
        (u) => {
          for (;;) {
            switch ((u.prev = u.next)) {
              case 0:
                u.prev = 0;
                module7 = {
                  headers: {
                    Authorization: 'Bearer KMGQ0YTYgIMTk5Mjc2NzZY4OMjJlNzAC0WU2DgiYzE41ZDwN',
                  },
                };
                u.next = 4;
                return regeneratorRuntime.default.awrap(module400.default.get(`${n.url}/flag`, module7));
```

Now, to get the flag we can either input the OTP secret to any MFA app and generate the OTP and key it into the app, or simply send a request to the server:

```bash
curl -H "Authorization: Bearer KMGQ0YTYgIMTk5Mjc2NzZY4OMjJlNzAC0WU2DgiYzE41ZDwN" http://congon4tor.com:7777/flag
```

Flag: `flag{5450384e093a0444e6d3d39795dd7ddd}`
