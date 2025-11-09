# JWT authentication bypass via weak signing key

With hashcat we brute-force the secret using the following dictionary. [jwt-secret.txt](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list)

```bash
hashcat -a 0 <jwt-token> <jwt-wordlist>
```

![Screenshot1](../../04-Screenshots/weak1.png.png)


![Screenshot2](../../04-Screenshots/weak1.png.png)


![Screenshot3](../../04-Screenshots/weak1.png.png)