# SQL injection with filter WAF bypass via XML encoding with Hackvertor extension

In this lab we identified an SQL injection occurring within XXE entities

![Screenshot1](../../04-Screenshots/hackvertor1.png)

We discovered that certain keywords were blacklisted by the WAF

![Screenshot2](../../04-Screenshots/hackvertor2.png)

Using the BurpSuite extension HackVertor, we managed to bypass this restriction

![Screenshot3](../../04-Screenshots/hackvertor3.png)

We confirmed that the WAF bypass was successful

![Screenshot4](../../04-Screenshots/hackvertor4.png)

Finally, we were able to retrieve the required data

![Screenshot5](../../04-Screenshots/hackvertor5.png)