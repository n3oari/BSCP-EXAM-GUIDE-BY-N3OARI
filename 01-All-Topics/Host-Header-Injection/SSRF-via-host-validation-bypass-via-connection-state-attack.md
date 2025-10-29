# SSRF-via-host-validation-bypass-via-connection-state-attack

In this lab the back end strictly validates every parameter

![Screenshot1](/04-Screenshots/hosti-single-con1.png)

If we try to send a Host value different from the expected one, we are redirected to the root:

![Screenshot1](/04-Screenshots/hosti-single-con2.png)

To achieve an SSRF here we must send **two HTTP requests over the same TCP connection**.

The back end validates **only the first request** it receives on that connection; once it confirms the first request is correct it does not re-validate the second one.

![Screenshot2](/04-Screenshots/hosti-single-con3.png)


![Screenshot3](/04-Screenshots/hosti-single-con4.png)


We use the SSRF to look for sensitive information:


![Screenshot4](/04-Screenshots/hosti-single-con5.png)

Finally we trigger the SSRF:

![Screenshot5](/04-Screenshots/hosti-single-con6.png)