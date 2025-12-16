# Problem 1: JSON Parser and Validator (Easy)

## Instructions

Build a JSON utility tool that helps you work with JSON data.

---

## Requirements

Your tool should be able to:

1. **Parse JSON strings** and display them nicely
2. **Validate JSON syntax** and show errors
3. **Pretty print JSON** with proper indentation
4. **Minify JSON** (remove whitespace)
5. **Convert between formats**:
   - JSON string ↔ Python dict/JavaScript object
   - JSON file ↔ Python/JavaScript

---

## Your Code

### Python Template

```python
import json
import sys

class JSONUtility:
    """Utility for working with JSON data"""
    
    def parse_json(self, json_string):
        """
        Parse a JSON string
        
        Args:
            json_string (str): JSON string to parse
            
        Returns:
            tuple: (parsed_data, error_message)
        """
        try:
            data = json.loads(json_string)
            return data, None
        except json.JSONDecodeError as e:
            return None, f"JSON Parse Error: {e}"
    
    def validate_json(self, json_string):
        """
        Validate JSON syntax
        
        Args:
            json_string (str): JSON string to validate
            
        Returns:
            tuple: (is_valid, error_message)
        """
        # TODO: Implement validation
        # Return True and None if valid
        # Return False and error message if invalid
        pass
    
    def pretty_print(self, data, indent=2):
        """
        Pretty print JSON data
        
        Args:
            data: Python dict or list
            indent (int): Number of spaces for indentation
            
        Returns:
            str: Formatted JSON string
        """
        # TODO: Implement pretty printing
        pass
    
    def minify(self, json_string):
        """
        Minify JSON (remove all unnecessary whitespace)
        
        Args:
            json_string (str): JSON string to minify
            
        Returns:
            str: Minified JSON string
        """
        # TODO: Implement minification
        pass
    
    def json_to_file(self, data, filename):
        """
        Save data to JSON file
        
        Args:
            data: Python dict or list
            filename (str): Output filename
        """
        # TODO: Implement file writing
        pass
    
    def file_to_json(self, filename):
        """
        Read JSON from file
        
        Args:
            filename (str): Input filename
            
        Returns:
            tuple: (data, error_message)
        """
        # TODO: Implement file reading
        pass

def main():
    """Main function with interactive menu"""
    util = JSONUtility()
    
    print("JSON Utility Tool")
    print("=" * 50)
    print("1. Validate JSON")
    print("2. Pretty Print JSON")
    print("3. Minify JSON")
    print("4. Parse JSON file")
    print("5. Save JSON to file")
    print("6. Exit")
    print()
    
    # TODO: Implement interactive menu
    pass

if __name__ == "__main__":
    main()
```

### JavaScript Template

```javascript
class JSONUtility {
  /**
   * Parse a JSON string
   */
  parseJSON(jsonString) {
    try {
      const data = JSON.parse(jsonString);
      return { data, error: null };
    } catch (e) {
      return { data: null, error: `JSON Parse Error: ${e.message}` };
    }
  }
  
  /**
   * Validate JSON syntax
   */
  validateJSON(jsonString) {
    // TODO: Implement validation
  }
  
  /**
   * Pretty print JSON data
   */
  prettyPrint(data, indent = 2) {
    // TODO: Implement pretty printing
  }
  
  /**
   * Minify JSON
   */
  minify(jsonString) {
    // TODO: Implement minification
  }
}

function main() {
  const util = new JSONUtility();
  
  console.log("JSON Utility Tool");
  console.log("=".repeat(50));
  
  // TODO: Implement interactive menu
}

main();
```

---

## Test Cases

Test your utility with these JSON strings:

### Test 1: Valid Simple JSON
```json
{"name": "Alice", "age": 20, "courses": ["Math", "CS"]}
```

### Test 2: Valid Complex JSON
```json
{
  "user": {
    "id": 123,
    "name": "Bob",
    "address": {
      "city": "Boston",
      "zip": "02101"
    },
    "interests": ["coding", "music", "sports"]
  },
  "timestamp": "2024-12-16T10:00:00Z"
}
```

### Test 3: Invalid JSON - Single Quotes
```json
{'name': 'Alice'}
```

### Test 4: Invalid JSON - Trailing Comma
```json
{
  "name": "Alice",
  "age": 20,
}
```

### Test 5: Invalid JSON - Unquoted Keys
```json
{
  name: "Alice",
  age: 20
}
```

### Test 6: Invalid JSON - Unclosed Bracket
```json
{
  "name": "Alice",
  "age": 20
```

---

## Expected Output Examples

### Validation
```
Input: {"name": "Alice", "age": 20}
✓ Valid JSON

Input: {'name': 'Alice'}
✗ Invalid JSON
Error: Expecting property name enclosed in double quotes: line 1 column 2 (char 1)
```

### Pretty Print
```
Input: {"name":"Alice","age":20,"courses":["Math","CS"]}

Output:
{
  "name": "Alice",
  "age": 20,
  "courses": [
    "Math",
    "CS"
  ]
}
```

### Minify
```
Input:
{
  "name": "Alice",
  "age": 20
}

Output: {"name":"Alice","age":20}
```

---

## Testing Checklist

- [ ] Successfully parses valid JSON
- [ ] Identifies invalid JSON
- [ ] Shows helpful error messages
- [ ] Pretty prints with correct indentation
- [ ] Minifies JSON correctly
- [ ] Reads from files
- [ ] Writes to files
- [ ] Handles nested structures
- [ ] Handles arrays
- [ ] Handles special characters
- [ ] User-friendly interface

---

## Bonus Challenges

### Challenge 1: JSON Comparison
```python
def compare_json(json1, json2):
    """
    Compare two JSON structures and show differences
    
    Returns:
        list: List of differences
    """
    # TODO: Implement JSON comparison
    pass
```

### Challenge 2: JSON Flattening
```python
def flatten_json(nested_json):
    """
    Flatten nested JSON to single level with dot notation
    
    Example:
        {"user": {"name": "Alice"}} 
        becomes 
        {"user.name": "Alice"}
    """
    # TODO: Implement flattening
    pass
```

### Challenge 3: JSON Type Inspector
```python
def inspect_types(data):
    """
    Analyze and display data types in JSON structure
    
    Example output:
        name: string
        age: number
        courses: array of strings
        address: object
        address.city: string
    """
    # TODO: Implement type inspection
    pass
```

---

## Reflection Questions

1. **What's the difference between `json.loads()` and `json.load()` in Python?**
```


```

2. **Why is JSON more popular than XML for APIs?**
```


```

3. **How would you handle very large JSON files (gigabytes)?**
```


```

4. **What security considerations should you keep in mind when parsing JSON?**
```


```

---

**Save your code as `problem1.py` or `problem1.js`**

**Check the main README for solution approaches!**
