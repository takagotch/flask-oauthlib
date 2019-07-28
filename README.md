### flask-oauthlib
---
https://github.com/lepture/flask-oauthlib

```py
from flask import Flask
from authlib.flask.client import OAuth
from loginpass import create_flask_blueprint, GitHub

app = Flask(__name__)
oauth = OAuth(app)

def handle_authorize(remote, token, user_info):
  if token:
    save_token(remote.name, token)
  if user_info:
    save_user(user_info)
    return user_page
  raise some_error

github_bp = create_flask_blueprint(Github, oauth, handle_authorize)
app.register_blueprint(github_bp, url_prefix='/github')









```

```sh
pip install Flask-OAuthlib
easy_install Flask-OAuthlib
```

```
```


