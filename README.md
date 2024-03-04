
---

## Python OAuth2 Token Retrieval Example

This Python script demonstrates how to obtain an OAuth2 access token from an authorization server using the authorization code flow. It's a basic example that uses the `requests` library to make an HTTP POST request to the token endpoint of the authorization server.

### Prerequisites:
- Python 3.x
- `requests` library (Install using `pip install requests`)
- Registered OAuth client with `client_id` and `client_secret`
- Authorization code obtained after user authorization

### Code:

```python
import os
import requests

# OAuth client credentials from environment variables
client_id = os.getenv('OAUTH_CLIENT_ID')
client_secret = os.getenv('OAUTH_CLIENT_SECRET')

# Your application's callback URL
redirect_uri = 'https://yourwebsite.com/callback'

# Authorization code received from the authorization server
authorization_code = 'ReceivedAuthorizationCode'

# Token endpoint URL of the authorization server
token_url = 'https://authorization-server.com/oauth/token'

# Data payload for the token request
data = {
    'grant_type': 'authorization_code',
    'client_id': client_id,
    'client_secret': client_secret,
    'redirect_uri': redirect_uri,
    'code': authorization_code,
}

# HTTP headers for the request
headers = {'Content-Type': 'application/x-www-form-urlencoded'}

# Creating a session to manage the request
with requests.Session() as session:
    response = session.post(token_url, data=data, headers=headers)

    # Checking the response status code
    if response.status_code == 200:
        # Parsing the access token from the response
        token_data = response.json()
        access_token = token_data.get('access_token')
        print(f"Access Token: {access_token}")
    else:
        # Handling errors
        print(f"Error obtaining access token: {response.text}")
```




---

