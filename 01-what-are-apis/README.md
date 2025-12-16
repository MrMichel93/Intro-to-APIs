# What Are APIs? 🤔

## Introduction

Imagine you're at a restaurant. You don't go into the kitchen to cook your own food, right? Instead, you tell the waiter what you want, they go to the kitchen, and then bring your food back to you. 

An **API (Application Programming Interface)** works just like that waiter! It's a messenger that takes your request, tells a system what you want, and then returns the response back to you.

## What is an API?

An API is a set of rules and protocols that allows different software applications to communicate with each other. It defines the methods and data formats that applications can use to request and exchange information.

### Real-World Examples

1. **Weather Apps** 🌤️
   - When you check the weather on your phone, the app uses an API to request weather data from a weather service
   - The API returns the current temperature, forecast, etc.

2. **Social Media** 📱
   - When you share a YouTube link on Twitter, Twitter uses YouTube's API to fetch the video title and thumbnail
   - This happens automatically in the background

3. **Payment Systems** 💳
   - When you buy something online, the website uses a payment API (like Stripe or PayPal) to process your payment
   - The API securely handles the transaction

4. **Maps** 🗺️
   - Apps that show maps use APIs from Google Maps or other mapping services
   - The API provides map data, directions, and location information

## Why Are APIs Important?

1. **Reusability**: Developers don't have to reinvent the wheel. Why build your own payment system when you can use a payment API?

2. **Efficiency**: APIs let different systems work together smoothly without knowing each other's internal workings

3. **Security**: APIs provide controlled access to data. You can request information without accessing the entire database

4. **Scalability**: Companies can build services that others can use, creating ecosystems of applications

## Types of APIs

### 1. **Web APIs** (Most Common)
- Accessed over the internet using HTTP/HTTPS
- Examples: Twitter API, Google Maps API, Weather API

### 2. **Library/Framework APIs**
- Functions and methods provided by programming libraries
- Example: Python's `requests` library

### 3. **Operating System APIs**
- Allow programs to interact with the operating system
- Example: File system operations, window management

### 4. **Database APIs**
- Allow applications to communicate with databases
- Example: SQL queries

## How Do APIs Work?

Think of the API request-response cycle:

1. **Client Makes Request**: Your application (the client) sends a request to the API
2. **API Processes Request**: The API receives the request and processes it
3. **Server Responds**: The API sends back a response with the requested data or confirmation
4. **Client Receives Response**: Your application receives and uses the data

### Example Flow

```
You (Client) → Request Weather Data → Weather API → Weather Database
                                                           ↓
You (Client) ← Returns Weather Data ← Weather API ← Fetches Data
```

## API Endpoints

An **endpoint** is a specific URL where an API can be accessed. Think of it as an address where you send your requests.

Example endpoints:
- `https://api.weather.com/current` - Get current weather
- `https://api.weather.com/forecast` - Get weather forecast
- `https://api.twitter.com/tweets` - Access tweets

Each endpoint serves a different purpose and returns different data.

## Key Terminology

- **Client**: The application making the request (your code)
- **Server**: The system that hosts the API and provides the data
- **Request**: Asking the API for information or to perform an action
- **Response**: The data or result sent back by the API
- **Endpoint**: The URL where an API can be accessed

## What's Next?

Now that you understand what APIs are, you'll learn about:
- HTTP protocol (how APIs communicate)
- REST APIs (a popular API architecture)
- How to make actual API requests
- Authentication (keeping APIs secure)

Ready to practice? Try the exercises below!

---

## 📝 Practice Problems

### Problem 1: API Identification (Easy)
**File**: `problem1.md`

Look at these scenarios and identify which type of API (Web API, Library API, OS API, or Database API) is being used:

1. A mobile app displays a map showing nearby restaurants
2. A Python program uses `json.loads()` to parse data
3. A website allows users to log in with their Google account
4. An application saves user preferences to a file on your computer
5. A fitness app gets your step count from your phone's health data

Write your answers in `problem1.md`.

### Problem 2: Real-World API Uses (Medium)
**File**: `problem2.md`

Think about your favorite apps or websites. Choose THREE and research what APIs they might use. For each app:

1. Name the app/website
2. Describe what it does
3. List at least 2 APIs it likely uses and why
4. Explain how these APIs improve the user experience

Example format:
```
App: Spotify
Purpose: Music streaming service
APIs Used:
- Facebook API (for social login and sharing)
- Payment APIs like PayPal (for subscription payments)
Benefits: Users can log in easily with their Facebook account and pay securely without Spotify handling credit cards directly.
```

### Problem 3: Design Your Own API Concept (Hard)
**File**: `problem3.md`

Imagine you're building a **Book Library Management System** that other developers can integrate into their applications.

Design an API for this system by answering these questions:

1. **Purpose**: What will your API do? (What problems does it solve?)

2. **Endpoints**: List at least 5 endpoints your API would need. For each endpoint, describe:
   - The URL path (e.g., `/books`, `/users/favorites`)
   - What it does
   - What data it needs from the user (if any)
   - What data it returns

3. **Use Cases**: Describe 3 real-world scenarios where someone would use your API

4. **Security**: What information should be protected? How would you ensure only authorized users can access certain features?

5. **Data Format**: What format would your API use to send and receive data? (Hint: We'll learn about JSON later, but you can suggest a format)

Be creative and detailed! This exercise will help you think like an API designer.

---

## 🎯 Solutions

Solutions are learning tools! Try to complete the problems first, then check your work.

### Problem 1 Solution
1. **Web API** - The app uses a mapping service API like Google Maps API
2. **Library API** - `json.loads()` is a function from Python's JSON library
3. **Web API** - This uses Google's OAuth API for authentication
4. **OS API** - File system operations use the operating system's API
5. **OS API** (with some Web API) - Accessing health data uses the phone's OS API

### Problem 2 Solution
(Students will have different answers - this is just an example)

**Instagram**
- Purpose: Photo and video sharing social network
- APIs Used:
  - Facebook API (owned by same company, for cross-posting and login)
  - Cloud storage APIs (AWS or similar for storing photos/videos)
  - Payment API (for promoting posts)
- Benefits: Seamless integration with Facebook, reliable photo storage, secure payments

### Problem 3 Solution
(Students will have creative answers - here's an example framework)

**Book Library Management API**

1. **Purpose**: Allow developers to integrate book lending, catalog search, and user management into their applications

2. **Endpoints**:
   - `GET /books` - Search and list all available books
   - `GET /books/{id}` - Get details about a specific book
   - `POST /books` - Add a new book to the library (admin only)
   - `GET /users/{id}/borrowed` - Get list of books borrowed by a user
   - `POST /borrow` - Borrow a book (needs book ID and user ID)
   - `POST /return` - Return a borrowed book
   - `GET /users/{id}` - Get user information

3. **Use Cases**:
   - A school can integrate this into their student portal
   - A mobile app can be built for library members to browse and reserve books
   - An analytics dashboard can track which books are most popular

4. **Security**:
   - User authentication required for borrowing books
   - Admin authentication for adding/removing books
   - Personal information (addresses, contact details) should be encrypted
   - Only users can see their own borrowing history

5. **Data Format**: JSON (JavaScript Object Notation) - a text-based format that's easy to read and widely supported

---

**Great job completing Module 1! 🎉**

Next up: **[02-http-basics](../02-http-basics/)** - Learn how APIs actually communicate over the internet!
