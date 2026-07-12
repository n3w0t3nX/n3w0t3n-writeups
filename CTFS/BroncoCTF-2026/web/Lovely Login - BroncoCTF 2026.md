بسم الله الرحمن الرحيم  - اللهم صلي على سيدنا محمد 

## Challenge Description

> Welcome to our lovely new login page 💕. The developers swear it’s secure… but they may have forgotten to clean up a few things before launch.
>
> Can you figure out how authentication works and log in as the right user?
>
> **P.S.** Please follow my wishes and do not scrape it...

https://broncoctf-lovely-login.chals.io/

---

![[login.png]]

At first glance, it looks like a normal internal login page.

I tried a few common credentials such as:

```text
admin:admin
support:support
```

but nothing worked.

As usual, I viewed the page source using `Ctrl + U`.

There wasn't anything interesting except that the login request is sent to the `/login` endpoint, and the response is displayed inside the following HTML element:

```html
<div id="out"></div>
```

![[out.png]]

Since nothing useful appeared in the source code, I started my usual directory fuzzing using **dirsearch**.

```bash
dirsearch -u https://broncoctf-lovely-login.chals.io/
```

It returned two interesting endpoints:

```text
[16:11:30] 200 -   71B  - /robots.txt
[16:11:31] 200 -  387B  - /security
```

I checked the `robots.txt` file first.

```txt
User-agent: *
Disallow: /security

# amVmZixzYXJhaCxhZG1pbixndWVzdA==
```

The last line looked like Base64, so I decoded it.

![[base64.png]]

Now we have four possible usernames:

```text
jeff
sarah
admin
guest
```

Before trying them manually or starting a brute-force attack, I decided to check the other endpoint.

```
/security
```

![[security.png]]

It seems the developers forgot to remove their internal security notes before deployment.

![[qasrelmemez_يا_ريتني_ما_سألت_فيلم_تمبلت_الباشا_تلميذ_كريم_عبد_العزيز.png]]

## Summarizing the notes

The page reveals two important details:

- Passwords are derived from usernames.
- They are simply stored **backwards** instead of being hashed.

So if the username is:

```text
jeff
```

the password becomes:

```text
ffej
```

That means the administrator credentials should be:

```text
admin:nimda
```

And... it worked.

![[BroncoCTF-2026/web/images/flag.png]]

### Flag

```text
bronco{R3v3rs1ng_1s_S3cure}
```


*Thank u for reading .*
*متنساش تصلي على النبي :>*