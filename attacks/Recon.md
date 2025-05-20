# Recon

```jsx
site:*.target.com inurl:search= | inurl:s= | inurl:message= | inurl:q=
```

`grep -r -E "aws_access_key|aws_secret_key|api key|passwd|pwd|heroku|slack|firebase|swagger|aws_secret_key|aws key|password|ftp password|jdbc|db|sql|secret jet|config|admin|pwd|json|gcp|htaccess|.env|ssh key|.git|access key|secret token|oauth_token|oauth_token_secret|smtp" *.js`

- FUZZ
    
    ```jsx
    ffuf -w wordlist_location -u http://192.168.1.1/FUZZ
    Ffuf -w wordlist_location -u http://192.168.1.1/FUZZ -fc 301 --recursion --recursion-depth 2
    Ffuf -w wordlist_location -u "http://192.168.1.1/FUZZ.EXT" -w extensions_list_location :EXT
    Ffuf -w wordlist_location -u www.google.com/FUZZ -H "User-Agent: your_user_agent" -ac -acc /admin -acc/secret
    Ffuf -w wordlist_location -u 'www.target.com/?param1=FUZZ&param2=test' -fc 200
    ```
    

[Mastering Subdomain Enumeration](https://h0tak88r.medium.com/mastering-subdomain-enumeration-6c84571b07b)