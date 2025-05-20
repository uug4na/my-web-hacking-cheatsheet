# JWT

```php
hashcat -m 16500 -a 0 token.txt ~/hek/wordlists/rockyou.txt
Crack: john jwt.txt --wordlist=jwt.secrets.list --format=HMAC-SHA256

Checklist > 
	*None algorithm
	*Key bruteforce
	*JWK header injection
		Creates new RSA key
		Embed JWK in header of jwt (Fake public key makes server think its right)

	*bypass kid header by path traversal
		>generate symmetric key and changes K to "AA==" to make it empty 
		>changes kid to `"kid": "../../../../../../../dev/null"` (server tries to locate key used to sign the token then it becomes null)

	
```