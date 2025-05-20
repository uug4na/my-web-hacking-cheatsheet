# Web Cache Attacks

- Example Blogs, POCS
    
    [Cache Deception Allows Cache Poisoning](https://bxmbn.medium.com/chaining-cache-deception-poisoning-250ec69774c8)
    
    [How I Test For Web Cache Vulnerabilities + Tips And Tricks](https://bxmbn.medium.com/how-i-test-for-web-cache-vulnerabilities-tips-and-tricks-9b138da08ff9)
    
    [DOS via cache poisoning](https://infosecwriteups.com/dos-via-cache-poisoning-38f3a87f997c)
    
- Ideas
    
    ```jsx
    When finds caching page or endpoint.
    Tries 
    X-Forwarded-Host,
    Cookie XSS
    Origin header as cache buster
    ```
    

```jsx
/my-account/a.js
/my-account;a.js
/css/labs.css%2f..%2f..%2f..%2fmy-account?5.css
/my-account%23%2f%2e%2e%2fresources?abc
```