
# Host-header-injection-via-web-cache-poisoning+xss

We found that the server cache the response:

![Screenshot1](/04-Screenshots/hostcache-xss1.png)

We look for an **unkeyed input** and test different **Host header injection** techniques.

We discover that when the **Host header is duplicated**, it gets successfully injected.

![Screenshot2](/04-Screenshots/hostcache-xss2.png)


![Screenshot3](/04-Screenshots/hostcache-xss3.png)