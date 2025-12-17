# Project 2: GitHub Profile Viewer 👨‍💻

**Difficulty**: Beginner to Intermediate  
**Estimated Time**: 3-4 hours  
**Concepts Used**: REST APIs, Authentication, Multiple endpoints, Data aggregation

## 📋 Project Overview

Create an application that displays GitHub user profiles, including their repositories, followers, and contribution statistics. This project introduces you to working with a well-documented REST API and handling multiple related API calls.

## 🎯 Learning Objectives

By completing this project, you will:
- Work with a professional REST API (GitHub API)
- Make multiple related API requests
- Combine data from different endpoints
- Handle pagination in API responses
- Work with API rate limits
- Display complex data structures

## 🛠️ What You'll Build

An application that:
1. Accepts a GitHub username as input
2. Displays user profile information (avatar, bio, location, etc.)
3. Lists the user's public repositories
4. Shows repository statistics (stars, forks, languages)
5. Displays follower and following counts
6. Handles users that don't exist

## 📚 Prerequisites

Before starting this project, make sure you've completed:
- [Module 1: What Are APIs?](../../modules/01-what-are-apis/)
- [Module 3: REST APIs](../../modules/03-rest-apis/)
- [Module 4: Making API Requests](../../modules/04-making-api-requests/)
- [Module 5: API Authentication](../../modules/05-api-authentication/)
- [Project 1: Weather Dashboard](../01-weather-dashboard/)

## 🚀 Getting Started

### Step 1: Understand the GitHub API

**Good News**: GitHub API doesn't require authentication for basic requests!

**Documentation**: [GitHub REST API Documentation](https://docs.github.com/en/rest)

**Key Endpoints**:
- User Profile: `GET https://api.github.com/users/{username}`
- User Repos: `GET https://api.github.com/users/{username}/repos`
- User Followers: `GET https://api.github.com/users/{username}/followers`
- User Following: `GET https://api.github.com/users/{username}/following`

### Step 2: Test the API

Try these URLs in your browser (replace `octocat` with any username):

**User Profile**:
```
https://api.github.com/users/octocat
```

**User Repositories**:
```
https://api.github.com/users/octocat/repos
```

### Step 3: Understand Rate Limits

- **Unauthenticated requests**: 60 requests per hour
- **Authenticated requests**: 5,000 requests per hour

For this project, start without authentication. If you need more requests:
1. Create a Personal Access Token on GitHub
2. Include it in your requests: `Authorization: token YOUR_TOKEN`

### Step 4: Analyze the Response Data

When you request `https://api.github.com/users/octocat`, you get:

```json
{
  "login": "octocat",
  "id": 583231,
  "avatar_url": "https://avatars.githubusercontent.com/u/583231?v=4",
  "name": "The Octocat",
  "company": "@github",
  "blog": "https://github.blog",
  "location": "San Francisco",
  "bio": null,
  "public_repos": 8,
  "followers": 9000,
  "following": 9,
  "created_at": "2011-01-25T18:44:36Z"
}
```

**Important fields**:
- `login`: Username
- `name`: Display name
- `avatar_url`: Profile picture URL
- `bio`: User biography
- `public_repos`: Number of public repositories
- `followers`: Follower count
- `following`: Following count
- `created_at`: When the user joined GitHub

## 💻 Implementation Guide

### Architecture Overview

Your application will need:
1. **Input Handler**: Get username from user
2. **API Client**: Make requests to GitHub API
3. **Data Processor**: Extract and organize the data
4. **Display Module**: Show information in a readable format
5. **Error Handler**: Handle invalid users and API errors

### Python Implementation

```python
import requests
from datetime import datetime

class GitHubProfileViewer:
    BASE_URL = "https://api.github.com"
    
    def __init__(self):
        self.session = requests.Session()
        # Optional: Add your personal access token here
        # self.session.headers.update({'Authorization': 'token YOUR_TOKEN'})
    
    def get_user_profile(self, username):
        """Fetch user profile data"""
        url = f"{self.BASE_URL}/users/{username}"
        response = self.session.get(url)
        
        if response.status_code == 200:
            return response.json()
        elif response.status_code == 404:
            return None
        else:
            raise Exception(f"API Error: {response.status_code}")
    
    def get_user_repos(self, username, sort='updated', limit=10):
        """Fetch user's repositories"""
        url = f"{self.BASE_URL}/users/{username}/repos"
        params = {
            'sort': sort,
            'per_page': limit
        }
        response = self.session.get(url, params=params)
        
        if response.status_code == 200:
            return response.json()
        else:
            return []
    
    def format_date(self, date_string):
        """Convert ISO date to readable format"""
        date = datetime.fromisoformat(date_string.replace('Z', '+00:00'))
        return date.strftime('%B %d, %Y')
    
    def display_profile(self, profile):
        """Display user profile information"""
        print("\n" + "=" * 50)
        print(f"GitHub Profile: {profile['login']}")
        print("=" * 50)
        
        if profile.get('name'):
            print(f"Name: {profile['name']}")
        
        if profile.get('bio'):
            print(f"Bio: {profile['bio']}")
        
        if profile.get('location'):
            print(f"Location: {profile['location']}")
        
        if profile.get('company'):
            print(f"Company: {profile['company']}")
        
        if profile.get('blog'):
            print(f"Website: {profile['blog']}")
        
        print(f"\nPublic Repos: {profile['public_repos']}")
        print(f"Followers: {profile['followers']}")
        print(f"Following: {profile['following']}")
        print(f"Joined: {self.format_date(profile['created_at'])}")
        print(f"Profile: https://github.com/{profile['login']}")
    
    def display_repositories(self, repos):
        """Display user's repositories"""
        if not repos:
            print("\nNo public repositories found.")
            return
        
        print(f"\n{'=' * 50}")
        print(f"Top {len(repos)} Repositories")
        print('=' * 50)
        
        for i, repo in enumerate(repos, 1):
            print(f"\n{i}. {repo['name']}")
            
            if repo.get('description'):
                print(f"   Description: {repo['description']}")
            
            print(f"   ⭐ Stars: {repo['stargazers_count']} | "
                  f"🔱 Forks: {repo['forks_count']} | "
                  f"Language: {repo['language'] or 'N/A'}")
            
            print(f"   URL: {repo['html_url']}")
    
    def check_rate_limit(self):
        """Check remaining API rate limit"""
        url = f"{self.BASE_URL}/rate_limit"
        response = self.session.get(url)
        
        if response.status_code == 200:
            data = response.json()
            core = data['resources']['core']
            print(f"\nAPI Rate Limit: {core['remaining']}/{core['limit']} requests remaining")
            if core['remaining'] == 0:
                reset_time = datetime.fromtimestamp(core['reset'])
                print(f"Rate limit resets at: {reset_time}")

def main():
    viewer = GitHubProfileViewer()
    
    print("GitHub Profile Viewer")
    print("=" * 50)
    
    username = input("\nEnter GitHub username: ").strip()
    
    if not username:
        print("Error: Username cannot be empty")
        return
    
    try:
        # Fetch profile
        print(f"\nFetching profile for '{username}'...")
        profile = viewer.get_user_profile(username)
        
        if profile is None:
            print(f"Error: User '{username}' not found")
            return
        
        # Display profile
        viewer.display_profile(profile)
        
        # Fetch and display repositories
        print(f"\nFetching repositories...")
        repos = viewer.get_user_repos(username)
        viewer.display_repositories(repos)
        
        # Show rate limit status
        viewer.check_rate_limit()
        
    except Exception as e:
        print(f"An error occurred: {e}")

if __name__ == "__main__":
    main()
```

### JavaScript (Node.js) Implementation

```javascript
const fetch = require('node-fetch');

class GitHubProfileViewer {
    constructor() {
        this.baseUrl = 'https://api.github.com';
        // Optional: Add your personal access token
        this.headers = {
            // 'Authorization': 'token YOUR_TOKEN'
        };
    }

    async getUserProfile(username) {
        const url = `${this.baseUrl}/users/${username}`;
        try {
            const response = await fetch(url, { headers: this.headers });
            
            if (response.status === 200) {
                return await response.json();
            } else if (response.status === 404) {
                return null;
            } else {
                throw new Error(`API Error: ${response.status}`);
            }
        } catch (error) {
            throw new Error(`Network error: ${error.message}`);
        }
    }

    async getUserRepos(username, limit = 10) {
        const url = `${this.baseUrl}/users/${username}/repos?sort=updated&per_page=${limit}`;
        try {
            const response = await fetch(url, { headers: this.headers });
            
            if (response.status === 200) {
                return await response.json();
            } else {
                return [];
            }
        } catch (error) {
            console.error('Error fetching repos:', error);
            return [];
        }
    }

    formatDate(dateString) {
        const date = new Date(dateString);
        return date.toLocaleDateString('en-US', { 
            year: 'numeric', 
            month: 'long', 
            day: 'numeric' 
        });
    }

    displayProfile(profile) {
        console.log('\n' + '='.repeat(50));
        console.log(`GitHub Profile: ${profile.login}`);
        console.log('='.repeat(50));
        
        if (profile.name) console.log(`Name: ${profile.name}`);
        if (profile.bio) console.log(`Bio: ${profile.bio}`);
        if (profile.location) console.log(`Location: ${profile.location}`);
        if (profile.company) console.log(`Company: ${profile.company}`);
        if (profile.blog) console.log(`Website: ${profile.blog}`);
        
        console.log(`\nPublic Repos: ${profile.public_repos}`);
        console.log(`Followers: ${profile.followers}`);
        console.log(`Following: ${profile.following}`);
        console.log(`Joined: ${this.formatDate(profile.created_at)}`);
        console.log(`Profile: https://github.com/${profile.login}`);
    }

    displayRepositories(repos) {
        if (repos.length === 0) {
            console.log('\nNo public repositories found.');
            return;
        }

        console.log('\n' + '='.repeat(50));
        console.log(`Top ${repos.length} Repositories`);
        console.log('='.repeat(50));

        repos.forEach((repo, index) => {
            console.log(`\n${index + 1}. ${repo.name}`);
            
            if (repo.description) {
                console.log(`   Description: ${repo.description}`);
            }
            
            console.log(`   ⭐ Stars: ${repo.stargazers_count} | ` +
                       `🔱 Forks: ${repo.forks_count} | ` +
                       `Language: ${repo.language || 'N/A'}`);
            
            console.log(`   URL: ${repo.html_url}`);
        });
    }
}

async function main() {
    const readline = require('readline').createInterface({
        input: process.stdin,
        output: process.stdout
    });

    console.log('GitHub Profile Viewer');
    console.log('='.repeat(50));

    readline.question('\nEnter GitHub username: ', async (username) => {
        username = username.trim();
        
        if (!username) {
            console.log('Error: Username cannot be empty');
            readline.close();
            return;
        }

        const viewer = new GitHubProfileViewer();

        try {
            // Fetch profile
            console.log(`\nFetching profile for '${username}'...`);
            const profile = await viewer.getUserProfile(username);

            if (!profile) {
                console.log(`Error: User '${username}' not found`);
                readline.close();
                return;
            }

            // Display profile
            viewer.displayProfile(profile);

            // Fetch and display repositories
            console.log('\nFetching repositories...');
            const repos = await viewer.getUserRepos(username);
            viewer.displayRepositories(repos);

        } catch (error) {
            console.error(`An error occurred: ${error.message}`);
        }

        readline.close();
    });
}

main();
```

## ✅ Requirements Checklist

Your GitHub Profile Viewer should:

- [ ] Accept a GitHub username as input
- [ ] Fetch and display user profile information:
  - [ ] Username and display name
  - [ ] Bio (if available)
  - [ ] Location and company (if available)
  - [ ] Public repository count
  - [ ] Followers and following counts
  - [ ] Account creation date
- [ ] Fetch and display repositories:
  - [ ] Repository name
  - [ ] Description
  - [ ] Star count
  - [ ] Fork count
  - [ ] Primary language
  - [ ] Repository URL
- [ ] Handle errors:
  - [ ] User not found
  - [ ] Network errors
  - [ ] Rate limit exceeded

## 🎨 Bonus Challenges

1. **Web Interface** (Medium)
   - Create an HTML/CSS/JavaScript version
   - Display the user's avatar image
   - Make it responsive for mobile devices

2. **Additional Statistics** (Medium)
   - Calculate total stars across all repos
   - Show most used programming languages
   - Display contribution statistics

3. **Repository Search** (Medium)
   - Filter repositories by language
   - Search repositories by keyword
   - Sort by different criteria (stars, forks, recent)

4. **Followers/Following** (Medium-Hard)
   - Display list of followers and following
   - Show mutual followers
   - Implement pagination for large lists

5. **Compare Users** (Hard)
   - Compare two GitHub users side-by-side
   - Show similarities and differences
   - Visualize data with charts

6. **Authentication** (Hard)
   - Implement OAuth for authenticated requests
   - Access private repository data (with permission)
   - Show contribution graph

7. **Caching** (Hard)
   - Cache API responses to save rate limit
   - Implement time-based cache expiration
   - Store frequently accessed profiles locally

## 🐛 Common Issues and Solutions

### Issue: Rate Limit Exceeded
**Solution**:
- Wait for the rate limit to reset (check reset time)
- Create a Personal Access Token for 5,000 requests/hour
- Implement caching to reduce API calls

### Issue: User Has Too Many Repositories
**Solution**:
- Use pagination with `per_page` and `page` parameters
- Filter by most popular or recently updated
- Implement "Load More" functionality

### Issue: Some Data Fields Are Missing
**Solution**:
- Always check if fields exist before displaying
- Use default values for missing data
- Handle `null` values gracefully

## 📖 Learning Resources

- [GitHub REST API Documentation](https://docs.github.com/en/rest)
- [GitHub API Rate Limiting](https://docs.github.com/en/rest/overview/resources-in-the-rest-api#rate-limiting)
- [Creating Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
- [Pagination in REST APIs](https://docs.github.com/en/rest/guides/traversing-with-pagination)

## 🎯 Success Criteria

You've successfully completed this project when:
1. You can view any public GitHub user's profile
2. Repository information displays correctly
3. Errors are handled appropriately
4. The output is well-formatted and easy to read
5. You understand how to work with multiple API endpoints

## 🤔 Reflection Questions

After completing this project:

1. How does working with GitHub's API differ from the Weather API?
2. Why might you need authentication for some API requests?
3. How would you handle pagination for users with hundreds of repositories?
4. What are the benefits of GitHub providing this API?
5. How could rate limiting affect a production application?

## 📤 Share Your Work

- Screenshot your working application
- Try it with different GitHub users
- Share interesting profiles you discovered
- Consider adding it to your portfolio

---

**Need Help?**
- Read the GitHub API documentation thoroughly
- Test endpoints in your browser first
- Start with basic functionality, then add features
- Check the rate limit status regularly

**Ready for more?** Check out [Project 3: Recipe Finder App](../03-recipe-finder/) →

---

[← Back to Projects](../README.md) | [Main README](../../README.md)
