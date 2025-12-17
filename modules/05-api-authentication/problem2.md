# Problem 2: GitHub Authentication (Medium)

## Instructions

Build a tool that uses GitHub's API with token authentication.

**GitHub API Documentation**: https://docs.github.com/en/rest

---

## Setup

### Step 1: Create a Personal Access Token

1. Go to: https://github.com/settings/tokens
2. Click "Generate new token" → "Generate new token (classic)"
3. Give it a descriptive name (e.g., "API Learning Project")
4. Select scopes (permissions):
   - `repo` (if you want to create repositories)
   - `user` (read user info)
   - `public_repo` (for public repositories only)
5. Click "Generate token"
6. **IMPORTANT**: Copy the token immediately - you won't be able to see it again!

---

### Step 2: Store Token Securely

Create a `.env` file:

```
GITHUB_TOKEN=ghp_your_actual_token_here
```

Add to `.gitignore`:
```
.env
```

---

## Core Requirements

Build a GitHub client that can:

1. **Get authenticated user info**
   - Display: username, name, bio, public repos count
   
2. **List user's repositories**
   - Display: name, description, stars, language
   
3. **Compare rate limits**
   - Show rate limits with and without authentication
   
4. **Error handling**
   - Invalid token
   - Rate limit exceeded
   - Network errors

---

## Your Code

### Python Template

```python
import requests
import os
from dotenv import load_dotenv

load_dotenv()

class GitHubClient:
    """Client for interacting with GitHub API"""
    
    def __init__(self):
        self.token = os.environ.get('GITHUB_TOKEN')
        self.base_url = 'https://api.github.com'
        self.headers = {
            'Authorization': f'token {self.token}',
            'Accept': 'application/vnd.github.v3+json'
        }
    
    def get_authenticated_user(self):
        """Get info about the authenticated user"""
        # TODO: Make API request to /user endpoint
        # TODO: Handle errors
        # TODO: Return user data
        pass
    
    def list_user_repos(self, username=None):
        """List repositories for a user"""
        # TODO: If username is None, use authenticated user
        # TODO: Make API request
        # TODO: Return repositories list
        pass
    
    def check_rate_limit(self):
        """Check current rate limit status"""
        # TODO: Make request to /rate_limit endpoint
        # TODO: Return rate limit info
        pass
    
    def compare_auth_rates(self):
        """Compare rate limits with and without auth"""
        # TODO: Get rate limit with auth
        # TODO: Get rate limit without auth
        # TODO: Display comparison
        pass

def main():
    """Main function"""
    client = GitHubClient()
    
    # TODO: Test all functions
    pass

if __name__ == "__main__":
    main()
```

### JavaScript Template

```javascript
require('dotenv').config();

class GitHubClient {
  constructor() {
    this.token = process.env.GITHUB_TOKEN;
    this.baseURL = 'https://api.github.com';
    this.headers = {
      'Authorization': `token ${this.token}`,
      'Accept': 'application/vnd.github.v3+json'
    };
  }
  
  async getAuthenticatedUser() {
    // TODO: Make API request to /user endpoint
    // TODO: Handle errors
    // TODO: Return user data
  }
  
  async listUserRepos(username = null) {
    // TODO: If username is null, use authenticated user
    // TODO: Make API request
    // TODO: Return repositories list
  }
  
  async checkRateLimit() {
    // TODO: Make request to /rate_limit endpoint
    // TODO: Return rate limit info
  }
  
  async compareAuthRates() {
    // TODO: Get rate limit with auth
    // TODO: Get rate limit without auth
    // TODO: Display comparison
  }
}

async function main() {
  const client = new GitHubClient();
  
  // TODO: Test all functions
}

main();
```

---

## Expected Output

```
==================================================
Authenticated User Information
==================================================
Username: johndoe
Name: John Doe
Bio: Software developer and open source enthusiast
Public Repos: 42
Followers: 150
Following: 80

==================================================
Your Repositories
==================================================
1. awesome-project ⭐ 245
   Description: An awesome project for doing awesome things
   Language: Python

2. learning-apis ⭐ 12
   Description: Learning about APIs
   Language: JavaScript

3. my-website ⭐ 5
   Description: Personal portfolio website
   Language: HTML

==================================================
Rate Limit Comparison
==================================================
With Authentication:    5000 requests/hour (4998 remaining)
Without Authentication: 60 requests/hour (58 remaining)

Benefit of authentication: 83.3x more requests!
```

---

## Testing Checklist

- [ ] Token loaded from environment variable
- [ ] Successfully authenticates with GitHub
- [ ] Fetches authenticated user info
- [ ] Lists user's repositories
- [ ] Checks rate limits correctly
- [ ] Compares authenticated vs unauthenticated rates
- [ ] Handles invalid token gracefully
- [ ] Handles rate limit exceeded
- [ ] Code is well-structured and documented
- [ ] Token NOT committed to git

---

## Part 2: Advanced Features

Implement at least **3** of these features:

### Feature 1: Star/Unstar a Repository
```python
def star_repository(self, owner, repo):
    """Star a repository"""
    # PUT /user/starred/{owner}/{repo}
    pass

def unstar_repository(self, owner, repo):
    """Unstar a repository"""
    # DELETE /user/starred/{owner}/{repo}
    pass

def check_if_starred(self, owner, repo):
    """Check if you've starred a repository"""
    # GET /user/starred/{owner}/{repo}
    # Returns 204 if starred, 404 if not
    pass
```

**Your Code:**
```python
# Your code here










```

---

### Feature 2: Create a Repository
```python
def create_repository(self, name, description, private=False):
    """Create a new repository"""
    # POST /user/repos
    # Be careful with this one!
    pass
```

**Your Code:**
```python
# Your code here










```

---

### Feature 3: List Followers and Following
```python
def get_followers(self, username=None):
    """Get user's followers"""
    pass

def get_following(self, username=None):
    """Get who the user is following"""
    pass
```

**Your Code:**
```python
# Your code here










```

---

### Feature 4: Search Repositories
```python
def search_repositories(self, query, sort='stars'):
    """Search for repositories"""
    # GET /search/repositories
    pass
```

**Your Code:**
```python
# Your code here










```

---

### Feature 5: Get Repository Languages
```python
def get_repo_languages(self, owner, repo):
    """Get programming languages used in a repository"""
    # GET /repos/{owner}/{repo}/languages
    pass
```

**Your Code:**
```python
# Your code here










```

---

## Part 3: Token Validation

Implement token validation and refresh logic:

```python
def validate_token(self):
    """Check if the token is valid"""
    # TODO: Make a simple API request
    # TODO: Check response status
    # TODO: Return True/False
    pass

def get_token_scopes(self):
    """Get the scopes/permissions of the current token"""
    # Hint: Check the 'X-OAuth-Scopes' header in response
    pass
```

**Your Code:**
```python
# Your code here










```

---

## Bonus Challenge

### GitHub Profile Summary

Create a comprehensive profile summary that includes:
- User info
- Total stars across all repos
- Most used programming language
- Contribution activity
- Top repositories by stars

**Your Code:**
```python
# Your code here













```

---

## Reflection Questions

1. **Why does GitHub offer higher rate limits for authenticated requests?**
```



```

2. **What are the security implications of using a personal access token?**
```



```

3. **How would you implement automatic token refresh in a long-running application?**
```



```

4. **Why is it important to request only the minimum necessary scopes for your token?**
```



```

---

## Testing

Test your implementation with:
- [ ] Your own GitHub account
- [ ] Public profiles (e.g., 'torvalds', 'gvanrossum')
- [ ] Invalid tokens (test error handling)
- [ ] Rate limit checks before and after operations

---

**Excellent work with token authentication! 🎉**

**Check the main README for solution code!**
