# Problem 2: Design a RESTful API (Medium)

## Instructions

Design a complete RESTful API for a **Movie Review System**.

Your system should handle:
- **Movies** (title, genre, year, director, rating)
- **Reviews** (rating, comment, reviewer)
- **Users** (name, email, favorite genres)

---

## Part 1: CRUD Endpoints

Design all CRUD endpoints for each resource.

### Movies Resource

For each endpoint, include:
- HTTP method
- URL path
- Brief description
- Expected status codes

**List all movies:**
```
Method:
URL:
Description:
Status codes:
```

**Get specific movie:**
```
Method:
URL:
Description:
Status codes:
```

**Create new movie:**
```
Method:
URL:
Description:
Status codes:
```

**Update movie:**
```
Method:
URL:
Description:
Status codes:
```

**Delete movie:**
```
Method:
URL:
Description:
Status codes:
```

---

### Reviews Resource

**List all reviews:**
```
Method:
URL:
Description:
Status codes:
```

**Get specific review:**
```
Method:
URL:
Description:
Status codes:
```

**Create review:**
```
Method:
URL:
Description:
Status codes:
```

**Update review:**
```
Method:
URL:
Description:
Status codes:
```

**Delete review:**
```
Method:
URL:
Description:
Status codes:
```

---

### Users Resource

**List all users:**
```
Method:
URL:
Description:
Status codes:
```

**Get user profile:**
```
Method:
URL:
Description:
Status codes:
```

**Create user:**
```
Method:
URL:
Description:
Status codes:
```

**Update user:**
```
Method:
URL:
Description:
Status codes:
```

**Delete user:**
```
Method:
URL:
Description:
Status codes:
```

---

## Part 2: Relationship Endpoints

Design at least **3 endpoints** that show relationships between resources.

**Endpoint 1:**
```
Method:
URL:
Description:
Example: GET /movies/123/reviews - Get all reviews for movie 123
```

**Endpoint 2:**
```
Method:
URL:
Description:
```

**Endpoint 3:**
```
Method:
URL:
Description:
```

**Additional endpoints (optional):**
```



```

---

## Part 3: Query Parameters

Design query parameters for filtering, searching, sorting, and pagination.

### Filtering Movies
```
Example endpoint with filters:


What filters does it support?


```

### Searching Movies
```
Example endpoint with search:


What can users search by?


```

### Sorting Reviews
```
Example endpoint with sorting:


What sort options are available?


```

### Pagination
```
Example endpoint with pagination:


What parameters control pagination?


```

---

## Part 4: Sample Requests and Responses

### Sample 1: Create a New Movie

**Request:**
```
Method:
URL:
Headers:


Body:




```

**Response:**
```
Status Code:
Body:






```

---

### Sample 2: Get All Reviews for a Movie

**Request:**
```
Method:
URL:
Query Parameters:
```

**Response:**
```
Status Code:
Body:










```

---

### Sample 3: Update a Review

**Request:**
```
Method:
URL:
Headers:


Body:



```

**Response:**
```
Status Code:
Body:






```

---

## Bonus Challenges

### Challenge 1: Design error responses
What would the API return if:
- User tries to review a movie that doesn't exist?
- User tries to delete someone else's review?

### Challenge 2: Add more features
Design endpoints for:
- User's watchlist (movies they want to watch)
- Top-rated movies
- Recently added movies

---

## Reflection

1. What was the most challenging part of designing this API?

2. How did you decide on the URL structure?

3. What would you add to make this API more useful?

---

**Check the main README for a complete solution example!**
