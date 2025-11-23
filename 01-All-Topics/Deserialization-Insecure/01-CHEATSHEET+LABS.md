
# Deserialization Insecure  - CHEATSHEET + LABS

## Key Terms

```
- Serialization    -> Process of converting an object into a byte/string format for storage or transmission.
- Deserialization  -> Reconstructing an object from serialized data. Dangerous if the data is user-controlled.

- ysoserial        -> Tool that generates malicious Java deserialization payloads using known gadget chains. (use java 8)
- phpggc           -> Tool that generates malicious PHP serialized objects using gadget chains from popular frameworks.


```

## Walkthrough - Most Important Labs


- [java ysoserial !! PENDIENTE !!]() 
- [PHP deserialization in cookie with a pre-build gadget chain using phpgcc](php-des.md)
- [Ruby deserialization in cookie using a documented gadget chain (ruby rce exploit)](php-des.md)


## Methodology

```bash
- b:0?  -> change to -> b:1 
- access token? -> s:32<token> -> change to ->  b:1
- backup file -> <file>~  , e.g ->  /libs/CustomTemplate.php~
```




