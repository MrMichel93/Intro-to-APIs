# Working with JSON 📦

## Introduction

You've been working with JSON throughout this course, but now let's dive deep into understanding and mastering JSON - the most common data format for APIs!

**JSON** stands for **JavaScript Object Notation**. Despite the name, it's language-independent and used everywhere - not just JavaScript!

## What is JSON?

JSON is a lightweight data format for storing and exchanging data. It's:
- **Human-readable**: Easy to read and write
- **Machine-friendly**: Easy for programs to parse
- **Language-independent**: Works with any programming language
- **Text-based**: Just plain text, no special binary format

Think of JSON as a way to write data structures that both humans and computers can understand.

## JSON Syntax Rules

### Basic Structure

JSON is built from two structures:
1. **Objects**: Collections of key-value pairs (like dictionaries)
2. **Arrays**: Ordered lists of values

### Valid JSON Data Types

1. **Strings**: `"Hello"`, `"API"`
2. **Numbers**: `42`, `3.14`, `-10`
3. **Booleans**: `true`, `false`
4. **Null**: `null`
5. **Objects**: `{"key": "value"}`
6. **Arrays**: `[1, 2, 3]`

### Syntax Rules

```json
{
  "name": "John Doe",          // String
  "age": 25,                    // Number
  "isStudent": true,            // Boolean
  "grade": null,                // Null
  "courses": ["Math", "CS"],    // Array
  "address": {                  // Nested object
    "city": "Boston",
    "zip": "02101"
  }
}
```

**Important Rules:**
- Keys must be strings (in double quotes)
- Strings must use double quotes (not single)
- No trailing commas
- No comments in JSON (though we show them for explanation)

## JSON Examples

### Simple Object
```json
{
  "username": "student123",
  "email": "student@example.com",
  "verified": true
}
```

### Array of Objects
```json
[
  {
    "id": 1,
    "name": "Alice",
    "score": 95
  },
  {
    "id": 2,
    "name": "Bob",
    "score": 87
  }
]
```

### Nested Structure
```json
{
  "user": {
    "id": 123,
    "name": "Alice",
    "contact": {
      "email": "alice@example.com",
      "phone": "+1234567890"
    }
  },
  "posts": [
    {
      "id": 1,
      "title": "First Post",
      "tags": ["intro", "hello"]
    },
    {
      "id": 2,
      "title": "Second Post",
      "tags": ["update"]
    }
  ]
}
```

## Working with JSON in Python

### Parsing JSON (String to Object)

```python
import json

# JSON string
json_string = '{"name": "Alice", "age": 20, "courses": ["Math", "CS"]}'

# Parse JSON string to Python dict
data = json.loads(json_string)

print(data['name'])        # Output: Alice
print(data['age'])         # Output: 20
print(data['courses'][0])  # Output: Math
```

### Creating JSON (Object to String)

```python
import json

# Python dictionary
user = {
    "name": "Bob",
    "age": 22,
    "enrolled": True,
    "courses": ["Physics", "Math"]
}

# Convert to JSON string
json_string = json.dumps(user)
print(json_string)
# Output: {"name": "Bob", "age": 22, "enrolled": true, "courses": ["Physics", "Math"]}

# Pretty print with indentation
json_string = json.dumps(user, indent=2)
print(json_string)
# Output (formatted):
# {
#   "name": "Bob",
#   "age": 22,
#   "enrolled": true,
#   "courses": ["Physics", "Math"]
# }
```

### Reading JSON from File

```python
import json

# Read JSON file
with open('data.json', 'r') as file:
    data = json.load(file)  # Note: load, not loads
    
print(data)
```

### Writing JSON to File

```python
import json

data = {
    "users": [
        {"name": "Alice", "age": 20},
        {"name": "Bob", "age": 22}
    ]
}

# Write to file
with open('output.json', 'w') as file:
    json.dump(data, file, indent=2)  # Note: dump, not dumps
```

### Working with API Responses

```python
import requests
import json

# Fetch data from API
response = requests.get('https://api.github.com/users/octocat')

# Parse JSON response
user_data = response.json()  # Automatically parses JSON

# Access data
print(f"Name: {user_data['name']}")
print(f"Public repos: {user_data['public_repos']}")

# Or manually parse
json_string = response.text
user_data = json.loads(json_string)
```

## Working with JSON in JavaScript

### Parsing JSON (String to Object)

```javascript
// JSON string
const jsonString = '{"name": "Alice", "age": 20, "courses": ["Math", "CS"]}';

// Parse JSON string to JavaScript object
const data = JSON.parse(jsonString);

console.log(data.name);        // Output: Alice
console.log(data.age);         // Output: 20
console.log(data.courses[0]);  // Output: Math
```

### Creating JSON (Object to String)

```javascript
// JavaScript object
const user = {
  name: "Bob",
  age: 22,
  enrolled: true,
  courses: ["Physics", "Math"]
};

// Convert to JSON string
const jsonString = JSON.stringify(user);
console.log(jsonString);

// Pretty print with indentation
const prettyJson = JSON.stringify(user, null, 2);
console.log(prettyJson);
```

### Working with API Responses

```javascript
// Using fetch
fetch('https://api.github.com/users/octocat')
  .then(response => response.json())  // Automatically parses JSON
  .then(data => {
    console.log(`Name: ${data.name}`);
    console.log(`Public repos: ${data.public_repos}`);
  });

// Using async/await
async function fetchUser() {
  const response = await fetch('https://api.github.com/users/octocat');
  const data = await response.json();
  
  console.log(data.name);
}
```

## Accessing Nested JSON Data

### Example Data

```json
{
  "user": {
    "id": 123,
    "name": "Alice",
    "address": {
      "street": "123 Main St",
      "city": "Boston",
      "coordinates": {
        "lat": 42.3601,
        "lon": -71.0589
      }
    },
    "friends": [
      {"id": 2, "name": "Bob"},
      {"id": 3, "name": "Charlie"}
    ]
  }
}
```

### Accessing in Python

```python
import json

data = json.loads(json_string)

# Access nested values
user_name = data['user']['name']
city = data['user']['address']['city']
latitude = data['user']['address']['coordinates']['lat']
first_friend = data['user']['friends'][0]['name']

print(f"Name: {user_name}")
print(f"City: {city}")
print(f"Latitude: {latitude}")
print(f"First friend: {first_friend}")

# Safe access with .get() to avoid KeyError
email = data['user'].get('email', 'No email provided')
```

### Accessing in JavaScript

```javascript
const data = JSON.parse(jsonString);

// Access nested values
const userName = data.user.name;
const city = data.user.address.city;
const latitude = data.user.address.coordinates.lat;
const firstFriend = data.user.friends[0].name;

console.log(`Name: ${userName}`);
console.log(`City: ${city}`);
console.log(`Latitude: ${latitude}`);
console.log(`First friend: ${firstFriend}`);

// Safe access with optional chaining
const email = data.user?.email ?? 'No email provided';
```

## Handling Complex JSON

### Iterating Over Arrays

```python
# Python
json_data = '''
{
  "students": [
    {"name": "Alice", "grade": 95},
    {"name": "Bob", "grade": 87},
    {"name": "Charlie", "grade": 92}
  ]
}
'''

data = json.loads(json_data)

for student in data['students']:
    print(f"{student['name']}: {student['grade']}")

# Output:
# Alice: 95
# Bob: 87
# Charlie: 92
```

```javascript
// JavaScript
const data = JSON.parse(jsonData);

data.students.forEach(student => {
  console.log(`${student.name}: ${student.grade}`);
});
```

### Filtering Data

```python
# Python
# Get students with grade > 90
high_achievers = [
    student for student in data['students']
    if student['grade'] > 90
]
```

```javascript
// JavaScript
// Get students with grade > 90
const highAchievers = data.students.filter(student => student.grade > 90);
```

### Transforming Data

```python
# Python
# Extract just the names
names = [student['name'] for student in data['students']]
```

```javascript
// JavaScript
// Extract just the names
const names = data.students.map(student => student.name);
```

## Common JSON Patterns in APIs

### Pagination Response

```json
{
  "data": [
    {"id": 1, "title": "Post 1"},
    {"id": 2, "title": "Post 2"}
  ],
  "pagination": {
    "page": 1,
    "per_page": 10,
    "total": 100,
    "total_pages": 10
  }
}
```

### Error Response

```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "The request was invalid",
    "details": [
      {
        "field": "email",
        "message": "Email is required"
      }
    ]
  }
}
```

### Metadata Response

```json
{
  "data": {
    "user": {
      "id": 123,
      "name": "Alice"
    }
  },
  "meta": {
    "request_id": "abc-123",
    "timestamp": "2024-12-16T10:00:00Z",
    "version": "1.0"
  }
}
```

## JSON Validation

### Valid JSON

```json
{
  "name": "Alice",
  "age": 20,
  "courses": ["Math", "CS"]
}
```

### Invalid JSON (Common Mistakes)

```json
// ❌ Single quotes instead of double quotes
{'name': 'Alice'}

// ❌ Trailing comma
{
  "name": "Alice",
  "age": 20,
}

// ❌ Comments (not allowed in JSON)
{
  "name": "Alice",  // This is a comment
  "age": 20
}

// ❌ Unquoted keys
{
  name: "Alice",
  age: 20
}
```

## Handling JSON Errors

### Python Error Handling

```python
import json

def safe_json_parse(json_string):
    """Safely parse JSON with error handling"""
    try:
        data = json.loads(json_string)
        return data, None
    except json.JSONDecodeError as e:
        return None, f"JSON parsing error: {e}"

# Usage
json_string = '{"name": "Alice", "age": 20}'
data, error = safe_json_parse(json_string)

if error:
    print(f"Error: {error}")
else:
    print(f"Success: {data}")
```

### JavaScript Error Handling

```javascript
function safeJsonParse(jsonString) {
  try {
    const data = JSON.parse(jsonString);
    return { data, error: null };
  } catch (e) {
    return { data: null, error: `JSON parsing error: ${e.message}` };
  }
}

// Usage
const jsonString = '{"name": "Alice", "age": 20}';
const { data, error } = safeJsonParse(jsonString);

if (error) {
  console.log(`Error: ${error}`);
} else {
  console.log(`Success: ${data}`);
}
```

## Best Practices

### 1. **Always Validate JSON**
```python
# Check if response is valid JSON
try:
    data = response.json()
except json.JSONDecodeError:
    print("Invalid JSON response")
```

### 2. **Use Safe Access Methods**
```python
# Python - use .get() with defaults
email = user.get('email', 'no-email@example.com')

# JavaScript - use optional chaining
const email = user?.email ?? 'no-email@example.com';
```

### 3. **Pretty Print for Debugging**
```python
# Python
print(json.dumps(data, indent=2))

# JavaScript
console.log(JSON.stringify(data, null, 2));
```

### 4. **Handle Nested Structures Carefully**
```python
# Check if keys exist before accessing
if 'user' in data and 'address' in data['user']:
    city = data['user']['address']['city']
```

### 5. **Type Check Values**
```python
# Verify data types
if isinstance(data.get('age'), int):
    age = data['age']
else:
    age = 0  # Default value
```

## JSON Schema (Advanced)

JSON Schema is a way to describe what valid JSON should look like:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "age": {
      "type": "integer",
      "minimum": 0
    },
    "email": {
      "type": "string",
      "format": "email"
    }
  },
  "required": ["name", "email"]
}
```

## Real-World Example

```python
import requests
import json

def fetch_and_process_github_user(username):
    """Fetch GitHub user and process JSON data"""
    url = f"https://api.github.com/users/{username}"
    
    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()
        
        # Parse JSON
        user = response.json()
        
        # Extract and process data
        processed_data = {
            'username': user.get('login', 'Unknown'),
            'name': user.get('name', 'No name provided'),
            'public_repos': user.get('public_repos', 0),
            'followers': user.get('followers', 0),
            'created_at': user.get('created_at', 'Unknown'),
            'has_bio': bool(user.get('bio'))
        }
        
        # Save to file
        output_file = f"{username}_data.json"
        with open(output_file, 'w') as f:
            json.dump(processed_data, f, indent=2)
        
        print(f"Data saved to {output_file}")
        return processed_data
        
    except requests.exceptions.RequestException as e:
        print(f"Error fetching data: {e}")
        return None
    except json.JSONDecodeError as e:
        print(f"Error parsing JSON: {e}")
        return None

# Usage
data = fetch_and_process_github_user('octocat')
if data:
    print(f"User has {data['public_repos']} public repositories")
```

## What's Next?

Congratulations! You've completed the Introduction to APIs course! 🎉

You now know:
- What APIs are and why they matter
- HTTP protocol and REST principles
- How to make API requests
- API authentication methods
- How to work with JSON data

**Next steps:**
- Build your own API projects
- Explore more advanced topics (GraphQL, WebSockets, gRPC)
- Contribute to open source projects that use APIs
- Keep practicing with different APIs!

---

## 📝 Practice Problems

### Problem 1: JSON Parser and Validator (Easy)
**File**: `problem1.md` and `problem1.py` or `problem1.js`

Build a JSON utility tool that can:
1. Parse JSON strings and display them nicely
2. Validate JSON syntax
3. Pretty print JSON
4. Convert between JSON and Python dict/JavaScript object

Test with various JSON strings including invalid ones.

### Problem 2: JSON Data Transformer (Medium)
**File**: `problem2.md` and `problem2.py` or `problem2.js`

Build a tool that transforms JSON data from one structure to another.

**Example:**
Transform API response format to database format, or vice versa.

**Requirements:**
- Read JSON from file or API
- Transform structure based on mapping rules
- Validate transformed output
- Handle nested objects and arrays
- Save transformed JSON

### Problem 3: API Response Analyzer (Hard)
**File**: `problem3.md` and `problem3.py` or `problem3.js`

Build a comprehensive tool that analyzes JSON responses from multiple APIs.

**Features:**
- Fetch data from multiple APIs
- Analyze JSON structure (depth, types, missing fields)
- Compare responses from different APIs
- Generate JSON schema from responses
- Find anomalies or inconsistencies
- Create summary reports
- Visualize data structure

---

## 🎯 Solutions

See the problem files for complete solutions and examples!

---

**Congratulations on completing all the modules! 🎓**

You now have a solid foundation in APIs. Ready to put your knowledge into practice?

**Next Steps:**
- Check out the [Projects](../../projects/) folder for hands-on projects
- Start with [Project 1: Weather Dashboard](../../projects/01-weather-dashboard/)
- Build real applications that use APIs!

---

[← Back to Modules](../README.md) | [Projects →](../../projects/)
