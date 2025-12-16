# Problem 1: API Key Authentication (Easy)

## Instructions

Practice using API key authentication with the OpenWeatherMap API.

**API Documentation**: https://openweathermap.org/api

---

## Setup

### Step 1: Get Your API Key

1. Go to: https://openweathermap.org/api
2. Sign up for a free account
3. Navigate to "API keys" section
4. Copy your API key

**Note:** It may take a few minutes for the API key to activate.

---

### Step 2: Set Up Environment Variables

Create a `.env` file in your project directory:

```
OPENWEATHER_API_KEY=your_actual_api_key_here
```

**IMPORTANT:** Add `.env` to your `.gitignore` file!

---

## Requirements

Build a weather information tool with these features:

1. **Fetch weather data** for a given city
2. **Display** the following information:
   - City name
   - Temperature (in Celsius)
   - "Feels like" temperature
   - Weather description
   - Humidity percentage
   - Wind speed

3. **Error handling** for:
   - Invalid API key (401)
   - City not found (404)
   - Network errors
   - Missing environment variable

4. **Test with multiple cities**

---

## Your Code

### Python Template

```python
import requests
import os
from dotenv import load_dotenv

# Load environment variables
load_dotenv()

def get_weather(city):
    """
    Fetch weather data for a city
    
    Args:
        city (str): Name of the city
        
    Returns:
        dict: Weather information or None if error
    """
    # TODO: Get API key from environment variable
    
    # TODO: Build API request URL and parameters
    
    # TODO: Make the API request
    
    # TODO: Handle different status codes
    
    # TODO: Parse and return the data
    
    pass

def display_weather(weather_info):
    """Display weather information in a nice format"""
    # TODO: Format and print the weather data
    pass

def main():
    """Main function"""
    test_cities = ['London', 'New York', 'Tokyo', 'InvalidCity']
    
    # TODO: Test with each city
    pass

if __name__ == "__main__":
    main()
```

### JavaScript Template

```javascript
require('dotenv').config();
const fetch = require('node-fetch'); // or use built-in fetch

async function getWeather(city) {
  /**
   * Fetch weather data for a city
   * 
   * @param {string} city - Name of the city
   * @returns {Object|null} Weather information or null if error
   */
  // TODO: Get API key from environment variable
  
  // TODO: Build API request URL and parameters
  
  // TODO: Make the API request
  
  // TODO: Handle different status codes
  
  // TODO: Parse and return the data
}

function displayWeather(weatherInfo) {
  // TODO: Format and print the weather data
}

async function main() {
  const testCities = ['London', 'New York', 'Tokyo', 'InvalidCity'];
  
  // TODO: Test with each city
}

main();
```

---

## Expected Output

```
==================================================
Weather in London
==================================================
Temperature: 12.5°C
Feels like: 11.2°C
Conditions: Partly cloudy
Humidity: 72%
Wind Speed: 3.5 m/s

==================================================
Weather in New York
==================================================
Temperature: 8.3°C
Feels like: 6.1°C
Conditions: Clear sky
Humidity: 65%
Wind Speed: 4.2 m/s

==================================================
Weather in Tokyo
==================================================
Temperature: 15.7°C
Feels like: 14.9°C
Conditions: Light rain
Humidity: 80%
Wind Speed: 2.8 m/s

Error: City 'InvalidCity' not found
```

---

## Testing Checklist

- [ ] API key loaded from environment variable
- [ ] Successfully fetches weather data
- [ ] Displays all required information
- [ ] Handles invalid API key (401)
- [ ] Handles city not found (404)
- [ ] Handles network errors gracefully
- [ ] Tests with multiple cities
- [ ] Code is well-organized and commented
- [ ] .env file NOT committed to git

---

## Part 2: Enhancements

Choose at least **2** enhancements to implement:

### Enhancement 1: Multiple Units
```
Allow user to choose temperature units: Celsius, Fahrenheit, or Kelvin
API supports: units=metric (Celsius), units=imperial (Fahrenheit), units=standard (Kelvin)
```

**Your Code:**
```python
# Your code here






```

---

### Enhancement 2: 5-Day Forecast
```
Fetch and display 5-day weather forecast
API endpoint: https://api.openweathermap.org/data/2.5/forecast
```

**Your Code:**
```python
# Your code here






```

---

### Enhancement 3: Weather Alerts
```
Check for severe weather warnings
Display any weather alerts for the location
```

**Your Code:**
```python
# Your code here






```

---

### Enhancement 4: Save to File
```
Save weather data to a JSON file with timestamp
Useful for tracking weather history
```

**Your Code:**
```python
# Your code here






```

---

## Reflection Questions

1. **Why is it important to use environment variables for API keys?**
```



```

2. **What could happen if you accidentally commit your API key to GitHub?**
```



```

3. **How would you handle an expired or invalid API key in a production application?**
```



```

4. **What are the advantages of using the OpenWeatherMap API over scraping weather data from websites?**
```



```

---

## Bonus Challenge

### Weather Comparison Tool

Create a tool that compares weather between multiple cities and finds:
- Warmest city
- Coldest city
- Most humid city
- Windiest city

**Your Code:**
```python
# Your code here













```

---

**Great job learning API key authentication! 🎉**

**Check the main README for solution code!**
