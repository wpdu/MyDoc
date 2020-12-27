# Flask AppContext, Request RequestContext
```python
from flask import Flask, current_app, request, Request
ctx = app.app_context()
ctx.push()
current_app.config['DEBUG']
ctx.pop()
```