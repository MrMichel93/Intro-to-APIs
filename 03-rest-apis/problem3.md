# Problem 3: REST API Critique and Redesign (Hard)

## Instructions

You've been hired to review and improve a badly designed API for an online learning platform.

---

## Current (Bad) API Design

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

---

## Task 1: Identify Problems

List at least **8 specific problems** with this API design and explain why each is problematic.

**Problem 1:**
```


```

**Problem 2:**
```


```

**Problem 3:**
```


```

**Problem 4:**
```


```

**Problem 5:**
```


```

**Problem 6:**
```


```

**Problem 7:**
```


```

**Problem 8:**
```


```

**Additional problems (optional):**
```


```

---

## Task 2: Redesign the API

Create a complete RESTful redesign with proper resource hierarchy, correct HTTP methods, and clean URL structure.

### Users Endpoints
```








```

### Courses Endpoints
```








```

### Enrollments Endpoints
```
(Show the relationship between users and courses)






```

### Progress Endpoints
```






```

### Additional Resource Endpoints
```
(Any other endpoints you think are necessary)




```

---

## Task 3: Add Missing Features

Identify at least **3 important features** this API is missing and design endpoints for them.

**Missing Feature 1:**
```
Feature:
Why it's important:
Endpoints:




```

**Missing Feature 2:**
```
Feature:
Why it's important:
Endpoints:




```

**Missing Feature 3:**
```
Feature:
Why it's important:
Endpoints:




```

---

## Task 4: Error Handling

Design the error response structure and give examples.

### Error Response Structure
```json
{






}
```

### Example Error 1: User tries to enroll in a course that doesn't exist

**Request:**
```
Method:
URL:
Body:
```

**Response:**
```
Status Code:
Body:




```

---

### Example Error 2: User tries to access another user's progress

**Request:**
```
Method:
URL:
```

**Response:**
```
Status Code:
Body:




```

---

### Example Error 3: Invalid data in course creation

**Request:**
```
Method:
URL:
Body:


```

**Response:**
```
Status Code:
Body:






```

---

## Task 5: API Documentation

Write brief API documentation for your redesigned API.

### Overview
```
What does this API do?



```

### Base URL
```

```

### Authentication
```
How do users authenticate?



```

### Common Use Cases

**Use Case 1:**
```
Scenario:
Endpoints involved:
Example flow:



```

**Use Case 2:**
```
Scenario:
Endpoints involved:
Example flow:



```

### Example Request/Response

**Example: Get user's enrolled courses**
```
Request:
Method:
URL:
Headers:

Response:
Status:
Body:








```

---

## Task 6: Advanced Features

Design endpoints for these advanced features:

### Course Prerequisites
```
Description: A course requires completing other courses first

Endpoints:






Example usage:


```

---

### Course Ratings and Reviews
```
Description: Students can rate and review courses

Endpoints:






Example usage:


```

---

### Instructor Profiles
```
Description: Information about course instructors

Endpoints:






Example usage:


```

---

### Student Achievements/Badges
```
Description: Awards for completing milestones

Endpoints:






Example usage:


```

---

## Reflection Questions

1. **What were the biggest improvements in your redesign?**
```




```

2. **How does your design make the API easier to use?**
```




```

3. **What security considerations did you include?**
```




```

4. **If you had to add one more feature, what would it be and why?**
```




```

5. **How would you handle API versioning as the platform grows?**
```




```

---

**This is a comprehensive exercise - take your time and be thorough!**

**Check the main README for a complete solution!**
