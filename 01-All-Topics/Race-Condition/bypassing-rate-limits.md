# Bypassing rate limits via race conditions



In this lab, it was found that the login panel was protected by a Rate Limiting mechanism. To bypass this defense, the Burp Intruder tool (or the Turbo Intruder extension) was used.

The attack method consisted of adding every request generated from the wordlist to a single active TCP connection. Once the entirety of the payload dictionary had been prepared, all requests were sent simultaneously through the same TCP connection. By synchronizing the submission this way, the imposed rate limit was successfully bypassed.

`- Turbo intruder -> race-singe-packet-attack.py -> configure`

![](../../04-Screenshots/rate-limit.png)