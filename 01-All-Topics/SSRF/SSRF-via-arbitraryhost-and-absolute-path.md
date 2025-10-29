---
tags:
  - BSCP
  - lab
---
In Burp Intruder we perform a brute-force attack against the **Host**.

> ❗ Important: disable the **Update Host header to match target** option

![[Pasted image 20251029185545.png]]

Once we identify the IP that redirects to **/admin**, we gather any relevant information.

![[Pasted image 20251029185918.png]]

Using that information, we can successfully trigger the SSRF:

![[Pasted image 20251029190038.png]]


Below is an example from a different lab where only the Host header injection method changes — the Intruder methodology is the same.

In this variant we obtain the Host header by using an absolute URL in the GET request. In some server configurations, sending an absolute path/URL causes the server to use that value instead of the original Host header, allowing the same SSRF technique to succeed


![[Pasted image 20251029191640.png]]
