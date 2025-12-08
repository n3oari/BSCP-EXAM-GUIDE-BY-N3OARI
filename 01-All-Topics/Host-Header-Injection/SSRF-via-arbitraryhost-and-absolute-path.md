# Routing-based SSRF via arbitraty host + EXTRA: absolute path

In Burp Intruder we perform a brute-force attack against the **Host**.

> ❗ Important: disable the **Update Host header to match target** option


![Screenshot1](/04-Screenshots/absolute1.png)

Once we identify the IP that redirects to **/admin**, we gather any relevant information.


![Screenshot2](/04-Screenshots/absolute2.png)


Using that information, we can successfully trigger the SSRF:


![Screenshot3](/04-Screenshots/absolute3.png)

**EXTRA LAB: Absolute Path**

Below is an example from a different lab where only the Host header injection method changes — the Intruder methodology is the same.

In this variant we obtain the Host header by using an absolute URL in the GET request. In some server configurations, sending an absolute path/URL causes the server to use that value instead of the original Host header, allowing the same SSRF technique to succeed


![Screenshot4](/04-Screenshots/absolute4.png)
