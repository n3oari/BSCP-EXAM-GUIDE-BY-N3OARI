# HTTP/2 - CRLF injection 

In this lab, the application sanitizes the Transfer-Encoding header in some way.

![Screenshot1](../../04-Screenshots/crlf1.png)

To bypass this restriction, we inject one value inside another value using \r\n (this is known as CRLF injection):

![Screenshot2](../../04-Screenshots/crlf2.png)

Once we have verified the HTTP request smuggler by viewing the 404 code, we dump the victim's response into the search history.

![Screenshot3](../../04-Screenshots/crlf3.png)


![Screenshot4](../../04-Screenshots/crlf4.png)

## EXTRA

You can also inject an entire request through the value of a header.

![Screenshot5](../../04-Screenshots/crlf5.png)