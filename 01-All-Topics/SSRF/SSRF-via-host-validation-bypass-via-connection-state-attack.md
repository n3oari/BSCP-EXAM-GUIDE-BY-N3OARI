---
tags:
  - lab
  - BSCP
  - github-repo
---
In this lab the back end strictly validates every parameter

![[Pasted image 20251029193503.png]]

If we try to send a Host value different from the expected one, we are redirected to the root:

![[Pasted image 20251029193622.png]]

To achieve an SSRF here we must send **two HTTP requests over the same TCP connection**.

The back end validates **only the first request** it receives on that connection; once it confirms the first request is correct it does not re-validate the second one.

![[Pasted image 20251029193937.png]]
![[Pasted image 20251029194017.png]]


We use the SSRF to look for sensitive information:


![[Pasted image 20251029194145.png]]

Finally we trigger the SSRF:

![[Pasted image 20251029194235.png]]