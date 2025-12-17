# Problem 3: API Response Analyzer (Hard)

## Instructions

Build a comprehensive tool that analyzes JSON responses from multiple APIs.

This tool will help you understand API response structures, find inconsistencies, and generate documentation.

---

## Core Features

Your analyzer should:

1. **Fetch data from multiple APIs**
2. **Analyze JSON structure**:
   - Maximum nesting depth
   - Field types
   - Missing or null fields
   - Array lengths
3. **Compare responses** from different APIs
4. **Generate JSON schema** from responses
5. **Find anomalies** or inconsistencies
6. **Create summary reports**
7. **Visualize data structure** (text-based tree)

---

## Your Code

### Python Template

```python
import requests
import json
from typing import Dict, Any, List, Set
from collections import defaultdict
from datetime import datetime

class JSONAnalyzer:
    """Analyze JSON structures from APIs"""
    
    def __init__(self):
        self.analyses = []
    
    def fetch_and_analyze(self, url, name=None):
        """
        Fetch JSON from URL and analyze it
        
        Args:
            url: API endpoint URL
            name: Optional name for this API
            
        Returns:
            dict: Analysis results
        """
        try:
            response = requests.get(url, timeout=10)
            response.raise_for_status()
            data = response.json()
            
            analysis = {
                'name': name or url,
                'url': url,
                'timestamp': datetime.now().isoformat(),
                'data': data,
                'structure': self.analyze_structure(data),
                'statistics': self.calculate_statistics(data)
            }
            
            self.analyses.append(analysis)
            return analysis
            
        except Exception as e:
            return {'error': str(e)}
    
    def analyze_structure(self, data, path='root'):
        """
        Analyze the structure of JSON data
        
        Returns:
            dict: Structure information
        """
        # TODO: Implement structure analysis
        # Should return:
        # - type of data (object, array, string, etc.)
        # - for objects: keys and types
        # - for arrays: length and item types
        # - nesting depth
        pass
    
    def calculate_depth(self, data, current_depth=0):
        """
        Calculate maximum nesting depth
        
        Args:
            data: JSON data
            current_depth: Current depth level
            
        Returns:
            int: Maximum depth
        """
        # TODO: Implement depth calculation
        pass
    
    def get_field_types(self, data, prefix=''):
        """
        Get all field paths and their types
        
        Args:
            data: JSON data
            prefix: Current path prefix
            
        Returns:
            dict: Field paths to types mapping
        """
        # TODO: Implement field type extraction
        # Example output:
        # {
        #   "user.name": "string",
        #   "user.age": "integer",
        #   "user.addresses": "array"
        # }
        pass
    
    def calculate_statistics(self, data):
        """
        Calculate statistics about the data
        
        Returns:
            dict: Statistics
        """
        stats = {
            'total_fields': 0,
            'null_fields': 0,
            'empty_arrays': 0,
            'max_array_length': 0,
            'field_types': {},
            'max_depth': 0
        }
        
        # TODO: Implement statistics calculation
        
        return stats
    
    def find_missing_fields(self, data, expected_fields):
        """
        Find fields that are expected but missing
        
        Args:
            data: JSON data
            expected_fields: List of expected field paths
            
        Returns:
            list: Missing field paths
        """
        # TODO: Implement missing field detection
        pass
    
    def generate_schema(self, data):
        """
        Generate JSON Schema from data
        
        Returns:
            dict: JSON Schema
        """
        # TODO: Implement schema generation
        # Should create a JSON Schema that describes the data structure
        pass
    
    def visualize_structure(self, data, indent=0):
        """
        Create a text-based tree visualization
        
        Args:
            data: JSON data
            indent: Current indentation level
            
        Returns:
            str: Tree visualization
        """
        # TODO: Implement tree visualization
        # Example output:
        # root (object)
        #   ├─ user (object)
        #   │  ├─ name (string)
        #   │  └─ age (integer)
        #   └─ posts (array, length: 3)
        pass
    
    def compare_analyses(self, analysis1, analysis2):
        """
        Compare two analyses
        
        Returns:
            dict: Comparison results
        """
        # TODO: Implement comparison
        # Should compare:
        # - Field differences
        # - Type differences
        # - Structure differences
        pass
    
    def find_anomalies(self, data):
        """
        Find potential issues or anomalies
        
        Returns:
            list: List of anomalies found
        """
        anomalies = []
        
        # TODO: Detect anomalies like:
        # - Very deep nesting (> 5 levels)
        # - Very long arrays (> 100 items)
        # - Null values in critical fields
        # - Inconsistent data types
        # - Empty objects or arrays
        
        return anomalies
    
    def generate_report(self, analysis):
        """
        Generate a comprehensive report
        
        Returns:
            str: Formatted report
        """
        # TODO: Create formatted report with all analysis results
        pass

class APIComparator:
    """Compare responses from multiple APIs"""
    
    def __init__(self):
        self.analyzer = JSONAnalyzer()
    
    def compare_endpoints(self, endpoints):
        """
        Fetch and compare multiple endpoints
        
        Args:
            endpoints: List of (name, url) tuples
            
        Returns:
            dict: Comparison results
        """
        # TODO: Implement multi-endpoint comparison
        pass
    
    def find_common_fields(self, analyses):
        """Find fields that appear in all responses"""
        # TODO: Implement
        pass
    
    def find_unique_fields(self, analyses):
        """Find fields unique to each response"""
        # TODO: Implement
        pass

def main():
    """Main function with examples"""
    analyzer = JSONAnalyzer()
    
    # Example APIs to analyze
    apis = [
        ("GitHub User", "https://api.github.com/users/octocat"),
        ("JSONPlaceholder User", "https://jsonplaceholder.typicode.com/users/1"),
        ("PokeAPI", "https://pokeapi.co/api/v2/pokemon/pikachu"),
    ]
    
    print("API Response Analyzer")
    print("=" * 70)
    print()
    
    for name, url in apis:
        print(f"Analyzing: {name}")
        print("-" * 70)
        
        analysis = analyzer.fetch_and_analyze(url, name)
        
        if 'error' in analysis:
            print(f"Error: {analysis['error']}")
        else:
            report = analyzer.generate_report(analysis)
            print(report)
        
        print()

if __name__ == "__main__":
    main()
```

---

## Expected Output Example

```
API Response Analyzer
======================================================================

Analyzing: GitHub User
----------------------------------------------------------------------
Name: GitHub User
URL: https://api.github.com/users/octocat
Analyzed at: 2024-12-16T14:30:00

Structure Analysis:
  Type: object
  Top-level fields: 30
  Max nesting depth: 3
  
Field Types:
  login: string
  id: integer
  avatar_url: string
  type: string
  name: string
  company: string (nullable)
  blog: string
  public_repos: integer
  followers: integer
  following: integer
  created_at: string (datetime)

Statistics:
  Total fields: 30
  Null fields: 2 (company, bio)
  Arrays: 0
  Objects: 1
  Strings: 18
  Integers: 7
  Booleans: 1
  
Anomalies:
  ✓ No anomalies detected

Schema:
  {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "login": {"type": "string"},
      "id": {"type": "integer"},
      ...
    }
  }

Structure Tree:
root (object)
├─ login (string)
├─ id (integer)
├─ avatar_url (string)
├─ type (string)
└─ ...

======================================================================
```

---

## Advanced Features

### Feature 1: Response Time Analysis
```python
def analyze_performance(self, url, iterations=5):
    """
    Analyze API response times
    
    Returns:
        dict: Performance metrics (avg, min, max, std dev)
    """
    # TODO: Implement performance analysis
    pass
```

### Feature 2: Data Quality Score
```python
def calculate_quality_score(self, data):
    """
    Calculate a quality score based on:
    - Completeness (no null values)
    - Consistency (uniform types)
    - Structure (reasonable depth)
    - Documentation (descriptive field names)
    
    Returns:
        float: Quality score (0-100)
    """
    # TODO: Implement quality scoring
    pass
```

### Feature 3: Historical Comparison
```python
def track_changes(self, url, interval_minutes=60):
    """
    Fetch API periodically and track changes
    
    Returns:
        list: Change history
    """
    # TODO: Implement change tracking
    pass
```

### Feature 4: Export Reports
```python
def export_report(self, analysis, format='markdown'):
    """
    Export report in various formats
    
    Supported formats: markdown, html, pdf, json
    """
    # TODO: Implement report export
    pass
```

---

## Test APIs

Use these APIs for testing:

1. **GitHub API**
   - User: `https://api.github.com/users/octocat`
   - Repos: `https://api.github.com/users/octocat/repos`

2. **JSONPlaceholder**
   - Users: `https://jsonplaceholder.typicode.com/users`
   - Posts: `https://jsonplaceholder.typicode.com/posts`

3. **PokeAPI**
   - Pokemon: `https://pokeapi.co/api/v2/pokemon/pikachu`
   - Ability: `https://pokeapi.co/api/v2/ability/1`

4. **REST Countries**
   - All countries: `https://restcountries.com/v3.1/all`
   - Specific: `https://restcountries.com/v3.1/name/canada`

---

## Use Cases

### Use Case 1: API Documentation Generator
```
Automatically generate API documentation by analyzing responses
```

### Use Case 2: API Testing Tool
```
Compare expected vs actual response structures in tests
```

### Use Case 3: Data Migration Planner
```
Analyze source and target API structures to plan data migration
```

### Use Case 4: API Monitoring
```
Track API response structure changes over time
```

---

## Bonus Challenges

### Challenge 1: Diff Tool
```python
def generate_diff(self, analysis1, analysis2):
    """
    Generate a detailed diff between two analyses
    Show added, removed, and changed fields
    """
    # TODO: Implement
    pass
```

### Challenge 2: GraphQL Support
```python
def analyze_graphql_response(self, response):
    """
    Analyze GraphQL response structure
    Handle fragments, inline fragments, etc.
    """
    # TODO: Implement
    pass
```

### Challenge 3: Web Dashboard
```python
def create_web_dashboard(self):
    """
    Create an interactive web dashboard using Flask
    Display analyses with charts and graphs
    """
    # TODO: Implement
    pass
```

---

## Testing Checklist

- [ ] Fetches from multiple APIs successfully
- [ ] Analyzes simple JSON structures
- [ ] Analyzes complex nested structures
- [ ] Handles arrays correctly
- [ ] Calculates depth accurately
- [ ] Generates valid JSON Schema
- [ ] Creates readable tree visualization
- [ ] Finds anomalies
- [ ] Compares responses
- [ ] Generates comprehensive reports
- [ ] Handles errors gracefully
- [ ] Well-documented code
- [ ] Comprehensive test coverage

---

## Reflection Questions

1. **What patterns did you notice across different APIs?**
```



```

2. **What makes a JSON response structure "good"?**
```



```

3. **How would you use this tool in a real project?**
```



```

4. **What additional features would be valuable?**
```



```

5. **How could machine learning enhance this analyzer?**
```



```

---

**Save your code as `problem3.py` or `problem3.js`**

**This is an advanced, portfolio-worthy project! 🌟**

**Congratulations on completing the entire Intro to APIs course! 🎓🎉**
