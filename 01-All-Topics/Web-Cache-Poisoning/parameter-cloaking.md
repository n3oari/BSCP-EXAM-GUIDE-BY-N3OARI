# Parameter Cloaking via unkeyed param (utm_content)

In this lab we obtained the following information:

- Unkeyed input used as a parameter (utm_content)
- Cache buster used for testing in the Origin header
- Cloaking parameter coming from the utm_content parameter

![Screenshot1](/04-Screenshots/cloaking0.png)

![Screenshot2](/04-Screenshots/cloaking1.png)

Once the XSS was confirmed, we removed the cache buster from Origin header.