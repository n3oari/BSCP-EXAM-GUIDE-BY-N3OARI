# DOM-based cookie manipulation (last viewed product)



We found that a cookie value is being set via the last viewed product feature, which assigns the URL as its value.

![Screenshot1](../../04-Screenshots/last-view1.png)

We escape the href anchor tag and inject our payload.

![Screenshot2](../../04-Screenshots/last-view2.png)

We create a script to exfiltrate the cookie.

![Screenshot3](../../04-Screenshots/last-view3.png)


![Screenshot4](../../04-Screenshots/last-view4.png)


> if(!window.x) is the logic used to prevent an infinite loop.