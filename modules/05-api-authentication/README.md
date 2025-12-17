# API Authentication 🔐

## Introduction

You've learned how to make API requests, but what about APIs that require you to prove who you are? That's where **authentication** comes in!

Authentication is the process of verifying your identity before you can access an API's resources. It's like showing your ID at the door of a club or logging into your email.

## Why Do APIs Need Authentication?

1. **Security** 🛡️
   - Protect sensitive data
   - Prevent unauthorized access
   - Track who's doing what

2. **Rate Limiting** ⏱️
   - Control how many requests each user can make
   - Prevent abuse
   - Ensure fair usage

3. **Personalization** 👤
   - Return data specific to the user
   - Track user preferences
   - Provide customized experiences

4. **Monetization** 💰
   - Charge for API access
   - Offer different pricing tiers
   - Track usage for billing

## Types of Authentication

### 1. **No Authentication** (Public APIs)

Some APIs are completely open and require no authentication:

```python
import requests

# Anyone can access this
response = requests.get('https://api.github.com/repos/microsoft/vscode')
```

**Examples:**
- Public GitHub repositories
- Open weather data
- Public cryptocurrency prices

---

### 2. **API Keys**

The most common and simplest authentication method.

#### What is an API Key?

An API key is a unique string of characters that identifies your application or account:
```
api_key = "sk_live_abc123xyz789"
```

Think of it like a password, but for programs instead of people.

#### How to Use API Keys

**Method 1: In the URL (Query Parameter)**
```python
import requests

api_key = "your_api_key_here"
url = f"https://api.example.com/data?api_key={api_key}"
response = requests.get(url)
```

**Method 2: In Headers (More Secure)**
```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}
response = requests.get('https://api.example.com/data', headers=headers)
```

**Method 3: In Authorization Header**
```python
import requests

headers = {
    'Authorization': 'ApiKey your_api_key_here'
}
response = requests.get('https://api.example.com/data', headers=headers)
```

#### API Key Best Practices

1. **Never hardcode API keys in your code!**
   ```python
   # ❌ BAD
   api_key = "sk_live_abc123xyz"
   
   # ✅ GOOD - Use environment variables
   import os
   api_key = os.environ.get('API_KEY')
   ```

2. **Don't commit API keys to Git**
   - Use `.env` files (add to `.gitignore`)
   - Use environment variables
   - Use secret management tools

3. **Rotate keys regularly**
   - Change your API keys periodically
   - Immediately rotate if compromised

4. **Use different keys for development and production**

---

### 3. **Bearer Tokens**

Bearer tokens are similar to API keys but usually temporary.

```python
import requests

headers = {
    'Authorization': 'Bearer your_token_here'
}
response = requests.get('https://api.example.com/data', headers=headers)
```

**Characteristics:**
- Usually obtained through a login/authentication process
- Often expire after some time
- More secure than permanent API keys

---

### 4. **Basic Authentication**

Uses a username and password encoded in Base64.

```python
import requests
from requests.auth import HTTPBasicAuth

response = requests.get(
    'https://api.example.com/data',
    auth=HTTPBasicAuth('username', 'password')
)

# Or simpler:
response = requests.get(
    'https://api.example.com/data',
    auth=('username', 'password')
)
```

**How it works:**
1. Username and password are combined: `username:password`
2. Encoded to Base64: `dXNlcm5hbWU6cGFzc3dvcmQ=`
3. Sent in header: `Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=`

**Security Note:** Only use with HTTPS! Base64 is encoding, not encryption.

---

### 5. **OAuth 2.0**

The most sophisticated authentication method, commonly used by social media platforms.

#### What is OAuth?

OAuth allows apps to access your data without sharing your password. Think "Sign in with Google" or "Login with GitHub."

#### The OAuth Flow

```
1. User clicks "Login with Google"
2. Redirected to Google's login page
3. User logs in and grants permissions
4. Google redirects back with an authorization code
5. Your app exchanges the code for an access token
6. Your app uses the token to access user's data
```

#### Example: GitHub OAuth

**Step 1: Redirect user to authorization URL**
```
https://github.com/login/oauth/authorize?
  client_id=YOUR_CLIENT_ID&
  redirect_uri=YOUR_REDIRECT_URI&
  scope=repo,user
```

**Step 2: User authorizes and is redirected back**
```
https://yourapp.com/callback?code=AUTHORIZATION_CODE
```

**Step 3: Exchange code for token**
```python
import requests

response = requests.post('https://github.com/login/oauth/access_token', data={
    'client_id': 'YOUR_CLIENT_ID',
    'client_secret': 'YOUR_CLIENT_SECRET',
    'code': 'AUTHORIZATION_CODE'
}, headers={'Accept': 'application/json'})

access_token = response.json()['access_token']
```

**Step 4: Use the token**
```python
headers = {
    'Authorization': f'Bearer {access_token}'
}
response = requests.get('https://api.github.com/user', headers=headers)
```

**OAuth Benefits:**
- Users don't share passwords with your app
- Users can revoke access anytime
- Fine-grained permissions (scopes)
- More secure

---

### 6. **JWT (JSON Web Tokens)**

A compact, URL-safe way to represent claims between two parties.

#### What is a JWT?

A JWT looks like this:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

It has three parts separated by dots:
1. **Header** - Token type and algorithm
2. **Payload** - Claims (user data)
3. **Signature** - Verification signature

#### Using JWTs

```python
import requests

# Usually obtained from a login endpoint
jwt_token = "eyJhbGci..."

headers = {
    'Authorization': f'Bearer {jwt_token}'
}
response = requests.get('https://api.example.com/data', headers=headers)
```

#### JWT Benefits:
- Self-contained (includes user info)
- Stateless (server doesn't need to store session)
- Can be verified without database lookup
- Expiration built-in

---

## Common Authentication Patterns

### Pattern 1: Login and Get Token

```python
import requests

# 1. Login
login_response = requests.post('https://api.example.com/login', json={
    'email': 'user@example.com',
    'password': 'password123'
})

token = login_response.json()['token']

# 2. Use token for subsequent requests
headers = {'Authorization': f'Bearer {token}'}
data_response = requests.get('https://api.example.com/data', headers=headers)
```

### Pattern 2: Refresh Tokens

Many APIs use refresh tokens for long-lived authentication:

```python
import requests

# When access token expires
def refresh_access_token(refresh_token):
    response = requests.post('https://api.example.com/refresh', json={
        'refresh_token': refresh_token
    })
    return response.json()['access_token']

# Use in your requests
try:
    response = requests.get(url, headers={'Authorization': f'Bearer {access_token}'})
    response.raise_for_status()
except requests.exceptions.HTTPError as e:
    if response.status_code == 401:  # Unauthorized
        # Token expired, refresh it
        access_token = refresh_access_token(refresh_token)
        # Retry the request
        response = requests.get(url, headers={'Authorization': f'Bearer {access_token}'})
```

### Pattern 3: API Key in Configuration

```python
import os
import requests
from dotenv import load_dotenv

# Load environment variables from .env file
load_dotenv()

class APIClient:
    def __init__(self):
        self.api_key = os.environ.get('API_KEY')
        self.base_url = 'https://api.example.com'
        self.headers = {
            'Authorization': f'ApiKey {self.api_key}'
        }
    
    def get_data(self, endpoint):
        url = f"{self.base_url}/{endpoint}"
        response = requests.get(url, headers=self.headers)
        return response.json()

# Usage
client = APIClient()
data = client.get_data('users')
```

## Security Best Practices

### 1. **Store Secrets Securely**

**Using Environment Variables (.env file):**
```bash
# .env file
API_KEY=your_api_key_here
API_SECRET=your_secret_here
```

```python
# Python code
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.environ.get('API_KEY')
```

**Add .env to .gitignore:**
```
.env
```

### 2. **Always Use HTTPS**

```python
# ✅ GOOD
url = "https://api.example.com"

# ❌ BAD - credentials sent in plain text!
url = "http://api.example.com"
```

### 3. **Validate SSL Certificates**

```python
import requests

# Default: Verifies SSL (good!)
response = requests.get('https://api.example.com')

# Only disable in development if absolutely necessary
# response = requests.get('https://api.example.com', verify=False)
```

### 4. **Handle Token Expiration**

```python
def make_authenticated_request(url, token):
    headers = {'Authorization': f'Bearer {token}'}
    response = requests.get(url, headers=headers)
    
    if response.status_code == 401:
        # Token expired, need to refresh
        raise TokenExpiredError("Token has expired")
    
    return response.json()
```

### 5. **Implement Rate Limiting**

```python
import time
import requests

class RateLimitedClient:
    def __init__(self, requests_per_second=1):
        self.min_interval = 1.0 / requests_per_second
        self.last_request_time = 0
    
    def request(self, url, **kwargs):
        # Wait if needed to respect rate limit
        elapsed = time.time() - self.last_request_time
        if elapsed < self.min_interval:
            time.sleep(self.min_interval - elapsed)
        
        self.last_request_time = time.time()
        return requests.get(url, **kwargs)
```

## Real-World Examples

### Example 1: Weather API with API Key

```python
import requests
import os

def get_weather(city):
    api_key = os.environ.get('OPENWEATHER_API_KEY')
    url = f"https://api.openweathermap.org/data/2.5/weather"
    
    params = {
        'q': city,
        'appid': api_key,
        'units': 'metric'
    }
    
    response = requests.get(url, params=params)
    
    if response.status_code == 200:
        data = response.json()
        return {
            'temperature': data['main']['temp'],
            'description': data['weather'][0]['description'],
            'humidity': data['main']['humidity']
        }
    elif response.status_code == 401:
        print("Invalid API key")
    elif response.status_code == 404:
        print(f"City '{city}' not found")
    else:
        print(f"Error: {response.status_code}")
    
    return None

# Usage
weather = get_weather('London')
if weather:
    print(f"Temperature: {weather['temperature']}°C")
    print(f"Conditions: {weather['description']}")
```

### Example 2: GitHub API with Token

```python
import requests
import os

def get_user_repos(username):
    token = os.environ.get('GITHUB_TOKEN')
    url = f"https://api.github.com/users/{username}/repos"
    
    headers = {
        'Authorization': f'token {token}',
        'Accept': 'application/vnd.github.v3+json'
    }
    
    response = requests.get(url, headers=headers)
    
    if response.status_code == 200:
        repos = response.json()
        for repo in repos[:5]:  # First 5 repos
            print(f"- {repo['name']}: {repo['stargazers_count']} stars")
    else:
        print(f"Error: {response.status_code}")
        print(response.json().get('message', 'Unknown error'))

# Usage
get_user_repos('octocat')
```

## Common Authentication Errors

### 1. **401 Unauthorized**
```
Problem: Invalid or missing credentials
Solutions:
- Check API key is correct
- Verify token hasn't expired
- Ensure proper header format
```

### 2. **403 Forbidden**
```
Problem: Valid credentials but insufficient permissions
Solutions:
- Check API key has necessary permissions
- Verify account subscription level
- Check if rate limit exceeded
```

### 3. **429 Too Many Requests**
```
Problem: Exceeded rate limit
Solutions:
- Implement rate limiting in your code
- Wait before retrying
- Upgrade to higher tier if available
```

## What's Next?

Now you understand API authentication! The final module covers:
- Working with JSON data in depth
- Parsing complex JSON structures
- Creating JSON payloads

Ready to practice? Try the exercises below!

---

## 📝 Practice Problems

### Problem 1: API Key Authentication (Easy)
**File**: `problem1.md` and `problem1.py` or `problem1.js`

Practice using API keys with a free weather API.

**Tasks:**
1. Sign up for a free OpenWeatherMap API key at: https://openweathermap.org/api
2. Store the API key in an environment variable
3. Create a function that fetches weather data for a city
4. Display temperature, conditions, and humidity
5. Handle errors (invalid API key, city not found)

**Test cities:** London, New York, Tokyo, InvalidCity

### Problem 2: GitHub Authentication (Medium)
**File**: `problem2.md` and `problem2.py` or `problem2.js`

Build a tool that uses GitHub's API with token authentication.

**Requirements:**
1. Create a GitHub personal access token
2. Store it securely in environment variables
3. Create functions to:
   - Get authenticated user's info
   - List user's repositories
   - Create a new repository (test with caution!)
   - Star/unstar a repository
4. Compare rate limits with and without authentication

**Bonus:** Implement token refresh/validation

### Problem 3: Multi-API Integration (Hard)
**File**: `problem3.md` and `problem3.py` or `problem3.js`

Build a dashboard that integrates multiple APIs with different authentication methods.

**Requirements:**

1. **Integrate at least 3 APIs** with different auth methods:
   - API Key authentication (e.g., Weather API)
   - Bearer Token (e.g., GitHub API)
   - OAuth 2.0 (e.g., Google, Spotify, or Twitter)

2. **Features:**
   - Securely manage multiple credentials
   - Handle different authentication flows
   - Gracefully handle authentication failures
   - Display combined data from all APIs

3. **Error Handling:**
   - Expired tokens
   - Invalid credentials
   - Rate limiting across multiple APIs
   - Network errors

4. **Advanced Features (choose at least 2):**
   - Automatic token refresh
   - Credential rotation
   - Rate limit tracking per API
   - Caching authenticated sessions
   - Retry logic with exponential backoff

**Example Dashboard Ideas:**
- Developer profile (GitHub repos + Stack Overflow stats + Twitter followers)
- Personal dashboard (Weather + Calendar + Todo list)
- Content aggregator (News + Reddit + Twitter)

---

## 🎯 Solutions

### Problem 1 Solution (Python)

```python
import requests
import os
from dotenv import load_dotenv

load_dotenv()

def get_weather(city):
    """Fetch weather data for a city using OpenWeatherMap API"""
    api_key = os.environ.get('OPENWEATHER_API_KEY')
    
    if not api_key:
        print("Error: OPENWEATHER_API_KEY not found in environment variables")
        return None
    
    url = "https://api.openweathermap.org/data/2.5/weather"
    
    params = {
        'q': city,
        'appid': api_key,
        'units': 'metric'  # Use Celsius
    }
    
    try:
        response = requests.get(url, params=params, timeout=5)
        
        if response.status_code == 200:
            data = response.json()
            
            weather_info = {
                'city': data['name'],
                'temperature': data['main']['temp'],
                'feels_like': data['main']['feels_like'],
                'description': data['weather'][0]['description'],
                'humidity': data['main']['humidity'],
                'wind_speed': data['wind']['speed']
            }
            
            return weather_info
            
        elif response.status_code == 401:
            print(f"Error: Invalid API key")
            return None
            
        elif response.status_code == 404:
            print(f"Error: City '{city}' not found")
            return None
            
        else:
            print(f"Error: {response.status_code}")
            print(response.text)
            return None
            
    except requests.exceptions.Timeout:
        print("Error: Request timed out")
        return None
        
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")
        return None

def display_weather(weather_info):
    """Display weather information in a nice format"""
    if weather_info:
        print(f"\n{'='*50}")
        print(f"Weather in {weather_info['city']}")
        print(f"{'='*50}")
        print(f"Temperature: {weather_info['temperature']}°C")
        print(f"Feels like: {weather_info['feels_like']}°C")
        print(f"Conditions: {weather_info['description'].capitalize()}")
        print(f"Humidity: {weather_info['humidity']}%")
        print(f"Wind Speed: {weather_info['wind_speed']} m/s")
        print()

def main():
    """Main function"""
    test_cities = ['London', 'New York', 'Tokyo', 'InvalidCity']
    
    for city in test_cities:
        weather = get_weather(city)
        display_weather(weather)

if __name__ == "__main__":
    main()
```

**Create .env file:**
```
OPENWEATHER_API_KEY=your_api_key_here
```

### Problem 2 Solution Outline

```python
import requests
import os
from dotenv import load_dotenv

load_dotenv()

class GitHubClient:
    def __init__(self):
        self.token = os.environ.get('GITHUB_TOKEN')
        self.base_url = 'https://api.github.com'
        self.headers = {
            'Authorization': f'token {self.token}',
            'Accept': 'application/vnd.github.v3+json'
        }
    
    def get_authenticated_user(self):
        """Get info about the authenticated user"""
        response = requests.get(f'{self.base_url}/user', headers=self.headers)
        if response.status_code == 200:
            return response.json()
        else:
            print(f"Error: {response.status_code}")
            return None
    
    def list_repos(self):
        """List user's repositories"""
        response = requests.get(f'{self.base_url}/user/repos', headers=self.headers)
        if response.status_code == 200:
            return response.json()
        return []
    
    def check_rate_limit(self):
        """Check current rate limit status"""
        response = requests.get(f'{self.base_url}/rate_limit', headers=self.headers)
        if response.status_code == 200:
            data = response.json()
            return {
                'limit': data['rate']['limit'],
                'remaining': data['rate']['remaining'],
                'reset': data['rate']['reset']
            }
        return None
    
    def compare_auth_rates(self):
        """Compare rate limits with and without authentication"""
        # With auth
        with_auth = self.check_rate_limit()
        
        # Without auth
        response = requests.get(f'{self.base_url}/rate_limit')
        without_auth = response.json()['rate']
        
        print(f"With Authentication: {with_auth['limit']} requests/hour")
        print(f"Without Authentication: {without_auth['limit']} requests/hour")

# Usage
client = GitHubClient()
user = client.get_authenticated_user()
if user:
    print(f"Authenticated as: {user['login']}")
```

---

**Excellent work completing the authentication module! 🎉**

Next up: **[06-working-with-json](../06-working-with-json/)** - Master JSON data manipulation!
