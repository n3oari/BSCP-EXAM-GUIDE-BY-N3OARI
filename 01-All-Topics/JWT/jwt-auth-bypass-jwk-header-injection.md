# JWT authentication bypass via jwk header injection

By abusing the jwk parameter in the token header, a vulnerable server may accept a JWT that embeds the public key used to verify its signature — without checking whether that key comes from a trusted source.

- 1: Generate our RSA key pair (private + public).

![Screenshot1](../../04-Screenshots/jwk1.png)

- 2: Inject our public key into the JWT header using jwk.

![Screenshot2](../../04-Screenshots/jwk2.png)

- 3: Sign the JWT with our private key and send it to the server.

![Screenshot3](../../04-Screenshots/jwk3.png)

If the server is vulnerable and uses the jwk supplied by the client to verify the signature, verification will succeed and the token will be accepted.