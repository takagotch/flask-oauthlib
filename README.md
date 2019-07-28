### flask-oauthlib
---
https://github.com/lepture/flask-oauthlib

https://docs.authlib.org/en/latest/index.html

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


from flask import Flask, jsonify
from authlib.flask.client import OAuth

app = Flask(__name__)
oauth = OAuth(app)
github = oauth.register('github', {...})

@app.route('/login')
def login():
  redirect_uri = url_for('authorize', _external=True)
  return github.authorize_redirect(redirect_uri)
  
@app.route('/authorize')
def authorize():
  token = github.authorize_access_token()
  profile = github.get('/user')
  return jsonify(profile)

from authlib.jose import jwt
with open('private.pem', 'rb') as f:
  key = f.read()
  
payload = {'iss': 'Authlib', 'sub': '123', ...}
header = {'alg': 'RS256'}
s = jwt.encode(header, payload, key)


def load_key(header, payload):
  kid = header['kid']
  return get_key_by_kid(kid)
  
jws.deserialize_compact(s, load_key)

header = {'protected': {'alg': 'HS256'}, 'header': {'cty': 'JWT'}}
key = b'secret'
payload = b'example'
jws.serialize_json(header, payload, key)

header = [{'protected': {'alg': 'HS256'}, 'header': {'cty': 'JWT'}}]
jws.serialize_json(header, payload, key)


def load_private_key(header, payload):
  kid = header['kid']
  return get_private_key(kid)
  
header = [
  {'protected': {'alg': 'HS256'}, 'header': {'kid': 'foo'}}
  {'protected': {'alg': 'RS256'}, 'header': {'kid': 'bar'}}
]
data = jws.serialize_json(header, payload, load_private_key)

def load_public_key(header, payload):
  kid = header['kid']
  return get_public_key(kid)
  
jws.deserialize_json(data, load_public_key)

private_headers = ['h1', 'h2']
jws = JWS(algorithms=JWS_ALGORITHMS, private_headers=private_headers)
```

```sh
pip install Flask-OAuthlib
easy_install Flask-OAuthlib
```

```
```


