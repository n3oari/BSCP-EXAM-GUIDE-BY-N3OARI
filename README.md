# TEST MAIN README

This wiki contains each cheatsheet along with its respective most important labs.

Each topic includes its own cheatsheet/methodology, the most relevant labs, and useful resources.

<br>

>⭐This is the result of months of work — I hope you find it helpful. If you do, please leave a star. ⭐

<br>

![Screenshot1](/04-Screenshots/obsidian.png) 

<br>

- [Tips and tricks before taking exam](/03-Extra/TIPS.md)

- [Most Important HTTP Headers](/03-Extra/HTTP-HEADERS.md)

- [HTB machines I recommended for each topic](/03-Extra/HTB-machines.md)

- [Burpsuite cheatsheet & tricks](/03-Extra/Burpsuite-CHEATSHEET.md)

<br>

> ❗This repository contains **my own** cheatsheets and methodologies for the exam — **not PortSwigger's**. You may consult PortSwigger's resources if you wish, but the files here are my personal notes.

> ❗I highly recommend creating **your own** cheatsheets. This repository is intended to help others, provide examples, show the overall organization, and demonstrate my work and methodologies.

> ❗This repository is a summary of all my Obsidian notes for the BSCP. I learned a lot while creating it because I focused on making it as clear and didactic as possible, fully internalizing all the concepts to be able to explain them correctly. This repo was created **before passing the exam**.

<br>
The following are basic resources offered by PortSwigger for the exam:

- [usernames wordlist](https://portswigger.net/web-security/authentication/auth-lab-usernames)  
- [passwords wordlist](https://portswigger.net/web-security/authentication/auth-lab-passwords)  
- [URL validation bypass cheat sheet (SSRF)](https://portswigger.net/web-security/ssrf/url-validation-bypass-cheat-sheet)  
- [delimiters wordlist (web cache deception)](https://portswigger.net/web-security/web-cache-deception/wcd-lab-delimiter-list)

---

The exam consists of **2 machines**, each with **3 phases**, and a duration of **4 hours**.
  - 1: Access any user account.
  - 2: Elevate privileges or compromising the administrator account.
  - 3: Exfiltrate contents of /home/carlos/secret and **submit solution**

 <br>

> ⚠️ This is a reference — please, always verify and research on your own.

<br>

<div align="center">

| Category  | Stage 1 | Stage 2 | Stage 3 |
|:--------:|:-------:|:-------:|:-------:|
| XSS      |   ✔️    |     ✔️    |         |
| DOM |         |         |         |
| SQLI |         |         |         |
| CSRF |      ✔️   |     ✔️    |         |
| SSRF |         |         |         |
| X |         |         |         |
| X |         |         |         |
| X |         |         |         |
| X |         |         |         |

</div>

<br>

### PHASE 1 → Obtain Inicial User

##### Enumeration & Web Discovery

- [API testing / recon](01-All-Topics/API-testing/01-CHEATSHEET+LABS.md)

##### Authentication

- [Authentication / Brute-Force](01-All-Topics/Authentication/01-CHEATSHEET+LABS.md)
- [OAuth](01-All-Topics/OAuth/01-CHEATSHEET+LABS.md)
- [Host Header Injection](01-All-Topics/Host-Header-Injection/01-CHEATSHEET+LABS.md) 


### PHASE 2 → Elevate Privileges 









- [CSRF](01-All-Topics/CSRF/01-CHEATSHEET+LABS.md)

### PHASE 3 → Exfiltrate Data
