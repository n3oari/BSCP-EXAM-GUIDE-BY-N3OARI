\# Stealing OAuth access tokens via an open redirect (implicit)



In this lab we encountered the `redirect\_uri` parameter, which is vulnerable to \*\*path traversal\*\*.



!\[\[1-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png]]



Once this was confirmed, our goal was to find an \*\*open redirect\*\*.



!\[\[2-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png]]



!\[\[3-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png]]



After testing that we could achieve an arbitrary open redirect, we created our script to obtain the `access\_token`.



!\[\[4-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png]]



!\[\[5-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png]]



!\[\[6-Stealing-OAuth-access-tokens-via-an-open-redirect-(implicit).png]]

