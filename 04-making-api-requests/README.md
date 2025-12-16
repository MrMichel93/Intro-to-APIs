# Making API Requests 💻

## Introduction

You've learned what APIs are, how HTTP works, and REST principles. Now it's time to actually **make API requests using code**! 

This module will show you how to call APIs using popular programming languages. Even if you don't know all these languages, the concepts are similar across all of them.

## Tools for Testing APIs

Before writing code, it's helpful to test APIs using these tools:

### 1. **Browser** (Simplest)
For simple GET requests, just paste the URL in your browser:
```
https://api.github.com/users/octocat
```

### 2. **curl** (Command Line)
A command-line tool for making HTTP requests:
```bash
curl https://api.github.com/users/octocat
```

### 3. **Postman** (Visual Interface)
A popular GUI application for testing APIs. Great for beginners!
- Download from: https://www.postman.com

### 4. **HTTPie** (Friendly CLI)
Like curl but more user-friendly:
```bash
http GET https://api.github.com/users/octocat
```

## Using curl (Command Line)

curl is pre-installed on most systems. Here's how to use it:

### Basic GET Request
```bash
curl https://api.github.com/users/octocat
```

### GET with Headers
```bash
curl -H "Authorization: Bearer token123" \
     -H "Accept: application/json" \
     https://api.example.com/data
```

### POST Request with Data
```bash
curl -X POST https://api.example.com/users \
     -H "Content-Type: application/json" \
     -d '{"name":"John","email":"john@example.com"}'
```

### PUT Request
```bash
curl -X PUT https://api.example.com/users/123 \
     -H "Content-Type: application/json" \
     -d '{"name":"John Updated"}'
```

### DELETE Request
```bash
curl -X DELETE https://api.example.com/users/123 \
     -H "Authorization: Bearer token123"
```

### See Response Headers
```bash
curl -i https://api.github.com/users/octocat
```

### Save Response to File
```bash
curl https://api.github.com/users/octocat > response.json
```

## Making API Requests in Python

Python is great for API interactions! The `requests` library makes it easy.

### Installing requests
```bash
pip install requests
```

### GET Request
```python
import requests

# Basic GET request
response = requests.get('https://api.github.com/users/octocat')

# Check if successful
if response.status_code == 200:
    data = response.json()  # Parse JSON response
    print(f"Name: {data['name']}")
    print(f"Public repos: {data['public_repos']}")
else:
    print(f"Error: {response.status_code}")
```

### GET with Query Parameters
```python
import requests

# Method 1: In the URL
response = requests.get('https://api.github.com/search/repositories?q=python&sort=stars')

# Method 2: As a dictionary (better)
params = {
    'q': 'python',
    'sort': 'stars',
    'order': 'desc'
}
response = requests.get('https://api.github.com/search/repositories', params=params)

data = response.json()
print(f"Found {data['total_count']} repositories")
```

### GET with Headers
```python
import requests

headers = {
    'Authorization': 'Bearer your-token-here',
    'Accept': 'application/json'
}

response = requests.get('https://api.example.com/data', headers=headers)
```

### POST Request
```python
import requests

url = 'https://api.example.com/users'
headers = {'Content-Type': 'application/json'}
data = {
    'name': 'John Doe',
    'email': 'john@example.com',
    'age': 18
}

response = requests.post(url, json=data, headers=headers)

if response.status_code == 201:
    print("User created successfully!")
    print(response.json())
else:
    print(f"Error: {response.status_code}")
    print(response.text)
```

### PUT and PATCH Requests
```python
import requests

# PUT - Full update
url = 'https://api.example.com/users/123'
data = {
    'name': 'John Updated',
    'email': 'john.new@example.com',
    'age': 19
}
response = requests.put(url, json=data)

# PATCH - Partial update
data = {'email': 'john.new@example.com'}
response = requests.patch(url, json=data)
```

### DELETE Request
```python
import requests

url = 'https://api.example.com/users/123'
headers = {'Authorization': 'Bearer token123'}

response = requests.delete(url, headers=headers)

if response.status_code == 204:
    print("User deleted successfully!")
```

### Error Handling
```python
import requests

try:
    response = requests.get('https://api.example.com/data', timeout=5)
    response.raise_for_status()  # Raises exception for 4xx/5xx status codes
    data = response.json()
    print(data)
except requests.exceptions.Timeout:
    print("Request timed out")
except requests.exceptions.HTTPError as e:
    print(f"HTTP error occurred: {e}")
except requests.exceptions.RequestException as e:
    print(f"Error occurred: {e}")
```

## Making API Requests in JavaScript

JavaScript can make API requests in both browsers and Node.js.

### Using fetch (Modern Browsers and Node.js 18+)

### GET Request
```javascript
// Basic GET request
fetch('https://api.github.com/users/octocat')
  .then(response => response.json())
  .then(data => {
    console.log(`Name: ${data.name}`);
    console.log(`Public repos: ${data.public_repos}`);
  })
  .catch(error => console.error('Error:', error));

// Using async/await (cleaner)
async function getUser() {
  try {
    const response = await fetch('https://api.github.com/users/octocat');
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}

getUser();
```

### GET with Query Parameters
```javascript
// Build URL with parameters
const params = new URLSearchParams({
  q: 'python',
  sort: 'stars',
  order: 'desc'
});

fetch(`https://api.github.com/search/repositories?${params}`)
  .then(response => response.json())
  .then(data => console.log(`Found ${data.total_count} repositories`))
  .catch(error => console.error('Error:', error));
```

### POST Request
```javascript
async function createUser() {
  const url = 'https://api.example.com/users';
  const userData = {
    name: 'John Doe',
    email: 'john@example.com',
    age: 18
  };

  try {
    const response = await fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer token123'
      },
      body: JSON.stringify(userData)
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    console.log('User created:', data);
  } catch (error) {
    console.error('Error:', error);
  }
}

createUser();
```

### PUT, PATCH, and DELETE
```javascript
// PUT Request
async function updateUser(userId, userData) {
  const response = await fetch(`https://api.example.com/users/${userId}`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(userData)
  });
  return response.json();
}

// PATCH Request
async function patchUser(userId, updates) {
  const response = await fetch(`https://api.example.com/users/${userId}`, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(updates)
  });
  return response.json();
}

// DELETE Request
async function deleteUser(userId) {
  const response = await fetch(`https://api.example.com/users/${userId}`, {
    method: 'DELETE',
    headers: { 'Authorization': 'Bearer token123' }
  });
  return response.status === 204;
}
```

### Using axios (Popular Library)

First, install axios:
```bash
npm install axios
```

```javascript
const axios = require('axios');

// GET Request
axios.get('https://api.github.com/users/octocat')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error.message);
  });

// POST Request
axios.post('https://api.example.com/users', {
  name: 'John Doe',
  email: 'john@example.com'
}, {
  headers: {
    'Authorization': 'Bearer token123'
  }
})
.then(response => console.log(response.data))
.catch(error => console.error(error));

// With async/await
async function fetchData() {
  try {
    const response = await axios.get('https://api.github.com/users/octocat');
    console.log(response.data);
  } catch (error) {
    console.error('Error:', error.message);
  }
}
```

## Common Patterns

### 1. Checking Status Codes
```python
# Python
if response.status_code == 200:
    # Success
elif response.status_code == 404:
    # Not found
elif response.status_code >= 500:
    # Server error
```

```javascript
// JavaScript
if (response.status === 200) {
  // Success
} else if (response.status === 404) {
  // Not found
} else if (response.status >= 500) {
  // Server error
}
```

### 2. Parsing JSON
```python
# Python
data = response.json()
```

```javascript
// JavaScript
const data = await response.json();
```

### 3. Setting Timeouts
```python
# Python
response = requests.get(url, timeout=5)  # 5 seconds
```

```javascript
// JavaScript with AbortController
const controller = new AbortController();
const timeoutId = setTimeout(() => controller.abort(), 5000);

try {
  const response = await fetch(url, { signal: controller.signal });
} finally {
  clearTimeout(timeoutId);
}
```

### 4. Retrying Failed Requests
```python
# Python with retries
import time

def fetch_with_retry(url, max_retries=3):
    for attempt in range(max_retries):
        try:
            response = requests.get(url, timeout=5)
            response.raise_for_status()
            return response.json()
        except requests.exceptions.RequestException as e:
            if attempt == max_retries - 1:
                raise
            time.sleep(2 ** attempt)  # Exponential backoff
```

## Best Practices

### 1. **Always Handle Errors**
Don't assume requests will succeed!

```python
try:
    response = requests.get(url)
    response.raise_for_status()
    data = response.json()
except Exception as e:
    print(f"Error: {e}")
```

### 2. **Use Timeouts**
Prevent hanging requests:
```python
response = requests.get(url, timeout=10)
```

### 3. **Check Status Codes**
```python
if response.status_code == 200:
    # Success
else:
    print(f"Error: {response.status_code}")
```

### 4. **Store API Keys Securely**
Never hardcode API keys in your code!

```python
# Bad
api_key = "sk_live_abc123xyz"

# Good - use environment variables
import os
api_key = os.environ.get('API_KEY')
```

### 5. **Respect Rate Limits**
Many APIs limit how many requests you can make:
```python
import time

for item in items:
    response = requests.get(f"{url}/{item}")
    time.sleep(1)  # Wait 1 second between requests
```

### 6. **Log Requests for Debugging**
```python
import logging

logging.basicConfig(level=logging.DEBUG)

response = requests.get(url)
logging.info(f"Status: {response.status_code}")
logging.debug(f"Response: {response.text}")
```

## Free Public APIs for Practice

Here are some free APIs you can use to practice (no authentication required):

### 1. **JSONPlaceholder** (Fake API for testing)
```
https://jsonplaceholder.typicode.com/posts
https://jsonplaceholder.typicode.com/users
https://jsonplaceholder.typicode.com/comments
```

### 2. **GitHub API** (Public data)
```
https://api.github.com/users/octocat
https://api.github.com/repos/microsoft/vscode
```

### 3. **PokeAPI** (Pokemon data)
```
https://pokeapi.co/api/v2/pokemon/pikachu
https://pokeapi.co/api/v2/pokemon?limit=20
```

### 4. **Open Weather Map** (Weather data - requires free API key)
```
https://openweathermap.org/api
```

### 5. **REST Countries** (Country information)
```
https://restcountries.com/v3.1/all
https://restcountries.com/v3.1/name/canada
```

## Example: Complete Python Script

```python
import requests
import json

def fetch_github_user(username):
    """Fetch GitHub user information"""
    url = f"https://api.github.com/users/{username}"
    
    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()
        
        user = response.json()
        
        print(f"\n{'=' * 50}")
        print(f"GitHub User: {user['login']}")
        print(f"{'=' * 50}")
        print(f"Name: {user.get('name', 'N/A')}")
        print(f"Bio: {user.get('bio', 'N/A')}")
        print(f"Public Repos: {user['public_repos']}")
        print(f"Followers: {user['followers']}")
        print(f"Following: {user['following']}")
        print(f"Profile: {user['html_url']}")
        
    except requests.exceptions.HTTPError as e:
        if response.status_code == 404:
            print(f"User '{username}' not found")
        else:
            print(f"HTTP error occurred: {e}")
    except requests.exceptions.Timeout:
        print("Request timed out")
    except requests.exceptions.RequestException as e:
        print(f"Error occurred: {e}")

# Test the function
if __name__ == "__main__":
    fetch_github_user("octocat")
    fetch_github_user("torvalds")
```

## Example: Complete JavaScript Script

```javascript
async function fetchGitHubUser(username) {
  const url = `https://api.github.com/users/${username}`;
  
  try {
    const response = await fetch(url);
    
    if (!response.ok) {
      if (response.status === 404) {
        throw new Error(`User '${username}' not found`);
      }
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    const user = await response.json();
    
    console.log('\n' + '='.repeat(50));
    console.log(`GitHub User: ${user.login}`);
    console.log('='.repeat(50));
    console.log(`Name: ${user.name || 'N/A'}`);
    console.log(`Bio: ${user.bio || 'N/A'}`);
    console.log(`Public Repos: ${user.public_repos}`);
    console.log(`Followers: ${user.followers}`);
    console.log(`Following: ${user.following}`);
    console.log(`Profile: ${user.html_url}`);
    
  } catch (error) {
    console.error('Error:', error.message);
  }
}

// Test the function
fetchGitHubUser('octocat');
fetchGitHubUser('torvalds');
```

## What's Next?

Now you know how to make API requests! Next, you'll learn about:
- API authentication methods
- Working with JSON data in depth

Ready to practice? Try the exercises below!

---

## 📝 Practice Problems

### Problem 1: Basic API Requests (Easy)
**File**: `problem1.md` and `problem1.py` or `problem1.js`

Use the **JSONPlaceholder API** to practice basic requests.

**Tasks:**
1. Fetch all posts: `https://jsonplaceholder.typicode.com/posts`
2. Fetch a specific post (ID 1): `https://jsonplaceholder.typicode.com/posts/1`
3. Fetch all users: `https://jsonplaceholder.typicode.com/users`
4. Fetch comments for post 1: `https://jsonplaceholder.typicode.com/posts/1/comments`

For each request:
- Print the status code
- Print the number of items returned (if it's a list)
- Print relevant data (title, name, etc.)

**Try it with:**
- curl commands
- Python code
- JavaScript code (choose one or try both!)

### Problem 2: Pokemon Data Explorer (Medium)
**File**: `problem2.md` and `problem2.py` or `problem2.js`

Use the **PokeAPI** to build a Pokemon information tool.

**Requirements:**
1. Create a function that takes a Pokemon name and fetches its data
2. Display:
   - Name
   - Types (e.g., "electric", "water")
   - Abilities
   - Height and weight
   - Stats (HP, Attack, Defense, etc.)
3. Handle errors (Pokemon not found, network errors)
4. Allow the user to search for multiple Pokemon
5. BONUS: Fetch and display the Pokemon's evolution chain

**Test with these Pokemon:**
- pikachu
- charizard
- mewtwo
- ditto
- invalidname (to test error handling)

### Problem 3: GitHub Repository Analyzer (Hard)
**File**: `problem3.md` and `problem3.py` or `problem3.js`

Build a tool that analyzes GitHub repositories using the GitHub API.

**Requirements:**

1. **Fetch Repository Info**
   - API: `https://api.github.com/repos/{owner}/{repo}`
   - Display: name, description, stars, forks, language, open issues

2. **List Recent Commits**
   - API: `https://api.github.com/repos/{owner}/{repo}/commits`
   - Display: last 5 commits with author and message

3. **List Contributors**
   - API: `https://api.github.com/repos/{owner}/{repo}/contributors`
   - Display: top 5 contributors with their contribution count

4. **Error Handling**
   - Handle repository not found (404)
   - Handle rate limiting (403)
   - Handle network errors

5. **Advanced Features** (Choose at least 2):
   - Compare two repositories side-by-side
   - Show repository languages breakdown
   - Fetch and display recent pull requests
   - Show repository issues statistics
   - Calculate and display "activity score" based on commits, stars, and forks

6. **Rate Limiting**
   - GitHub API has rate limits (60 requests/hour without auth)
   - Check remaining rate limit: `https://api.github.com/rate_limit`
   - Display remaining requests to user
   - Handle rate limit gracefully

**Test with these repositories:**
- microsoft/vscode
- facebook/react
- python/cpython
- torvalds/linux

**Bonus Challenges:**
- Add command-line arguments to specify repository
- Save results to a JSON file
- Create a simple comparison feature between two repos
- Add progress indicators for multiple requests

---

## 🎯 Solutions

### Problem 1 Solution (Python)

```python
import requests

def fetch_all_posts():
    """Fetch all posts"""
    url = "https://jsonplaceholder.typicode.com/posts"
    response = requests.get(url)
    
    print(f"Status Code: {response.status_code}")
    
    if response.status_code == 200:
        posts = response.json()
        print(f"Number of posts: {len(posts)}")
        print(f"\nFirst post:")
        print(f"  Title: {posts[0]['title']}")
        print(f"  Body: {posts[0]['body'][:50]}...")

def fetch_specific_post(post_id):
    """Fetch a specific post"""
    url = f"https://jsonplaceholder.typicode.com/posts/{post_id}"
    response = requests.get(url)
    
    print(f"\nStatus Code: {response.status_code}")
    
    if response.status_code == 200:
        post = response.json()
        print(f"Post {post_id}:")
        print(f"  Title: {post['title']}")
        print(f"  Body: {post['body']}")

def fetch_all_users():
    """Fetch all users"""
    url = "https://jsonplaceholder.typicode.com/users"
    response = requests.get(url)
    
    print(f"\nStatus Code: {response.status_code}")
    
    if response.status_code == 200:
        users = response.json()
        print(f"Number of users: {len(users)}")
        print(f"\nFirst three users:")
        for user in users[:3]:
            print(f"  - {user['name']} ({user['email']})")

def fetch_post_comments(post_id):
    """Fetch comments for a post"""
    url = f"https://jsonplaceholder.typicode.com/posts/{post_id}/comments"
    response = requests.get(url)
    
    print(f"\nStatus Code: {response.status_code}")
    
    if response.status_code == 200:
        comments = response.json()
        print(f"Number of comments on post {post_id}: {len(comments)}")
        print(f"\nFirst comment:")
        print(f"  Name: {comments[0]['name']}")
        print(f"  Email: {comments[0]['email']}")
        print(f"  Body: {comments[0]['body'][:50]}...")

# Run all functions
if __name__ == "__main__":
    fetch_all_posts()
    fetch_specific_post(1)
    fetch_all_users()
    fetch_post_comments(1)
```

### Problem 1 Solution (curl)

```bash
# Fetch all posts
curl https://jsonplaceholder.typicode.com/posts

# Fetch specific post
curl https://jsonplaceholder.typicode.com/posts/1

# Fetch all users
curl https://jsonplaceholder.typicode.com/users

# Fetch comments for post 1
curl https://jsonplaceholder.typicode.com/posts/1/comments

# With formatted output (if you have jq installed)
curl https://jsonplaceholder.typicode.com/posts/1 | jq
```

### Problem 2 Solution Outline

```python
import requests

def get_pokemon_info(pokemon_name):
    """Fetch and display Pokemon information"""
    url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name.lower()}"
    
    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()
        
        pokemon = response.json()
        
        print(f"\n{'='*50}")
        print(f"Pokemon: {pokemon['name'].title()}")
        print(f"{'='*50}")
        
        # Types
        types = [t['type']['name'] for t in pokemon['types']]
        print(f"Types: {', '.join(types)}")
        
        # Abilities
        abilities = [a['ability']['name'] for a in pokemon['abilities']]
        print(f"Abilities: {', '.join(abilities)}")
        
        # Physical attributes
        print(f"Height: {pokemon['height']/10}m")
        print(f"Weight: {pokemon['weight']/10}kg")
        
        # Stats
        print(f"\nStats:")
        for stat in pokemon['stats']:
            stat_name = stat['stat']['name']
            stat_value = stat['base_stat']
            print(f"  {stat_name}: {stat_value}")
            
    except requests.exceptions.HTTPError as e:
        if response.status_code == 404:
            print(f"Pokemon '{pokemon_name}' not found!")
        else:
            print(f"HTTP error: {e}")
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")

# Test
pokemon_list = ['pikachu', 'charizard', 'mewtwo', 'ditto', 'invalidname']
for pokemon in pokemon_list:
    get_pokemon_info(pokemon)
```

### Problem 3 Solution Outline

```python
import requests
import time

class GitHubRepoAnalyzer:
    BASE_URL = "https://api.github.com"
    
    def __init__(self):
        self.session = requests.Session()
    
    def get_repo_info(self, owner, repo):
        """Get repository information"""
        url = f"{self.BASE_URL}/repos/{owner}/{repo}"
        response = self.session.get(url)
        
        if response.status_code == 404:
            print(f"Repository {owner}/{repo} not found")
            return None
        
        response.raise_for_status()
        return response.json()
    
    def get_commits(self, owner, repo, limit=5):
        """Get recent commits"""
        url = f"{self.BASE_URL}/repos/{owner}/{repo}/commits"
        params = {'per_page': limit}
        response = self.session.get(url, params=params)
        response.raise_for_status()
        return response.json()
    
    def get_contributors(self, owner, repo, limit=5):
        """Get top contributors"""
        url = f"{self.BASE_URL}/repos/{owner}/{repo}/contributors"
        params = {'per_page': limit}
        response = self.session.get(url, params=params)
        response.raise_for_status()
        return response.json()
    
    def check_rate_limit(self):
        """Check API rate limit"""
        url = f"{self.BASE_URL}/rate_limit"
        response = self.session.get(url)
        data = response.json()
        return data['rate']['remaining'], data['rate']['limit']
    
    def analyze_repo(self, owner, repo):
        """Complete repository analysis"""
        try:
            # Check rate limit first
            remaining, limit = self.check_rate_limit()
            print(f"API Rate Limit: {remaining}/{limit} remaining\n")
            
            # Get repo info
            print(f"Analyzing {owner}/{repo}...")
            repo_data = self.get_repo_info(owner, repo)
            
            if not repo_data:
                return
            
            print(f"\n{'='*60}")
            print(f"Repository: {repo_data['full_name']}")
            print(f"{'='*60}")
            print(f"Description: {repo_data['description']}")
            print(f"Language: {repo_data['language']}")
            print(f"Stars: {repo_data['stargazers_count']}")
            print(f"Forks: {repo_data['forks_count']}")
            print(f"Open Issues: {repo_data['open_issues_count']}")
            
            # Get recent commits
            print(f"\nRecent Commits:")
            commits = self.get_commits(owner, repo)
            for i, commit in enumerate(commits, 1):
                author = commit['commit']['author']['name']
                message = commit['commit']['message'].split('\n')[0][:60]
                print(f"  {i}. {author}: {message}")
            
            # Get contributors
            print(f"\nTop Contributors:")
            contributors = self.get_contributors(owner, repo)
            for i, contributor in enumerate(contributors, 1):
                print(f"  {i}. {contributor['login']} - {contributor['contributions']} contributions")
                
        except requests.exceptions.RequestException as e:
            print(f"Error: {e}")

# Usage
analyzer = GitHubRepoAnalyzer()
analyzer.analyze_repo("microsoft", "vscode")
```

---

**Excellent work! 🎉**

Next up: **[05-api-authentication](../05-api-authentication/)** - Learn how to secure and authenticate API requests!
