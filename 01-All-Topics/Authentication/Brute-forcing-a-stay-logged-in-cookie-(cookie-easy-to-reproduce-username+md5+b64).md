# Brute-forcing a stay-logged-in cookie (cookie easy to reproduce -> username + md5 + b64)

In this lab, we find a functionality called **stay-logged-in**, which assigns us a cookie to keep the session open.
In some cases this cookie is easy to reproduce:

![Screenshot2](/04-Screenshots/stay-logged2.png)

We perform a brute-force attack by applying the following rules in Burp Intruder to each password in the dictionary:

- Prefix → username:

- Hash → in this case, the password in MD5.

- Encode → Base64.
  
As a result, each iteration will use the expected format.

![Screenshot2](/04-Screenshots/stay-logged1.png)

<br>

> In the exam you may need to change those rules to the required ones.






