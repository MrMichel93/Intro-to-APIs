# Problem 3: GitHub Repository Analyzer (Hard)

## Instructions

Build a comprehensive tool that analyzes GitHub repositories using the GitHub API.

**GitHub API Documentation**: https://docs.github.com/en/rest

**Base URL**: `https://api.github.com`

**Note**: GitHub API has rate limits (60 requests/hour without authentication). Be mindful of this!

---

## Core Requirements

### 1. Fetch Repository Information

**API Endpoint**: `GET https://api.github.com/repos/{owner}/{repo}`

Display:
- Repository name
- Description
- Primary language
- Stars count
- Forks count
- Open issues count
- Created date
- Last updated date
- License (if available)

---

### 2. List Recent Commits

**API Endpoint**: `GET https://api.github.com/repos/{owner}/{repo}/commits`

Display the last 5 commits with:
- Commit SHA (first 7 characters)
- Author name
- Commit message (first line only)
- Date

---

### 3. List Top Contributors

**API Endpoint**: `GET https://api.github.com/repos/{owner}/{repo}/contributors`

Display top 5 contributors with:
- Username
- Number of contributions

---

### 4. Error Handling

Handle these scenarios:
- Repository not found (404)
- Rate limit exceeded (403)
- Network errors
- Invalid repository format

---

## Your Code

### Python Template

```python
import requests
import sys

class GitHubRepoAnalyzer:
    """Analyzer for GitHub repositories"""
    
    BASE_URL = "https://api.github.com"
    
    def __init__(self):
        self.session = requests.Session()
        # Optional: Add GitHub token for higher rate limits
        # self.session.headers.update({
        #     'Authorization': 'token YOUR_GITHUB_TOKEN'
        # })
    
    def get_repo_info(self, owner, repo):
        """Fetch repository information"""
        # Your code here
        pass
    
    def get_commits(self, owner, repo, limit=5):
        """Fetch recent commits"""
        # Your code here
        pass
    
    def get_contributors(self, owner, repo, limit=5):
        """Fetch top contributors"""
        # Your code here
        pass
    
    def check_rate_limit(self):
        """Check GitHub API rate limit"""
        url = f"{self.BASE_URL}/rate_limit"
        response = self.session.get(url)
        data = response.json()
        return data['rate']['remaining'], data['rate']['limit']
    
    def analyze_repo(self, owner, repo):
        """Complete repository analysis"""
        # Your code here
        # Combine all the above methods
        pass

def main():
    """Main function"""
    analyzer = GitHubRepoAnalyzer()
    
    # Test with these repositories
    test_repos = [
        ("microsoft", "vscode"),
        ("facebook", "react"),
    ]
    
    for owner, repo in test_repos:
        analyzer.analyze_repo(owner, repo)
        print("\n" + "="*60 + "\n")

if __name__ == "__main__":
    main()
```

### JavaScript Template

```javascript
class GitHubRepoAnalyzer {
  constructor() {
    this.baseURL = 'https://api.github.com';
    // Optional: Add GitHub token for higher rate limits
    // this.headers = {
    //   'Authorization': 'token YOUR_GITHUB_TOKEN'
    // };
  }
  
  async getRepoInfo(owner, repo) {
    // Your code here
  }
  
  async getCommits(owner, repo, limit = 5) {
    // Your code here
  }
  
  async getContributors(owner, repo, limit = 5) {
    // Your code here
  }
  
  async checkRateLimit() {
    const url = `${this.baseURL}/rate_limit`;
    const response = await fetch(url);
    const data = await response.json();
    return {
      remaining: data.rate.remaining,
      limit: data.rate.limit
    };
  }
  
  async analyzeRepo(owner, repo) {
    // Your code here
    // Combine all the above methods
  }
}

async function main() {
  const analyzer = new GitHubRepoAnalyzer();
  
  // Test with these repositories
  const testRepos = [
    ['microsoft', 'vscode'],
    ['facebook', 'react'],
  ];
  
  for (const [owner, repo] of testRepos) {
    await analyzer.analyzeRepo(owner, repo);
    console.log('\n' + '='.repeat(60) + '\n');
  }
}

main();
```

---

## Expected Output Example

```
API Rate Limit: 58/60 remaining

Analyzing microsoft/vscode...

============================================================
Repository: microsoft/vscode
============================================================
Description: Visual Studio Code
Language: TypeScript
Stars: 150000
Forks: 25000
Open Issues: 5000
Created: 2015-09-03
Last Updated: 2024-12-16
License: MIT

Recent Commits:
  1. abc1234 - John Doe: Fix syntax highlighting issue
  2. def5678 - Jane Smith: Update documentation
  3. ghi9012 - Bob Johnson: Add new feature for debugging
  4. jkl3456 - Alice Brown: Improve performance
  5. mno7890 - Charlie Wilson: Fix memory leak

Top Contributors:
  1. johndoe - 1500 contributions
  2. janesmith - 1200 contributions
  3. bobjohnson - 900 contributions
  4. alicebrown - 800 contributions
  5. charliewilson - 700 contributions
```

---

## Part 2: Advanced Features

Implement at least **2** of these advanced features:

### Feature 1: Compare Two Repositories
```
Allow user to compare two repositories side-by-side:
- Which has more stars?
- Which is more active (recent commits)?
- Which has more contributors?
```

**Your Code:**
```python
# Your code here










```

---

### Feature 2: Repository Languages Breakdown
```
API: GET /repos/{owner}/{repo}/languages

Display the programming languages used and their percentages
```

**Your Code:**
```python
# Your code here










```

---

### Feature 3: Recent Pull Requests
```
API: GET /repos/{owner}/{repo}/pulls

Display the 5 most recent pull requests:
- Title
- Author
- State (open/closed)
- Created date
```

**Your Code:**
```python
# Your code here










```

---

### Feature 4: Issues Statistics
```
API: GET /repos/{owner}/{repo}/issues

Analyze and display:
- Total open issues
- Issues opened this week
- Most common labels
```

**Your Code:**
```python
# Your code here










```

---

### Feature 5: Activity Score
```
Calculate a custom "activity score" based on:
- Number of commits in the last month
- Number of stars
- Number of forks
- Number of contributors

Create your own formula!
```

**Your Code:**
```python
# Your code here










```

---

## Part 3: User Interface

Choose at least **1**:

### Option 1: Command-Line Arguments
```bash
python problem3.py microsoft vscode
python problem3.py facebook react --compare torvalds linux
```

**Your Code:**
```python
import argparse

# Your code here










```

---

### Option 2: Interactive Menu
```
GitHub Repository Analyzer
--------------------------
1. Analyze a repository
2. Compare two repositories
3. Check rate limit
4. Exit

Choose an option:
```

**Your Code:**
```python
# Your code here










```

---

### Option 3: Save Results to JSON
```
Save analysis results to a JSON file for later reference
```

**Your Code:**
```python
import json

# Your code here










```

---

## Testing

Test your analyzer with these repositories:

1. **microsoft/vscode** - Large, active project
2. **facebook/react** - Very popular project
3. **python/cpython** - Python language implementation
4. **torvalds/linux** - Huge project with many contributors
5. **yourname/nonexistent** - Test error handling

---

## Testing Checklist

- [ ] Fetches repository info correctly
- [ ] Displays recent commits
- [ ] Shows top contributors
- [ ] Checks and displays rate limit
- [ ] Handles repository not found (404)
- [ ] Handles rate limit exceeded (403)
- [ ] Handles network errors
- [ ] At least 2 advanced features implemented
- [ ] Code is well-organized and modular
- [ ] Includes helpful comments
- [ ] User-friendly output formatting

---

## Bonus Challenges

### Challenge 1: GitHub Authentication
```
Add support for GitHub personal access token to increase rate limit to 5000/hour

Steps:
1. Create a token at: https://github.com/settings/tokens
2. Add it to your code (use environment variables!)
3. Test increased rate limit
```

**Your Code:**
```python
import os

# Your code here
```

---

### Challenge 2: Caching
```
Cache API responses to avoid hitting rate limits during development

Use a simple file-based cache or Python's functools.lru_cache
```

**Your Code:**
```python
# Your code here
```

---

### Challenge 3: Progress Indicators
```
Add progress indicators for multiple API calls

For Python: Use tqdm library
For JavaScript: Use cli-progress or similar
```

**Your Code:**
```python
# Your code here
```

---

## Reflection Questions

1. **How did you handle multiple API calls efficiently?**
```



```

2. **What strategy did you use to stay within rate limits?**
```



```

3. **What was the most complex part of this project?**
```



```

4. **How would you extend this tool to be even more useful?**
```



```

5. **What did you learn about the GitHub API?**
```



```

---

## Submission

Save your code as:
- `problem3.py` (for Python) or
- `problem3.js` (for JavaScript)

Include:
- Well-commented code
- README with usage instructions
- Example output

---

**Congratulations on building a real-world API tool! 🎉**

**This is the kind of project you can showcase in a portfolio!**

**Check the main README for solution approaches!**
