# REST APIs 🏗️

## Introduction

You've learned what APIs are and how HTTP works. Now let's talk about **REST** - a specific architectural style for designing APIs that's become the most popular way to build web APIs!

**REST** stands for **REpresentational State Transfer**. Don't worry about the fancy name - it's just a set of rules and best practices that make APIs consistent, predictable, and easy to use.

## What is a REST API?

A **RESTful API** (or REST API) is an API that follows REST principles. Think of REST as a rulebook for designing APIs that everyone agrees to follow, making it easier for developers to understand and use any REST API.

### The Restaurant Analogy 🍽️

Imagine you go to a restaurant:
- **Menu** = API documentation (shows what's available)
- **Table number** = Resource URL (where to find things)
- **Waiter** = HTTP methods (how you interact)
- **Order** = Request
- **Food** = Response data

A REST API is like a well-organized restaurant where:
- Everything has a clear address (URL)
- You use standard actions (GET, POST, etc.)
- The menu is consistent and predictable

## The 6 Principles of REST

### 1. **Client-Server Architecture** 👥
The client (your app) and server (API) are separate. They can evolve independently as long as the interface stays the same.

**Example**: Twitter can update their backend servers without breaking third-party apps that use their API.

### 2. **Stateless** 🔄
Each request contains all the information needed to complete it. The server doesn't remember previous requests.

**Analogy**: Every time you call tech support, you have to explain your problem from scratch. They don't remember your previous calls.

**Example**:
- ❌ Bad: "Get the next page" (server needs to remember current page)
- ✅ Good: "Get page 3" (request contains all needed info)

### 3. **Cacheable** 💾
Responses should indicate whether they can be cached (stored temporarily) to improve performance.

**Analogy**: Like saving a copy of a website for offline reading instead of downloading it every time.

**Example**: Weather data might be cached for 10 minutes since it doesn't change that quickly.

### 4. **Uniform Interface** 🎯
REST APIs follow consistent rules for how resources are accessed and manipulated.

**Key parts**:
- **Resource identification**: Everything has a unique URL
- **Resource manipulation**: Use standard HTTP methods
- **Self-descriptive messages**: Responses include all needed info
- **HATEOAS**: Links to related resources (advanced topic)

### 5. **Layered System** 🏢
The client doesn't need to know if it's talking directly to the server or through intermediaries (like load balancers or caches).

**Analogy**: When you call customer service, you don't know if they're in one building or spread across multiple locations.

### 6. **Code on Demand** (Optional) 📦
Servers can send executable code to clients if needed (like JavaScript).

**Example**: A website sending JavaScript that runs in your browser.

## REST Resource Design

### What is a Resource?

A **resource** is anything you want to expose through your API:
- Users
- Blog posts
- Products
- Comments
- Etc.

### Resource URLs (Endpoints)

REST uses **nouns** (not verbs) in URLs to represent resources:

✅ **Good REST URLs:**
```
GET    /users              # Get all users
GET    /users/123          # Get user with ID 123
POST   /users              # Create a new user
PUT    /users/123          # Update user 123
DELETE /users/123          # Delete user 123

GET    /users/123/posts    # Get posts by user 123
GET    /posts/456/comments # Get comments on post 456
```

❌ **Bad REST URLs (using verbs):**
```
GET    /getUsers
POST   /createUser
GET    /deleteUser/123
```

### Resource Hierarchy

Organize related resources hierarchically:

```
/users                    # Collection of users
/users/123               # Specific user
/users/123/posts         # Posts by this user
/users/123/posts/456     # Specific post by this user
/posts                   # All posts
/posts/456               # Specific post
/posts/456/comments      # Comments on this post
```

## RESTful Operations (CRUD)

REST maps HTTP methods to **CRUD** operations:

| Operation | HTTP Method | URL Example        | Purpose                          |
|-----------|-------------|--------------------|----------------------------------|
| Create    | POST        | POST /users        | Create new user                  |
| Read      | GET         | GET /users/123     | Get user 123                     |
| Update    | PUT         | PUT /users/123     | Replace entire user 123          |
| Update    | PATCH       | PATCH /users/123   | Update specific fields of user 123|
| Delete    | DELETE      | DELETE /users/123  | Delete user 123                  |

**PUT vs PATCH:**
- **PUT**: Complete replacement - send all fields, even unchanged ones
- **PATCH**: Partial update - send only the fields you want to change

### Examples

**Create a new blog post:**
```
POST /posts
Content-Type: application/json

{
  "title": "My First Post",
  "content": "Hello world!",
  "authorId": 123
}

Response: 201 Created
{
  "id": 789,
  "title": "My First Post",
  "createdAt": "2024-12-16T10:00:00Z"
}
```

**Read all posts:**
```
GET /posts

Response: 200 OK
{
  "posts": [
    {"id": 789, "title": "My First Post"},
    {"id": 790, "title": "Another Post"}
  ]
}
```

**Update a post:**
```
PUT /posts/789
Content-Type: application/json

{
  "title": "My Updated Post",
  "content": "Updated content!"
}

Response: 200 OK
{
  "id": 789,
  "title": "My Updated Post",
  "updatedAt": "2024-12-16T11:00:00Z"
}
```

**Delete a post:**
```
DELETE /posts/789

Response: 204 No Content
```

## REST API Best Practices

### 1. **Use Plural Nouns for Collections**
- ✅ `/users` not `/user`
- ✅ `/posts` not `/post`

### 2. **Use Proper HTTP Status Codes**
- `200 OK` - Successful GET, PUT, PATCH
- `201 Created` - Successful POST
- `204 No Content` - Successful DELETE
- `400 Bad Request` - Invalid request
- `404 Not Found` - Resource doesn't exist
- `500 Internal Server Error` - Server error

### 3. **Version Your API**
Include version in the URL or headers:
- `/v1/users`
- `/v2/users`

Why? So you can make changes without breaking existing apps.

### 4. **Use Query Parameters for Filtering**
```
GET /users?age=18&city=Boston
GET /posts?author=123&sort=date
GET /products?category=electronics&maxPrice=500
```

### 5. **Use Pagination for Large Collections**
```
GET /posts?page=2&limit=10
```

Response includes:
```json
{
  "posts": [...],
  "page": 2,
  "totalPages": 15,
  "totalResults": 150
}
```

### 6. **Return Appropriate Error Messages**
```json
{
  "error": "Bad Request",
  "message": "Email is required",
  "statusCode": 400
}
```

### 7. **Use HTTPS**
Always encrypt sensitive data!

### 8. **Be Consistent**
- Use the same naming conventions everywhere
- Return data in the same format
- Handle errors consistently

## REST vs. Non-REST APIs

### REST API Example:
```
GET /api/users/123
```
Clear, predictable, follows standards.

### Non-REST API Example:
```
GET /api/getUserById?id=123
POST /api/updateUserEmail
```
Uses verbs in URLs, inconsistent structure.

## Common REST Patterns

### 1. **Filtering**
```
GET /products?category=books&minPrice=10&maxPrice=50
```

### 2. **Sorting**
```
GET /posts?sort=date&order=desc
```

### 3. **Field Selection** (return only certain fields)
```
GET /users/123?fields=name,email
```

### 4. **Searching**
```
GET /posts?search=javascript&searchFields=title,content
```

### 5. **Nested Resources**
```
GET /users/123/posts      # Posts by user 123
POST /posts/456/comments  # Add comment to post 456
```

## REST Constraints in Action

Let's see how a blog API follows REST principles:

```
# Stateless - each request is independent
GET /posts/123
Authorization: Bearer token-abc-123

# Cacheable - response includes cache headers
Response:
Cache-Control: max-age=300
{
  "id": 123,
  "title": "REST APIs Explained"
}

# Uniform Interface - consistent patterns
GET /posts          # Collection
GET /posts/123      # Single resource
POST /posts         # Create
PUT /posts/123      # Update
DELETE /posts/123   # Delete

# Layered - client doesn't know about intermediaries
Client → Load Balancer → API Server → Database
(Client only knows about the API endpoint)
```

## Why Use REST?

1. **Simplicity**: Easy to understand and use
2. **Scalability**: Stateless nature allows easy scaling
3. **Flexibility**: Can return any data format (usually JSON)
4. **Independence**: Client and server can evolve separately
5. **Widespread adoption**: Most developers know it

## REST API Example: Social Media

Here's how a social media platform might design their REST API:

```
# Users
GET    /users              # List all users
GET    /users/123          # Get user profile
POST   /users              # Create new user
PUT    /users/123          # Update user profile
DELETE /users/123          # Delete user

# Posts
GET    /posts              # Get all posts
GET    /posts/456          # Get specific post
POST   /posts              # Create new post
PUT    /posts/456          # Update post
DELETE /posts/456          # Delete post

# Relationships
GET    /users/123/posts    # Get posts by user 123
GET    /users/123/followers # Get user's followers
POST   /users/123/follow   # Follow user 123
DELETE /users/123/follow   # Unfollow user 123

# Comments
GET    /posts/456/comments # Get comments on post
POST   /posts/456/comments # Add comment
DELETE /comments/789       # Delete comment
```

## What's Next?

Now you understand REST principles! Next, you'll learn:
- How to actually make API requests using code
- Authentication methods
- Working with JSON data

Ready to practice? Try the exercises below!

---

## 📝 Practice Problems

### Problem 1: RESTful or Not? (Easy)
**File**: `problem1.md`

Examine these API endpoints and determine if they follow REST principles. For each one:
1. Say if it's RESTful or not
2. Explain why or why not
3. If it's not RESTful, provide a better RESTful alternative

Endpoints to evaluate:
1. `GET /getAllUsers`
2. `POST /users`
3. `GET /users/delete/123`
4. `PUT /users/123`
5. `GET /user-profile?id=123`
6. `POST /createNewBlogPost`
7. `GET /posts/456/comments`
8. `DELETE /comments/789`
9. `GET /posts?category=tech&sort=date`
10. `POST /updateUserPassword`

### Problem 2: Design a RESTful API (Medium)
**File**: `problem2.md`

Design a complete RESTful API for a **Movie Review System**. Your system should handle:
- Movies (title, genre, year, director, rating)
- Reviews (rating, comment, reviewer)
- Users (name, email, favorite genres)

For each resource, design:

1. **All CRUD endpoints** with:
   - HTTP method
   - URL path
   - Brief description
   - Expected status codes

2. **At least 3 advanced endpoints** that show relationships between resources (e.g., getting all reviews for a movie)

3. **Query parameters** for:
   - Filtering movies by genre or year
   - Searching movies by title
   - Sorting reviews by rating or date
   - Pagination for large lists

4. **Sample request and response** for:
   - Creating a new movie
   - Getting all reviews for a specific movie
   - Updating a review

### Problem 3: REST API Critique and Redesign (Hard)
**File**: `problem3.md`

You've been hired to review and improve a badly designed API for an online learning platform. Below is their current API design.

**Current (Bad) API Design:**

```
# User operations
GET /getUser?userId=123
POST /registerNewUser
POST /updateUser?userId=123
GET /deleteUser?userId=123

# Course operations
GET /getCourseById?courseId=456
POST /addNewCourse
POST /updateCourseInfo
GET /removeCourse?courseId=456
GET /getAllCoursesForUser?userId=123

# Enrollment
POST /enrollUserInCourse?userId=123&courseId=456
GET /getUserEnrollments?userId=123
POST /dropCourse?userId=123&courseId=456

# Progress tracking
POST /saveProgress?userId=123&lessonId=789&completed=true
GET /getProgress?userId=123&courseId=456
```

**Your Tasks:**

1. **Identify Problems**: List at least 8 specific problems with this API design and explain why each is problematic

2. **Redesign the API**: Create a complete RESTful redesign with:
   - Proper resource hierarchy
   - Correct HTTP methods
   - Clean URL structure
   - All necessary endpoints

3. **Add Missing Features**: Identify at least 3 important features this API is missing and design endpoints for them

4. **Error Handling**: Design the error response structure and give examples for:
   - User tries to enroll in a course that doesn't exist
   - User tries to access another user's progress
   - Invalid data in a course creation request

5. **Documentation**: Write brief API documentation for your redesigned API that includes:
   - Resource overview
   - Authentication requirements
   - Common use cases
   - Example requests/responses

6. **Advanced Features**: Design endpoints for:
   - Course prerequisites (a course requires completing other courses first)
   - Course ratings and reviews
   - Instructor profiles
   - Student achievements/badges

Be thorough and think about scalability, security, and developer experience!

---

## 🎯 Solutions

### Problem 1 Solution

1. `GET /getAllUsers`
   - **Not RESTful** ❌
   - Uses verb "getAll" in URL
   - **Better**: `GET /users`

2. `POST /users`
   - **RESTful** ✅
   - Correct method and noun-based URL

3. `GET /users/delete/123`
   - **Not RESTful** ❌
   - Uses GET for deletion and verb in URL
   - **Better**: `DELETE /users/123`

4. `PUT /users/123`
   - **RESTful** ✅
   - Correct method and structure

5. `GET /user-profile?id=123`
   - **Somewhat RESTful** ⚠️
   - Works but not ideal. ID should be in path, not query
   - **Better**: `GET /users/123` or `GET /users/123/profile`

6. `POST /createNewBlogPost`
   - **Not RESTful** ❌
   - Uses verb in URL
   - **Better**: `POST /posts`

7. `GET /posts/456/comments`
   - **RESTful** ✅
   - Shows resource hierarchy clearly

8. `DELETE /comments/789`
   - **RESTful** ✅
   - Correct method and structure

9. `GET /posts?category=tech&sort=date`
   - **RESTful** ✅
   - Good use of query parameters for filtering

10. `POST /updateUserPassword`
    - **Not RESTful** ❌
    - Uses verb and POST for update
    - **Better**: `PATCH /users/123/password` or `PUT /users/123/password`

### Problem 2 Solution

**Movie Review System REST API**

**Movies Resource:**
```
GET    /movies                 # List all movies (200 OK)
GET    /movies/123             # Get movie details (200 OK, 404 Not Found)
POST   /movies                 # Create movie (201 Created, 400 Bad Request)
PUT    /movies/123             # Update movie (200 OK, 404 Not Found)
PATCH  /movies/123             # Partial update (200 OK, 404 Not Found)
DELETE /movies/123             # Delete movie (204 No Content, 404 Not Found)
```

**Reviews Resource:**
```
GET    /reviews                # List all reviews (200 OK)
GET    /reviews/456            # Get specific review (200 OK, 404 Not Found)
POST   /reviews                # Create review (201 Created)
PUT    /reviews/456            # Update review (200 OK, 404 Not Found)
DELETE /reviews/456            # Delete review (204 No Content, 404 Not Found)
```

**Users Resource:**
```
GET    /users                  # List all users (200 OK)
GET    /users/789              # Get user profile (200 OK, 404 Not Found)
POST   /users                  # Create user (201 Created)
PUT    /users/789              # Update user (200 OK, 404 Not Found)
DELETE /users/789              # Delete user (204 No Content)
```

**Relationship Endpoints:**
```
GET    /movies/123/reviews     # Get all reviews for movie 123
POST   /movies/123/reviews     # Add review to movie 123
GET    /users/789/reviews      # Get all reviews by user 789
GET    /users/789/favorites    # Get user's favorite movies
POST   /users/789/favorites/123 # Add movie to favorites
DELETE /users/789/favorites/123 # Remove from favorites
```

**Query Parameters:**
```
# Filtering
GET /movies?genre=action&year=2024&minRating=4.0

# Searching
GET /movies?search=inception&searchFields=title,director

# Sorting
GET /movies?sort=rating&order=desc
GET /reviews?sort=date&order=asc

# Pagination
GET /movies?page=2&limit=20
GET /reviews?page=1&limit=50
```

**Sample Request 1: Create a movie**
```
POST /movies
Content-Type: application/json
Authorization: Bearer admin-token-xyz

{
  "title": "The Matrix",
  "genre": "Sci-Fi",
  "year": 1999,
  "director": "Wachowski Sisters",
  "rating": 8.7
}

Response: 201 Created
Location: /movies/123
{
  "id": 123,
  "title": "The Matrix",
  "genre": "Sci-Fi",
  "year": 1999,
  "director": "Wachowski Sisters",
  "rating": 8.7,
  "createdAt": "2024-12-16T10:00:00Z"
}
```

**Sample Request 2: Get reviews for a movie**
```
GET /movies/123/reviews?sort=rating&order=desc&limit=10

Response: 200 OK
{
  "movieId": 123,
  "movieTitle": "The Matrix",
  "reviews": [
    {
      "id": 456,
      "userId": 789,
      "userName": "MovieFan123",
      "rating": 5,
      "comment": "Mind-blowing movie!",
      "createdAt": "2024-12-15T14:30:00Z"
    },
    {
      "id": 457,
      "userId": 790,
      "userName": "CinemaLover",
      "rating": 4.5,
      "comment": "Revolutionary visual effects",
      "createdAt": "2024-12-14T09:15:00Z"
    }
  ],
  "page": 1,
  "totalReviews": 245
}
```

**Sample Request 3: Update a review**
```
PATCH /reviews/456
Content-Type: application/json
Authorization: Bearer user-token-abc

{
  "rating": 5,
  "comment": "After watching again, it's even better!"
}

Response: 200 OK
{
  "id": 456,
  "movieId": 123,
  "userId": 789,
  "rating": 5,
  "comment": "After watching again, it's even better!",
  "updatedAt": "2024-12-16T11:00:00Z"
}
```

### Problem 3 Solution

**1. Problems with Current API:**

1. **Uses verbs in URLs** - `/getUser`, `/registerNewUser`, `/addNewCourse` (REST uses nouns)
2. **Inconsistent HTTP methods** - Using GET for delete, POST for updates
3. **IDs in query parameters** - Should be in URL path (`/users/123` not `?userId=123`)
4. **No resource hierarchy** - Doesn't show relationships clearly
5. **Mixed singular/plural** - Not consistent with naming
6. **Wrong HTTP methods** - `GET /deleteUser` should be DELETE
7. **Verbose URLs** - Too wordy, not concise
8. **Unclear relationships** - Hard to understand resource connections
9. **No versioning** - Will be hard to update later
10. **Query parameters for actions** - Actions should use HTTP methods, not query params

**2. Redesigned RESTful API:**

```
# Users
GET    /api/v1/users                     # List all users
GET    /api/v1/users/123                 # Get user profile
POST   /api/v1/users                     # Register new user
PUT    /api/v1/users/123                 # Update user profile
PATCH  /api/v1/users/123                 # Partial update
DELETE /api/v1/users/123                 # Delete user

# Courses
GET    /api/v1/courses                   # List all courses
GET    /api/v1/courses/456               # Get course details
POST   /api/v1/courses                   # Create course
PUT    /api/v1/courses/456               # Update course
DELETE /api/v1/courses/456               # Delete course

# Enrollments (relationship between users and courses)
GET    /api/v1/users/123/enrollments     # Get user's enrollments
POST   /api/v1/users/123/enrollments     # Enroll in course
DELETE /api/v1/users/123/enrollments/456 # Drop course

# Alternative: Course-centric view
GET    /api/v1/courses/456/students      # Get enrolled students
POST   /api/v1/courses/456/students/123  # Enroll student

# Progress
GET    /api/v1/users/123/courses/456/progress    # Get progress
PUT    /api/v1/users/123/courses/456/progress    # Update progress
GET    /api/v1/users/123/courses/456/lessons/789 # Get lesson status
PATCH  /api/v1/users/123/courses/456/lessons/789 # Mark lesson complete
```

**3. Missing Features:**

```
# Course Content Structure
GET    /api/v1/courses/456/lessons       # List lessons in course
GET    /api/v1/lessons/789                # Get lesson details
POST   /api/v1/courses/456/lessons       # Add lesson to course

# Certificates
GET    /api/v1/users/123/certificates    # Get user's certificates
GET    /api/v1/courses/456/certificate   # Get certificate for course
POST   /api/v1/users/123/certificates    # Generate certificate

# Course Search and Discovery
GET    /api/v1/courses?search=python&level=beginner&sort=popularity
```

**4. Error Handling:**

Error Response Structure:
```json
{
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "The requested resource could not be found",
    "statusCode": 404,
    "timestamp": "2024-12-16T10:00:00Z",
    "path": "/api/v1/courses/999"
  }
}
```

Examples:

**Course doesn't exist:**
```
POST /api/v1/users/123/enrollments
Body: { "courseId": 999 }

Response: 404 Not Found
{
  "error": {
    "code": "COURSE_NOT_FOUND",
    "message": "Course with ID 999 does not exist",
    "statusCode": 404
  }
}
```

**Unauthorized access:**
```
GET /api/v1/users/456/progress

Response: 403 Forbidden
{
  "error": {
    "code": "FORBIDDEN",
    "message": "You don't have permission to view this user's progress",
    "statusCode": 403
  }
}
```

**Invalid data:**
```
POST /api/v1/courses
Body: { "title": "" }

Response: 400 Bad Request
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request validation failed",
    "statusCode": 400,
    "details": [
      {
        "field": "title",
        "message": "Title is required and cannot be empty"
      },
      {
        "field": "instructor",
        "message": "Instructor ID is required"
      }
    ]
  }
}
```

**5. API Documentation:**

```markdown
# Learning Platform API v1

Base URL: `https://api.learningplatform.com/api/v1`

## Authentication
All endpoints require authentication via Bearer token:
```
Authorization: Bearer your-token-here
```

## Resources

### Users
Represents students and instructors on the platform.

### Courses
Learning courses with lessons and content.

### Enrollments
Relationship between users and courses they're taking.

### Progress
Tracks user advancement through course lessons.

## Common Use Cases

**1. Student enrolls in a course:**
```
POST /users/123/enrollments
Body: { "courseId": 456 }
```

**2. View course progress:**
```
GET /users/123/courses/456/progress
```

**3. Mark lesson complete:**
```
PATCH /users/123/courses/456/lessons/789
Body: { "completed": true, "score": 95 }
```

## Example Requests

**Get user's courses:**
```
GET /api/v1/users/123/enrollments

Response: 200 OK
{
  "enrollments": [
    {
      "courseId": 456,
      "courseTitle": "Python for Beginners",
      "enrolledDate": "2024-01-15",
      "progress": 45,
      "status": "in_progress"
    }
  ]
}
```
```

**6. Advanced Features:**

```
# Course Prerequisites
GET    /api/v1/courses/456/prerequisites    # Get required courses
POST   /api/v1/courses/456/prerequisites    # Add prerequisite
DELETE /api/v1/courses/456/prerequisites/789 # Remove prerequisite

# Verify user can enroll (checks prerequisites)
GET    /api/v1/users/123/courses/456/can-enroll

# Ratings and Reviews
GET    /api/v1/courses/456/reviews          # Get course reviews
POST   /api/v1/courses/456/reviews          # Add review
PUT    /api/v1/reviews/111                   # Update review
DELETE /api/v1/reviews/111                   # Delete review
GET    /api/v1/courses/456/rating           # Get average rating

# Instructors
GET    /api/v1/instructors                   # List instructors
GET    /api/v1/instructors/222               # Get instructor profile
GET    /api/v1/instructors/222/courses      # Courses by instructor
GET    /api/v1/instructors/222/rating       # Instructor rating

# Achievements/Badges
GET    /api/v1/users/123/achievements       # User's achievements
GET    /api/v1/achievements                  # All available achievements
POST   /api/v1/users/123/achievements       # Award achievement (admin only)
```

---

**Excellent work! 🎉**

Next up: **[04-making-api-requests](../04-making-api-requests/)** - Learn to actually call APIs using code!
