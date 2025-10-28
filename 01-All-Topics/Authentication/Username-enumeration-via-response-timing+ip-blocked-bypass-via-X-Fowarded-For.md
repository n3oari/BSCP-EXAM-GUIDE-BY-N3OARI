# Username enumeration via response timing  + ip blocked bypass via X-Fowarded-For

In this lab we recover the password by observing the Response Time / Response Time Completed.

>Workflow - Pitchfork attack:

- 1: Use the `X-Forwarded-For` header found with ParamMiner to bypass IP-based blocking

- 2: Brute-force the username and put a **VERY LONG** password in the password field so that when the username is correct, the backend takes noticeably longer to verify the password than for other requests    
  
- 3: Brute-force the password


![Screenshot1](/04-Screenshots/response-time-long-pass1.png)

![Screenshot2](/04-Screenshots/response-time-long-pass2.png)

