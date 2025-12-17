# Problem 3: Multi-API Integration (Hard)

## Instructions

Build a dashboard that integrates multiple APIs with different authentication methods.

This is a comprehensive project that demonstrates real-world API integration skills.

---

## Requirements

### 1. Integrate at least 3 APIs

Choose APIs with **different authentication methods**:

**API Key Authentication:**
- OpenWeatherMap (weather data)
- NewsAPI (news articles)
- CoinGecko (cryptocurrency prices)
- ExchangeRate-API (currency conversion)

**Token/Bearer Authentication:**
- GitHub API
- Spotify API (with OAuth)
- Twitter API

**OAuth 2.0:**
- Google APIs (Calendar, Gmail, etc.)
- Spotify API
- Discord API

---

### 2. Core Features

Your dashboard should:
1. **Securely manage multiple credentials**
2. **Handle different authentication flows**
3. **Display combined data from all APIs**
4. **Gracefully handle errors**
5. **Be user-friendly**

---

## Example Dashboard Ideas

### Option 1: Developer Profile Dashboard
```
- GitHub: Repositories and activity
- Stack Overflow: Reputation and answers
- Twitter: Developer tweets and followers
```

### Option 2: Personal Dashboard
```
- Weather: Current weather for your location
- Calendar: Today's events (Google Calendar)
- Tasks: Todo list (Todoist or similar)
```

### Option 3: Content Aggregator
```
- News: Top headlines (NewsAPI)
- Reddit: Popular posts from favorite subreddits
- Weather: Current conditions
```

---

## Your Code Structure

### Python Template

```python
import requests
import os
from dotenv import load_dotenv
from datetime import datetime
import json

load_dotenv()

class APICredentialManager:
    """Manage API credentials securely"""
    
    def __init__(self):
        self.credentials = {
            'weather_api_key': os.environ.get('OPENWEATHER_API_KEY'),
            'github_token': os.environ.get('GITHUB_TOKEN'),
            'news_api_key': os.environ.get('NEWS_API_KEY'),
            # Add more as needed
        }
    
    def get_credential(self, api_name):
        """Get credential for a specific API"""
        return self.credentials.get(api_name)
    
    def validate_credentials(self):
        """Check that all required credentials are present"""
        missing = [key for key, value in self.credentials.items() if not value]
        if missing:
            print(f"Warning: Missing credentials for: {', '.join(missing)}")
        return len(missing) == 0

class WeatherService:
    """Service for weather data with API key auth"""
    
    def __init__(self, api_key):
        self.api_key = api_key
        self.base_url = 'https://api.openweathermap.org/data/2.5'
    
    def get_current_weather(self, city):
        """Fetch current weather"""
        # TODO: Implement
        pass
    
    def handle_error(self, response):
        """Handle API errors"""
        # TODO: Implement error handling
        pass

class GitHubService:
    """Service for GitHub data with token auth"""
    
    def __init__(self, token):
        self.token = token
        self.base_url = 'https://api.github.com'
        self.headers = {
            'Authorization': f'token {token}',
            'Accept': 'application/vnd.github.v3+json'
        }
    
    def get_user_activity(self):
        """Get user's recent activity"""
        # TODO: Implement
        pass
    
    def check_rate_limit(self):
        """Check remaining API calls"""
        # TODO: Implement
        pass

class NewsService:
    """Service for news data with API key auth"""
    
    def __init__(self, api_key):
        self.api_key = api_key
        self.base_url = 'https://newsapi.org/v2'
    
    def get_top_headlines(self, category='technology'):
        """Fetch top headlines"""
        # TODO: Implement
        pass

class Dashboard:
    """Main dashboard that combines all services"""
    
    def __init__(self):
        self.credential_manager = APICredentialManager()
        
        # Initialize services
        self.weather = WeatherService(
            self.credential_manager.get_credential('weather_api_key')
        )
        self.github = GitHubService(
            self.credential_manager.get_credential('github_token')
        )
        self.news = NewsService(
            self.credential_manager.get_credential('news_api_key')
        )
    
    def display_header(self):
        """Display dashboard header"""
        print("\n" + "="*60)
        print("  Personal Dashboard")
        print(f"  {datetime.now().strftime('%B %d, %Y - %I:%M %p')}")
        print("="*60 + "\n")
    
    def display_weather(self, city='London'):
        """Display weather section"""
        print("☀️  WEATHER")
        print("-" * 60)
        # TODO: Fetch and display weather
        pass
    
    def display_github_activity(self):
        """Display GitHub section"""
        print("\n💻 GITHUB ACTIVITY")
        print("-" * 60)
        # TODO: Fetch and display GitHub data
        pass
    
    def display_news(self):
        """Display news section"""
        print("\n📰 TOP NEWS")
        print("-" * 60)
        # TODO: Fetch and display news
        pass
    
    def run(self):
        """Run the dashboard"""
        if not self.credential_manager.validate_credentials():
            print("Error: Some API credentials are missing!")
            return
        
        self.display_header()
        
        try:
            self.display_weather()
            self.display_github_activity()
            self.display_news()
        except Exception as e:
            print(f"Error running dashboard: {e}")
        
        print("\n" + "="*60 + "\n")

def main():
    """Main function"""
    dashboard = Dashboard()
    dashboard.run()

if __name__ == "__main__":
    main()
```

---

## Expected Output

```
============================================================
  Personal Dashboard
  December 16, 2024 - 02:30 PM
============================================================

☀️  WEATHER
------------------------------------------------------------
Location: London, UK
Temperature: 12°C (Feels like 10°C)
Conditions: Partly cloudy
Humidity: 72%

💻 GITHUB ACTIVITY
------------------------------------------------------------
Username: johndoe
Public Repos: 42
Recent Activity:
  • Pushed to awesome-project (2 hours ago)
  • Starred microsoft/vscode (5 hours ago)
  • Created new repo: learning-apis (1 day ago)

API Rate Limit: 4998/5000 remaining

📰 TOP NEWS (Technology)
------------------------------------------------------------
1. New AI Model Breakthrough Announced
   Source: TechCrunch | 3 hours ago

2. Major Security Update Released for Popular Framework
   Source: The Verge | 5 hours ago

3. Tech Company Announces Revolutionary Product
   Source: Wired | 8 hours ago

============================================================
```

---

## Advanced Requirements

### 1. Error Handling

Implement comprehensive error handling:

```python
class APIError(Exception):
    """Base exception for API errors"""
    pass

class AuthenticationError(APIError):
    """Authentication failed"""
    pass

class RateLimitError(APIError):
    """Rate limit exceeded"""
    pass

class NetworkError(APIError):
    """Network/connection error"""
    pass

def handle_api_error(response):
    """Handle different API error scenarios"""
    # TODO: Implement
    pass
```

**Your Code:**
```python
# Your error handling implementation










```

---

### 2. Rate Limit Management

Track rate limits across all APIs:

```python
class RateLimitTracker:
    """Track rate limits for multiple APIs"""
    
    def __init__(self):
        self.limits = {}
    
    def update_limit(self, api_name, remaining, limit, reset_time):
        """Update rate limit for an API"""
        # TODO: Implement
        pass
    
    def check_limit(self, api_name):
        """Check if API has remaining requests"""
        # TODO: Implement
        pass
    
    def display_limits(self):
        """Display all rate limits"""
        # TODO: Implement
        pass
```

**Your Code:**
```python
# Your rate limit tracking implementation










```

---

### 3. Caching

Implement caching to reduce API calls:

```python
import time
import pickle

class APICache:
    """Simple cache for API responses"""
    
    def __init__(self, ttl=300):  # 5 minutes default
        self.cache = {}
        self.ttl = ttl
    
    def get(self, key):
        """Get cached value if not expired"""
        # TODO: Implement
        pass
    
    def set(self, key, value):
        """Cache a value with timestamp"""
        # TODO: Implement
        pass
    
    def clear_expired(self):
        """Remove expired cache entries"""
        # TODO: Implement
        pass
```

**Your Code:**
```python
# Your caching implementation










```

---

### 4. Token Refresh

Implement automatic token refresh for OAuth:

```python
class OAuthTokenManager:
    """Manage OAuth tokens with automatic refresh"""
    
    def __init__(self, client_id, client_secret):
        self.client_id = client_id
        self.client_secret = client_secret
        self.access_token = None
        self.refresh_token = None
        self.expires_at = None
    
    def is_token_expired(self):
        """Check if access token is expired"""
        # TODO: Implement
        pass
    
    def refresh_access_token(self):
        """Refresh the access token"""
        # TODO: Implement
        pass
    
    def get_valid_token(self):
        """Get a valid access token, refreshing if needed"""
        if self.is_token_expired():
            self.refresh_access_token()
        return self.access_token
```

**Your Code:**
```python
# Your token refresh implementation










```

---

### 5. Retry Logic

Implement retry with exponential backoff:

```python
import time
from functools import wraps

def retry_with_backoff(max_retries=3, initial_delay=1):
    """Decorator for retrying failed requests"""
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            delay = initial_delay
            for attempt in range(max_retries):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_retries - 1:
                        raise
                    print(f"Attempt {attempt + 1} failed: {e}")
                    print(f"Retrying in {delay} seconds...")
                    time.sleep(delay)
                    delay *= 2  # Exponential backoff
        return wrapper
    return decorator

# Usage
@retry_with_backoff(max_retries=3)
def make_api_request(url):
    # Your API request code
    pass
```

**Your Code:**
```python
# Your retry logic implementation










```

---

## Enhanced Features (Choose at least 2)

### Feature 1: Configuration File
```
Allow users to customize dashboard via config file
- Which APIs to use
- What data to display
- Refresh intervals
```

**Your Code:**
```python
# Your configuration implementation










```

---

### Feature 2: Data Export
```
Export dashboard data to JSON or CSV
Include timestamp and all fetched data
```

**Your Code:**
```python
# Your export implementation










```

---

### Feature 3: Scheduled Updates
```
Refresh dashboard data automatically at intervals
Display "Last updated" timestamps
```

**Your Code:**
```python
# Your scheduled updates implementation










```

---

### Feature 4: Web Dashboard
```
Create a simple web interface using Flask
Display data in a browser
Auto-refresh
```

**Your Code:**
```python
# Your web dashboard implementation










```

---

## Testing Checklist

- [ ] All API credentials loaded from environment
- [ ] Successfully authenticates with all APIs
- [ ] Handles different auth methods correctly
- [ ] Displays combined data from all sources
- [ ] Gracefully handles authentication errors
- [ ] Handles rate limiting
- [ ] Handles network errors
- [ ] Implements caching (if applicable)
- [ ] Code is well-organized and modular
- [ ] Comprehensive error messages
- [ ] No credentials in code or git
- [ ] Documentation/comments included

---

## Reflection Questions

1. **What were the biggest challenges in integrating multiple APIs?**
```




```

2. **How did you organize the code to keep it maintainable?**
```




```

3. **What strategies did you use to handle different authentication methods?**
```




```

4. **How would you scale this dashboard to include 10+ APIs?**
```




```

5. **What security considerations did you implement?**
```




```

---

## Bonus Challenge

### OAuth 2.0 Implementation

Implement a full OAuth 2.0 flow for one API (e.g., Spotify or Google):

1. Authorization URL generation
2. Callback handling
3. Token exchange
4. Token refresh
5. Token storage

**This is advanced - research OAuth flows first!**

---

**Congratulations on building a multi-API dashboard! 🎉**

**This is portfolio-worthy work!**

**Check the main README for solution approaches!**
