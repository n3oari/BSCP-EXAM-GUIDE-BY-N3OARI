# Web Cache Poisoning - CHEATSHEET + LABS

## Key Terms

```bash
- Param Miner -> Burpsutie Extension 
- Cache oracle -> an endpoint that reveals cache behavior 
- Cache Buster -> Used to test the cache without affecting the website’s functionality e.g -> /?cb=x
- Unkeyed Input -> Element that does not influence the cache key (potential attack vector)
- Cloaking Param -> Parameter/Header ignored by the cache but used by the backend eg -> /?callback=setCountryCookie&utm_content=x;callback=alert(1)

- X-Forwarded-For -> Forwards the original client IP address through proxies; can be abused to influence backend logic that trusts client IP.
- X-Forwarded-Host -> Forwards the original Host header (the hostname used by the client); can be used to craft redirects or host-based logic.
- X-Forwarded-Scheme: nohttps -> Indicates the original scheme 
- X-Forwarded-Proto: original protocol used by the client, typically http or https
- Pragma: x-get-cache-key -> A request hint used to ask the server (or a diagnostic endpoint) to reveal or compute the cache key for that request.
- Vary  Specifies which parts of the request should be included in the cache key
- X-Cache: hit (cached) / miss (not cached) / dynamic / refresh

```

## Walkthrough - Most Important Labs

- [Unkeyed key in cookie](cookie-unkeyed-key.md)

- [web cache poisoning via multuiple header](webcachepoisoning-with-multiple-headers.md)

- [Custom header + unkeyed user agent (found via vary header)](custom-header-vary-steal-useragent.md)

- [Unkeyed input utm_content + parameter poisoining via fat GET request body](unkeyed-fat-get.md)

- [Parameter Cloaking via utm_content](parameter-cloaking.md)


## Metodology

```bash
-- RECON -- 
- Param Miner
	-> Guess headers / intentar multiples 
	-> Guess params 
	-> Guess everything!

- Static files / dirs -> .js , .css , robots.txt , /static /assest, etc.
- Large differences in response time for the same request can indicate cached vs non-cached responses

-- BASIC FLOW --

- 1 -> Identify a potential cache oracle (an endpoint that reveals cache behavior)
- 2 -> Param Miner 
- 3 -> Find a cache-buster to run safe tests without breaking functionality
- 4 -> Locate unkeyed input  (in url, cookie, headers,fat body get.., param cloaking)
- 5 -> Locate headers
- 6 -> Inject a benign payload to confirm cache impact/behavior 


- CORS? ->  Access-Control-Allow-Origin: *
- Try overriding parameters (e.g., see if server accepts parameters in unexpected places, such as a GET body) — observe how the cache reacts
```

#### Example methodology guess headers :

1 - Find oracle cache

2 - Find cache buster to test


![Screenshot1](/04-Screenshots/recon1.png)


3 - Extensions + param miner -> Guest headers


![Screenshot2](/04-Screenshots/recon2.png)

4 - Redirect to our server


![Screenshot3](/04-Screenshots/recon3.png)


5 - Finally  test the cache buster endpoint.  
If the cache buster behaves correctly, remove it and perform the same test on a critical or user-facing endpoint.