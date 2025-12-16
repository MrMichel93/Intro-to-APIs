# HTTP Basics 🌐

## Introduction

Now that you know what APIs are, let's learn about **HTTP** - the language that web APIs use to communicate! HTTP stands for **HyperText Transfer Protocol**, and it's the foundation of data communication on the World Wide Web.

Think of HTTP as the rules of a conversation between a client (your app) and a server (the API). Just like human conversations have greetings, questions, and responses, HTTP has its own structure.

## What is HTTP?

HTTP is a protocol (a set of rules) for transferring data over the internet. When you:
- Visit a website
- Submit a form
- Make an API request

...you're using HTTP!

## How HTTP Works

### The Request-Response Cycle

```
Client (You)  ----REQUEST---->  Server (API)
                                    |
                                Processing
                                    |
Client (You)  <----RESPONSE----  Server (API)
```

1. **Client sends a request**: "Hey server, can I have some data?"
2. **Server processes the request**: Looks up the data or performs an action
3. **Server sends a response**: "Here's your data!" or "Done!"

## HTTP Request Structure

An HTTP request has several parts:

### 1. **HTTP Method** (The Action)
Tells the server what you want to do:

- **GET**: Retrieve data (like reading)
  - Example: Get a list of users
  
- **POST**: Create new data (like writing)
  - Example: Create a new user account
  
- **PUT**: Update existing data completely (like rewriting)
  - Example: Update all info for a user
  
- **PATCH**: Update part of existing data (like editing)
  - Example: Update just a user's email
  
- **DELETE**: Remove data (like erasing)
  - Example: Delete a user account

**Real-World Analogy:**
- GET = Reading a book from the library
- POST = Donating a new book to the library
- PUT = Replacing an entire book with a new edition
- PATCH = Fixing a typo in one page of a book
- DELETE = Removing a book from the library

### 2. **URL/Endpoint** (The Address)
Where you're sending the request:
```
https://api.example.com/users
```

Breaking it down:
- `https://` - The protocol (secure HTTP)
- `api.example.com` - The domain (server address)
- `/users` - The path (specific endpoint)

### 3. **Headers** (Metadata)
Extra information about the request:

```
Content-Type: application/json
Authorization: Bearer your-token-here
Accept: application/json
```

Common headers:
- **Content-Type**: What format is the data in?
- **Authorization**: Credentials to prove who you are
- **Accept**: What format do you want the response in?

### 4. **Body** (The Data)
Data you're sending with the request (used with POST, PUT, PATCH):

```json
{
  "username": "student123",
  "email": "student@example.com",
  "age": 18
}
```

## HTTP Response Structure

When the server responds, it includes:

### 1. **Status Code** (The Result)
A three-digit number that tells you what happened:

**2xx - Success! 🎉**
- **200 OK**: Request successful, here's your data
- **201 Created**: New resource created successfully
- **204 No Content**: Success, but no data to return

**3xx - Redirection 🔄**
- **301 Moved Permanently**: Resource moved to a new URL
- **304 Not Modified**: Cached version is still good

**4xx - Client Errors ❌**
- **400 Bad Request**: Your request has errors
- **401 Unauthorized**: You need to log in
- **403 Forbidden**: You're logged in but don't have permission
- **404 Not Found**: Resource doesn't exist
- **429 Too Many Requests**: Slow down! You're making too many requests

**5xx - Server Errors 💥**
- **500 Internal Server Error**: Something went wrong on the server
- **503 Service Unavailable**: Server is down or overloaded

### 2. **Headers**
Metadata about the response:
```
Content-Type: application/json
Date: Mon, 16 Dec 2024 10:00:00 GMT
```

### 3. **Body**
The actual data you requested:
```json
{
  "id": 123,
  "username": "student123",
  "email": "student@example.com"
}
```

## Example HTTP Conversation

Let's say you want to get information about a user:

**Your Request:**
```
Method: GET
URL: https://api.example.com/users/123
Headers:
  Authorization: Bearer abc123xyz
  Accept: application/json
```

**Server's Response:**
```
Status: 200 OK
Headers:
  Content-Type: application/json
  Date: Mon, 16 Dec 2024 10:00:00 GMT
Body:
{
  "id": 123,
  "username": "student123",
  "email": "student@example.com",
  "joinDate": "2024-01-15"
}
```

## HTTPS vs HTTP

- **HTTP**: Data is sent in plain text (not secure)
- **HTTPS**: Data is encrypted (secure)
  - The 'S' stands for "Secure"
  - **Always use HTTPS for ALL API communications!**
  - This prevents eavesdropping, tampering, and man-in-the-middle attacks
  - Modern applications should never use plain HTTP for APIs

Think of it like:
- HTTP = Sending a postcard (anyone can read it)
- HTTPS = Sending a locked box (only the recipient can open it)

**Security Note**: Even for non-sensitive data, HTTPS protects against various attacks including session hijacking, content injection, and data manipulation.

## URL Parameters

Sometimes you need to send small amounts of data in the URL itself:

### Query Parameters
Add filters or options to your request:
```
https://api.example.com/users?age=18&city=Boston
```
- `?` starts the query parameters
- `age=18` filters users who are 18
- `&` separates multiple parameters
- `city=Boston` filters by city

### Path Parameters
Part of the URL path itself:
```
https://api.example.com/users/123/posts
```
- `123` is the user ID (path parameter)
- Gets posts for user 123

## Common HTTP Headers Explained

### Request Headers
- **User-Agent**: What browser/app is making the request
- **Accept-Language**: What language you prefer
- **Cookie**: Session information
- **Referer**: What page you came from

### Response Headers
- **Content-Length**: Size of the response data
- **Set-Cookie**: Server sending a cookie to store
- **Cache-Control**: How long to cache the response
- **Access-Control-Allow-Origin**: CORS settings (security)

## HTTP Best Practices

1. **Use the right method**: GET for reading, POST for creating, etc.
2. **Use HTTPS**: Always encrypt sensitive data
3. **Set appropriate headers**: Let the server know what you're sending
4. **Handle status codes**: Check if the request succeeded
5. **Include error handling**: Things can go wrong!

## What's Next?

Now you understand HTTP! Next, you'll learn about:
- REST APIs (a specific way to design APIs using HTTP)
- How to actually make API requests in code
- Authentication methods

Ready for practice? Try the exercises below!

---

## 📝 Practice Problems

### Problem 1: HTTP Method Match (Easy)
**File**: `problem1.md`

Match each scenario with the correct HTTP method (GET, POST, PUT, PATCH, DELETE):

1. You want to see a list of all books in a library
2. You want to add a new book to your personal reading list
3. You want to change your entire user profile information
4. You want to update just your profile picture
5. You want to remove a book from your reading list
6. You want to search for books by a specific author
7. You want to create a new user account
8. You want to see details of a specific book

Also, explain why each method is appropriate for that scenario.

### Problem 2: Status Code Detective (Medium)
**File**: `problem2.md`

You're building a social media app. For each situation below:
1. Identify what HTTP status code should be returned
2. Explain why that status code is appropriate
3. Describe what message you would show to the user

Scenarios:
1. User tries to view a profile that doesn't exist
2. User successfully posts a new photo
3. User tries to delete someone else's post
4. User's login credentials are correct
5. User submits a form with missing required fields
6. Server database crashes while processing a request
7. User tries to access their feed but isn't logged in
8. User tries to upload a file that's too large

### Problem 3: Design an API Conversation (Hard)
**File**: `problem3.md`

You're building a **Recipe API** that lets users search for recipes, save favorites, and submit their own recipes.

For each of these features, design the complete HTTP request and response:

**Feature 1: Search for Recipes**
- Design the HTTP request (method, URL with parameters, headers)
- Design a sample successful response (status code, headers, body)
- Design an error response if no recipes are found

**Feature 2: Save a Recipe to Favorites**
- Design the HTTP request
- Design a successful response
- Design an error response if the recipe doesn't exist

**Feature 3: Submit a New Recipe**
- Design the HTTP request (include sample recipe data in body)
- Design a successful response
- Design error responses for: missing data, unauthorized user

**Feature 4: Update a Recipe's Rating**
- Design the HTTP request
- Design responses for: success, recipe not found, unauthorized

Be detailed! Include:
- Exact HTTP methods
- Full URLs with any parameters
- Relevant headers
- Sample request/response bodies
- Appropriate status codes
- Error messages

---

## 🎯 Solutions

### Problem 1 Solution

1. **GET** - Reading/retrieving data doesn't change anything
2. **POST** - Creating a new item in your list
3. **PUT** - Replacing all profile data at once
4. **PATCH** - Updating only one piece of data
5. **DELETE** - Removing an item
6. **GET** - Searching is retrieving data with filters
7. **POST** - Creating a new resource (user account)
8. **GET** - Retrieving specific information

**Key Principle**: GET for reading, POST for creating, PUT/PATCH for updating, DELETE for removing.

### Problem 2 Solution

1. **404 Not Found**
   - The profile doesn't exist in the database
   - User message: "Oops! We couldn't find that profile. It may have been deleted."

2. **201 Created**
   - A new resource (photo post) was successfully created
   - User message: "Your photo has been posted! ✨"

3. **403 Forbidden**
   - User is authenticated but doesn't have permission
   - User message: "You don't have permission to delete this post."

4. **200 OK**
   - Login successful, returning user data
   - User message: "Welcome back!"

5. **400 Bad Request**
   - Client sent invalid/incomplete data
   - User message: "Please fill in all required fields: name, email, and password."

6. **500 Internal Server Error**
   - Server-side issue, not the user's fault
   - User message: "Something went wrong on our end. Please try again later."

7. **401 Unauthorized**
   - User needs to authenticate first
   - User message: "Please log in to view your feed."

8. **413 Payload Too Large** (or **400 Bad Request** with explanation)
   - File exceeds size limit
   - User message: "File too large. Maximum size is 5MB."

### Problem 3 Solution

**Feature 1: Search for Recipes**

Request:
```
Method: GET
URL: https://api.recipes.com/recipes?ingredient=chicken&cuisine=italian&maxTime=30
Headers:
  Accept: application/json
  User-Agent: RecipeApp/1.0
```

Successful Response:
```
Status: 200 OK
Headers:
  Content-Type: application/json
Body:
{
  "results": 15,
  "recipes": [
    {
      "id": 101,
      "name": "Chicken Parmesan",
      "cuisine": "Italian",
      "prepTime": 25,
      "difficulty": "Medium"
    },
    {
      "id": 102,
      "name": "Chicken Marsala",
      "cuisine": "Italian",
      "prepTime": 30,
      "difficulty": "Medium"
    }
  ]
}
```

Error Response (no results):
```
Status: 200 OK (still successful, just empty results)
Headers:
  Content-Type: application/json
Body:
{
  "results": 0,
  "recipes": [],
  "message": "No recipes found matching your criteria"
}
```

**Feature 2: Save a Recipe to Favorites**

Request:
```
Method: POST
URL: https://api.recipes.com/users/me/favorites
Headers:
  Content-Type: application/json
  Authorization: Bearer user-token-abc123
Body:
{
  "recipeId": 101
}
```

Successful Response:
```
Status: 201 Created
Headers:
  Content-Type: application/json
Body:
{
  "message": "Recipe added to favorites",
  "favorite": {
    "id": 5001,
    "recipeId": 101,
    "recipeName": "Chicken Parmesan",
    "addedDate": "2024-12-16T10:00:00Z"
  }
}
```

Error Response (recipe doesn't exist):
```
Status: 404 Not Found
Headers:
  Content-Type: application/json
Body:
{
  "error": "Recipe not found",
  "message": "Recipe with ID 101 does not exist"
}
```

**Feature 3: Submit a New Recipe**

Request:
```
Method: POST
URL: https://api.recipes.com/recipes
Headers:
  Content-Type: application/json
  Authorization: Bearer user-token-abc123
Body:
{
  "name": "Grandma's Chocolate Cookies",
  "cuisine": "American",
  "prepTime": 45,
  "servings": 24,
  "difficulty": "Easy",
  "ingredients": [
    "2 cups flour",
    "1 cup sugar",
    "1/2 cup cocoa powder"
  ],
  "instructions": "1. Mix dry ingredients..."
}
```

Successful Response:
```
Status: 201 Created
Headers:
  Content-Type: application/json
  Location: https://api.recipes.com/recipes/150
Body:
{
  "message": "Recipe created successfully",
  "recipe": {
    "id": 150,
    "name": "Grandma's Chocolate Cookies",
    "author": "student123",
    "createdDate": "2024-12-16T10:00:00Z"
  }
}
```

Error Response (missing data):
```
Status: 400 Bad Request
Headers:
  Content-Type: application/json
Body:
{
  "error": "Invalid request",
  "message": "Missing required fields: ingredients, instructions"
}
```

Error Response (unauthorized):
```
Status: 401 Unauthorized
Headers:
  Content-Type: application/json
Body:
{
  "error": "Authentication required",
  "message": "Please log in to submit recipes"
}
```

**Feature 4: Update a Recipe's Rating**

Request:
```
Method: PATCH
URL: https://api.recipes.com/recipes/101
Headers:
  Content-Type: application/json
  Authorization: Bearer user-token-abc123
Body:
{
  "rating": 5
}
```

Successful Response:
```
Status: 200 OK
Headers:
  Content-Type: application/json
Body:
{
  "message": "Rating updated successfully",
  "recipe": {
    "id": 101,
    "name": "Chicken Parmesan",
    "averageRating": 4.7,
    "totalRatings": 143
  }
}
```

Error Response (not found):
```
Status: 404 Not Found
Headers:
  Content-Type: application/json
Body:
{
  "error": "Recipe not found",
  "message": "Recipe with ID 101 does not exist"
}
```

Error Response (unauthorized):
```
Status: 401 Unauthorized
Headers:
  Content-Type: application/json
Body:
{
  "error": "Authentication required",
  "message": "Please log in to rate recipes"
}
```

---

**Excellent work! 🎉**

Next up: **[03-rest-apis](../03-rest-apis/)** - Learn the principles that make APIs RESTful!
