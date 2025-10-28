# SSRF via OpenID dynamic client registration

We obtained the OpenID Connect configuration file:


`.well-known/openid-configuration`


![[/Screenshots/1-SSRF-via-OpenID-dynamic-client-registration.png]]


We registered a user at `/reg` and obtained its `client\\\_id` following the OpenID Connect documentation, and in the process we triggered/executed an SSRF.

![[/Screenshots/2-SSRF-via-OpenID-dynamic-client-registration.png]]

![[/Screenshots/3-SSRF-via-OpenID-dynamic-client-registration.png]]

![[/Screenshots/4-SSRF-via-OpenID-dynamic-client-registration.png]]



