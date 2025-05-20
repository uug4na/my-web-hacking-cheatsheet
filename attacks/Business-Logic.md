# Business Logic

1. **Low-level logic flaw** ( Like int overflow on products price etc )
2. **Email trick** > 

```jsx
very-long-string@victimcompany.com.mygmail.com

AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA@dontwannacry.com.exploit-0a220062042b168480b07f45019f0014.exploit-server.net
```

1. **Weak isolation** 

Removes verifying parameter
> username=administrator&current-password=lmao&new-password-1=lmao&new-password-2=lmao
> username=administrator&new-password-1=lmao&new-password-2=lmao

1. **Insufficient workflow validation**