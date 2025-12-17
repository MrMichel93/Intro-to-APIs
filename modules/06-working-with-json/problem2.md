# Problem 2: JSON Data Transformer (Medium)

## Instructions

Build a tool that transforms JSON data from one structure to another.

This is a common task when integrating different APIs or systems that use different data formats.

---

## Scenario

You're building a system that needs to:
1. Fetch data from an external API (format A)
2. Transform it to your database format (format B)
3. Also support transforming from your format back to API format

---

## Example Transformation

### API Format (Input)
```json
{
  "user_data": {
    "id": "123",
    "full_name": "Alice Johnson",
    "email_address": "alice@example.com",
    "join_date": "2024-01-15T10:30:00Z",
    "user_settings": {
      "theme": "dark",
      "notifications_enabled": true
    }
  }
}
```

### Database Format (Output)
```json
{
  "id": 123,
  "name": "Alice Johnson",
  "email": "alice@example.com",
  "created_at": "2024-01-15T10:30:00Z",
  "settings": {
    "theme": "dark",
    "notifications": true
  }
}
```

---

## Requirements

Build a transformer that can:

1. **Define mapping rules** between formats
2. **Transform data** from format A to format B
3. **Reverse transform** from format B to format A
4. **Handle nested objects** and arrays
5. **Validate** transformed output
6. **Handle missing fields** gracefully
7. **Support type conversion** (string to int, etc.)

---

## Your Code

### Python Template

```python
import json
from datetime import datetime
from typing import Dict, Any, List

class JSONTransformer:
    """Transform JSON data between different formats"""
    
    def __init__(self):
        # Define transformation mappings
        self.api_to_db_mapping = {
            "user_data.id": ("id", int),  # (target_path, type_converter)
            "user_data.full_name": ("name", str),
            "user_data.email_address": ("email", str),
            "user_data.join_date": ("created_at", str),
            "user_data.user_settings.theme": ("settings.theme", str),
            "user_data.user_settings.notifications_enabled": ("settings.notifications", bool),
        }
        
        # Reverse mapping for db to api
        self.db_to_api_mapping = self._reverse_mapping(self.api_to_db_mapping)
    
    def _reverse_mapping(self, mapping):
        """Create reverse mapping"""
        # TODO: Implement reverse mapping
        pass
    
    def get_nested_value(self, data, path):
        """
        Get value from nested dict using dot notation path
        
        Args:
            data: Dictionary to search
            path: Dot-notated path (e.g., "user.address.city")
            
        Returns:
            Value at path or None
        """
        # TODO: Implement nested value retrieval
        # Example: get_nested_value({"a": {"b": {"c": 1}}}, "a.b.c") returns 1
        pass
    
    def set_nested_value(self, data, path, value):
        """
        Set value in nested dict using dot notation path
        
        Args:
            data: Dictionary to modify
            path: Dot-notated path
            value: Value to set
        """
        # TODO: Implement nested value setting
        # Example: set_nested_value({}, "a.b.c", 1) creates {"a": {"b": {"c": 1}}}
        pass
    
    def transform(self, data, mapping):
        """
        Transform data using a mapping
        
        Args:
            data: Source data dictionary
            mapping: Transformation mapping
            
        Returns:
            Transformed dictionary
        """
        # TODO: Implement transformation logic
        pass
    
    def api_to_db(self, api_data):
        """Transform from API format to database format"""
        return self.transform(api_data, self.api_to_db_mapping)
    
    def db_to_api(self, db_data):
        """Transform from database format to API format"""
        return self.transform(db_data, self.db_to_api_mapping)
    
    def transform_array(self, data_array, mapping):
        """Transform an array of objects"""
        # TODO: Transform each object in array
        pass
    
    def validate_transformed_data(self, data, required_fields):
        """
        Validate that transformed data has all required fields
        
        Args:
            data: Transformed data
            required_fields: List of required field paths
            
        Returns:
            tuple: (is_valid, missing_fields)
        """
        # TODO: Implement validation
        pass

def main():
    """Main function with examples"""
    transformer = JSONTransformer()
    
    # Example API data
    api_data = {
        "user_data": {
            "id": "123",
            "full_name": "Alice Johnson",
            "email_address": "alice@example.com",
            "join_date": "2024-01-15T10:30:00Z",
            "user_settings": {
                "theme": "dark",
                "notifications_enabled": True
            }
        }
    }
    
    # Transform to database format
    print("API Data:")
    print(json.dumps(api_data, indent=2))
    
    db_data = transformer.api_to_db(api_data)
    print("\nDatabase Format:")
    print(json.dumps(db_data, indent=2))
    
    # Transform back to API format
    api_data_back = transformer.db_to_api(db_data)
    print("\nTransformed Back to API Format:")
    print(json.dumps(api_data_back, indent=2))

if __name__ == "__main__":
    main()
```

---

## Test Cases

### Test Case 1: Single User
```json
{
  "user_data": {
    "id": "123",
    "full_name": "Alice Johnson",
    "email_address": "alice@example.com"
  }
}
```

Expected output:
```json
{
  "id": 123,
  "name": "Alice Johnson",
  "email": "alice@example.com"
}
```

---

### Test Case 2: Array of Users
```json
{
  "users": [
    {
      "user_data": {
        "id": "123",
        "full_name": "Alice Johnson"
      }
    },
    {
      "user_data": {
        "id": "456",
        "full_name": "Bob Smith"
      }
    }
  ]
}
```

---

### Test Case 3: Missing Optional Fields
```json
{
  "user_data": {
    "id": "123",
    "full_name": "Alice Johnson",
    "email_address": "alice@example.com"
    // Missing user_settings
  }
}
```

Expected: Should handle gracefully with defaults

---

## Advanced Requirements

### 1. Type Conversion
```python
def convert_type(value, target_type):
    """
    Convert value to target type
    
    Supported conversions:
    - string to int
    - string to float
    - string to datetime
    - bool to string
    - etc.
    """
    # TODO: Implement type conversion
    pass
```

### 2. Custom Transformation Functions
```python
def add_custom_transformer(self, field, transformer_func):
    """
    Add custom transformation function for a field
    
    Example:
        # Convert timestamp to human readable
        transformer.add_custom_transformer(
            "created_at",
            lambda x: datetime.fromisoformat(x).strftime("%B %d, %Y")
        )
    """
    # TODO: Implement custom transformers
    pass
```

### 3. Conditional Transformations
```python
def add_conditional_rule(self, condition, mapping):
    """
    Apply mapping only if condition is met
    
    Example:
        # Only transform admin users
        transformer.add_conditional_rule(
            lambda data: data.get("role") == "admin",
            special_admin_mapping
        )
    """
    # TODO: Implement conditional transformations
    pass
```

---

## Real-World Scenarios

### Scenario 1: E-commerce Order Transformation

Transform Shopify order format to your internal format:

**Shopify Format:**
```json
{
  "order": {
    "id": 12345,
    "line_items": [
      {
        "title": "Widget",
        "quantity": 2,
        "price": "19.99"
      }
    ],
    "customer": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "john@example.com"
    }
  }
}
```

**Your Format:**
```json
{
  "order_id": 12345,
  "items": [
    {
      "name": "Widget",
      "qty": 2,
      "price": 19.99
    }
  ],
  "customer_name": "John Doe",
  "customer_email": "john@example.com"
}
```

---

### Scenario 2: Social Media Post Transformation

Transform Instagram API response to unified social media format:

**Your Code:**
```python
# Define your transformation here
```

---

## Bonus Challenges

### Challenge 1: Configuration File
```
Load transformation mappings from a JSON config file
```

**Config File Example:**
```json
{
  "mappings": [
    {
      "source": "user_data.id",
      "target": "id",
      "type": "int"
    },
    {
      "source": "user_data.full_name",
      "target": "name",
      "type": "string"
    }
  ]
}
```

### Challenge 2: Bidirectional Sync
```
Track which format is "canonical" and sync changes bidirectionally
```

### Challenge 3: Transformation History
```
Keep a log of all transformations performed
```

---

## Testing Checklist

- [ ] Transforms simple objects correctly
- [ ] Handles nested objects
- [ ] Transforms arrays
- [ ] Converts types correctly
- [ ] Handles missing fields gracefully
- [ ] Validates transformed data
- [ ] Supports reverse transformation
- [ ] Custom transformers work
- [ ] Well-documented code
- [ ] Comprehensive test cases

---

## Reflection Questions

1. **Why is data transformation necessary when working with APIs?**
```


```

2. **What are the risks of data transformation?**
```


```

3. **How would you handle versioning of transformation rules?**
```


```

4. **What testing strategy would you use for transformations?**
```


```

---

**Save your code as `problem2.py` or `problem2.js`**

**This is a valuable real-world skill! 🎯**
