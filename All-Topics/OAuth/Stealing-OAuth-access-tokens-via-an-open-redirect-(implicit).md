# Stealing OAuth access tokens via an open redirect (implicit)

In this lab we encountered the `redirect_uri` parameter, which is vulnerable to **path traversal**.

![Screenshot1](/Screenshots/1-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png)

Once this was confirmed, our goal was to find an **open redirect**.

![Screenshots2](/Screenshots/2-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png)

![Screenshots3](/Screenshots/3-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png)

After testing that we could achieve an arbitrary open redirect, we created our script to obtain the `access_token`.

![Screenshot4](/Screenshots/4-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png)

![Screenshot5](/Screenshots/5-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png)

![Screenshot](/Screenshots/6-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png)

