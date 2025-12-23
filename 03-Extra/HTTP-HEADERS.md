# MOST IMPORTANT HTTP HEADERS

- [MDN documentation](https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Headers)

```
- Host       -> indicates server domain
- Referer    -> indicates the previous web page from which a link redirected us
- Location   -> indicates the URL to which the user will be redirected
- Content-Security-Policy (CSP) -> specifies which resources can be loaded and executed on the web page
```

X-FORWARDED-*
```
- X-Forwarded-For   -> indicates the IP address of the client that connected to the proxy
- X-Forwarded-Host  -> indicates the Host header value sent by the client to the proxy
- X-Forwarded-Port  -> indicates the port the client used to connect to the proxy
- X-Forwarded-Proto -> indicates the protocol used by the client to connect to the proxy
```

CACHE
```
- Vary   -> specifies which request headers a cache should consider when storing a response
- Cache-Control -> defines caching directives for browsers and intermediate caches
- Pragma -> legacy header, mostly 'no-cache', used for HTTP/1.0 compatibility
- X-Cache: hit (cached) / miss (not cached) / dynamic / refresh -> indicates cache status
```

CORS
```
- Access-Control-Allow-Origin: * || <origin> || null -> specifies the allowed origin for cross-origin requests
- Access-Control-Allow-Credentials: true -> indicates whether credentials (cookies, HTTP auth) are allowed in cross-origin requests
- Origin -> indicates the origin of the request
```

Some typical/custom headers to bypass restrictions
```
X-Custom-IP-Authorization: 127.0.0.1
X-Forwarded-For: localhost
X-Forward-For: localhost
X-Remote-IP: localhost
X-Client-IP: localhost
X-Real-IP: localhost

X-Originating-IP: 127.0.0.1
X-Forwarded: 127.0.0.1
Forwarded-For: 127.0.0.1
X-Remote-Addr: 127.0.0.1
X-ProxyUser-Ip: 127.0.0.1
X-Original-URL: 127.0.0.1
Client-IP: 127.0.0.1
True-Client-IP: 127.0.0.1
Cluster-Client-IP: 127.0.0.1
X-ProxyUser-Ip: 127.0.0.1
```