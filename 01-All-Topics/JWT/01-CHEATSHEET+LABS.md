# JWT - CHEATSHEET + LABS

- [jwt secret wordlist](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list)
- jwt editor (burp extension)

## Key Terms

```bash
- JWT structure: Header (alg + typ) → Payload (claims/data) → Signature
- Algorithms:
    > symmetric  -> uses the same secret to sign and verify (e.g. HS256)
    > asymmetric -> uses a key pair: private key to sign, public key to verify (e.g. RS256)

- jwk → JSON Web Key (public key embedded directly in the JWT header)
- jku → JWK Set URL (pointer to a JWKS hosted on a server you control)
- kid → Key ID (identifier used to select which key in a JWKS or key store should be used to verify the signature)

```

## Walkthrough - Most Important Labs

- [JWT auth bypass weak simetric alg signing key (brute force secret)](jwt-auth-bypass-weak-signing-key.md)
- [JWT auth bypass via JWK header injection](jwt-auth-bypass-jwk-header-injection.md)
- [JWT auth bypass via JKU header injection](jwt-auth-bypass-via-jku-header-injection.md)
- [JWT auth bypass via KID path traversal to /dev/null](jwt-auth-bypass-kid-path-traversal.md)


```bash
- Modificar el valor del payload
- Cambiar el algorismo a none 
- weak signature? -> brute force
- Try inject header -> JWK or JKU
- Try path traversal in KID to /dev/null 
```

```bash
hashcat -a 0 <jwt-token> <jwt-wordlist>
```