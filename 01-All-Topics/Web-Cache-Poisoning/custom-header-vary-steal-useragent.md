# Web-Cache-Poisoning-Custom-Header-Vary-User-Agent

We encounter the `Vary` header with the value `User-Agent` and a custom header `X-Host`.  
The Vary header indicates which request headers affect the content of the response.  
That means the User-Agent will be used as part of the cache key; if the User-Agent changes, a separate cache entry will be created.

![Screenshot1](/04-Screenshots/vary-user1.png)


In this case, our JavaScript resource will be served only to clients presenting that particular User-Agent.

Our objective is to **obtain the User-Agent of the user we are interested in.**

![Screenshot2](/04-Screenshots/vary-user2.png)


With this information, we will be able to find the user’s User-Agent in our server logs.


![Screenshot3](/04-Screenshots/vary-user3.png)


At that point, we could attempt to poison the cache for users with that User-Agent.