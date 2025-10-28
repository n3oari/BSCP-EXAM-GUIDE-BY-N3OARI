# SSRF via OpenID dynamic client registration

We obtained the OpenID Connect configuration file:

`.well-known/openid-configuration`

![Screenshots1](/04-Screenshots/1-SSRF-via-OpenID-dynamic-client-registration.png)

We registered a user at `/reg` and obtained its `client\\\_id` following the OpenID Connect documentation, and in the process we triggered/executed an SSRF.

![Screenshots2](/04-Screenshots/2-SSRF-via-OpenID-dynamic-client-registration.png)

![Screenshots3](/04-Screenshots/3-SSRF-via-OpenID-dynamic-client-registration.png)

![Screenshots4](/04-Screenshots/4-SSRF-via-OpenID-dynamic-client-registration.png)



