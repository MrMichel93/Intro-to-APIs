# Problem 1: Basic API Requests (Easy)

## Instructions

Use the **JSONPlaceholder API** (https://jsonplaceholder.typicode.com) to practice making basic API requests.

This is a free fake REST API for testing and prototyping. Perfect for learning!

---

## Part 1: Using curl (Command Line)

Write curl commands for each of these requests and record the results:

### Task 1: Fetch all posts
```bash
# Your curl command:



# What status code did you get?


# How many posts were returned?


# What was the title of the first post?


```

---

### Task 2: Fetch a specific post (ID 1)
```bash
# Your curl command:



# What status code did you get?


# What was the post title?


# What was the userId?


```

---

### Task 3: Fetch all users
```bash
# Your curl command:



# How many users were returned?


# What was the name of the first user?


# What was their email?


```

---

### Task 4: Fetch comments for post 1
```bash
# Your curl command:



# How many comments were returned?


# What was the email of the first commenter?


```

---

## Part 2: Using Python or JavaScript

Choose Python OR JavaScript (or try both!) and write code to make the same requests.

### Setup

**For Python:**
```bash
pip install requests
```

**For JavaScript (Node.js):**
```bash
# No installation needed for fetch in Node.js 18+
# Or: npm install axios
```

---

### Task 1: Fetch all posts

**Your Code:**
```python
# Python example structure
import requests

def fetch_all_posts():
    # Your code here
    pass

# Test it
fetch_all_posts()
```

OR

```javascript
// JavaScript example structure
async function fetchAllPosts() {
  // Your code here
}

// Test it
fetchAllPosts();
```

**Output you should display:**
```
- Status code
- Number of posts
- Title of the first post
```

---

### Task 2: Fetch a specific post

**Your Code:**
```python
# Your code here




```

OR

```javascript
// Your code here




```

**Output you should display:**
```
- Status code
- Post title
- Post body
- User ID
```

---

### Task 3: Fetch all users

**Your Code:**
```python
# Your code here




```

OR

```javascript
// Your code here




```

**Output you should display:**
```
- Status code
- Number of users
- Name and email of the first 3 users
```

---

### Task 4: Fetch comments for post 1

**Your Code:**
```python
# Your code here




```

OR

```javascript
// Your code here




```

**Output you should display:**
```
- Status code
- Number of comments
- Name and body of the first comment (truncated to 50 characters)
```

---

## Part 3: Error Handling

Modify your code to handle these scenarios:

### Scenario 1: Post doesn't exist
Try fetching post ID 999999 (which doesn't exist).

**Your code:**
```




```

**What status code did you get?**
```

```

**How did you handle the error in your code?**
```


```

---

### Scenario 2: Network timeout
Add a timeout to your request (e.g., 1 second) and try with a slow endpoint.

**Your code:**
```




```

---

## Reflection Questions

1. **Which method did you find easier: curl or code? Why?**
```



```

2. **What was the most challenging part?**
```



```

3. **What did you learn about HTTP status codes?**
```



```

4. **When would you use curl vs. writing code?**
```



```

---

## Bonus Challenge

Create a function that:
1. Fetches a user by ID
2. Fetches all posts by that user
3. For each post, fetches the comments
4. Displays everything in an organized way

**Hint:** You'll need to make multiple API calls and combine the data!

---

**Check the main README for complete solution code!**
