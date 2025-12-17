# Project 1: Weather Dashboard 🌤️

**Difficulty**: Beginner  
**Estimated Time**: 2-3 hours  
**Concepts Used**: API requests, JSON parsing, basic HTTP

## 📋 Project Overview

Build a simple weather dashboard that displays current weather information for any city using a free weather API. This project will help you practice making API requests and displaying data in a user-friendly format.

## 🎯 Learning Objectives

By completing this project, you will:
- Make your first real API request to a public API
- Parse JSON response data
- Handle API errors gracefully
- Work with API keys and authentication
- Display data in a meaningful way

## 🛠️ What You'll Build

A command-line or web-based application that:
1. Accepts a city name as input
2. Fetches current weather data from an API
3. Displays temperature, weather conditions, humidity, and wind speed
4. Handles errors (invalid city names, network issues)

## 📚 Prerequisites

Before starting this project, make sure you've completed:
- [Module 1: What Are APIs?](../../modules/01-what-are-apis/)
- [Module 2: HTTP Basics](../../modules/02-http-basics/)
- [Module 4: Making API Requests](../../modules/04-making-api-requests/)
- [Module 6: Working with JSON](../../modules/06-working-with-json/)

## 🚀 Getting Started

### Step 1: Choose Your Weather API

We recommend using **OpenWeatherMap API** (free tier available):

1. Go to [OpenWeatherMap](https://openweathermap.org/api)
2. Sign up for a free account
3. Get your API key from the dashboard
4. Read the [Current Weather Data API documentation](https://openweathermap.org/current)

**Alternative APIs** (if you prefer):
- [WeatherAPI.com](https://www.weatherapi.com/) - Free tier with 1M calls/month
- [Weather.gov API](https://www.weather.gov/documentation/services-web-api) - Free, US-only, no key needed

### Step 2: Understand the API Endpoint

For OpenWeatherMap, the endpoint looks like:
```
https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}&units=metric
```

**Parameters**:
- `q`: City name (e.g., "London", "New York")
- `appid`: Your API key
- `units`: Temperature units ("metric" for Celsius, "imperial" for Fahrenheit)

**Example Request**:
```
https://api.openweathermap.org/data/2.5/weather?q=London&appid=YOUR_API_KEY&units=metric
```

### Step 3: Test the API

Before coding, test the API using one of these methods:

**Option A: Using a Web Browser**
1. Copy the example URL above
2. Replace `YOUR_API_KEY` with your actual API key
3. Replace `London` with any city
4. Paste the URL in your browser
5. You should see JSON data

**Option B: Using curl (Command Line)**
```bash
curl "https://api.openweathermap.org/data/2.5/weather?q=London&appid=YOUR_API_KEY&units=metric"
```

**Option C: Using an API Testing Tool**
- [Postman](https://www.postman.com/)
- [Insomnia](https://insomnia.rest/)
- [HTTPie](https://httpie.io/)

### Step 4: Understand the Response

The API returns JSON data that looks like this:

```json
{
  "name": "London",
  "main": {
    "temp": 15.5,
    "feels_like": 14.2,
    "humidity": 72
  },
  "weather": [
    {
      "main": "Clouds",
      "description": "overcast clouds"
    }
  ],
  "wind": {
    "speed": 4.5
  }
}
```

**Key fields you'll use**:
- `name`: City name
- `main.temp`: Current temperature
- `main.humidity`: Humidity percentage
- `weather[0].description`: Weather description
- `wind.speed`: Wind speed

## 💻 Implementation Guide

### Choose Your Programming Language

Pick one of the following based on your comfort level:

#### Option 1: Python (Recommended for Beginners)

**Required Libraries**:
```bash
pip install requests
```

**Basic Structure**:
```python
import requests
import json

# Your API key
API_KEY = "your_api_key_here"
BASE_URL = "https://api.openweathermap.org/data/2.5/weather"

def get_weather(city):
    # Build the complete URL
    params = {
        "q": city,
        "appid": API_KEY,
        "units": "metric"
    }
    
    # Make the API request
    response = requests.get(BASE_URL, params=params)
    
    # Check if request was successful
    if response.status_code == 200:
        return response.json()
    else:
        return None

def display_weather(weather_data):
    # Extract and display the weather information
    # TODO: Implement this function
    pass

def main():
    city = input("Enter city name: ")
    weather = get_weather(city)
    
    if weather:
        display_weather(weather)
    else:
        print("Error: Could not fetch weather data")

if __name__ == "__main__":
    main()
```

#### Option 2: JavaScript (Node.js)

**Required Libraries**:
```bash
npm init -y
npm install node-fetch
```

**Basic Structure**:
```javascript
const fetch = require('node-fetch');

const API_KEY = 'your_api_key_here';
const BASE_URL = 'https://api.openweathermap.org/data/2.5/weather';

async function getWeather(city) {
    const url = `${BASE_URL}?q=${city}&appid=${API_KEY}&units=metric`;
    
    try {
        const response = await fetch(url);
        if (response.ok) {
            return await response.json();
        } else {
            return null;
        }
    } catch (error) {
        console.error('Error:', error);
        return null;
    }
}

function displayWeather(weatherData) {
    // Extract and display the weather information
    // TODO: Implement this function
}

async function main() {
    const readline = require('readline').createInterface({
        input: process.stdin,
        output: process.stdout
    });
    
    readline.question('Enter city name: ', async (city) => {
        const weather = await getWeather(city);
        
        if (weather) {
            displayWeather(weather);
        } else {
            console.log('Error: Could not fetch weather data');
        }
        
        readline.close();
    });
}

main();
```

#### Option 3: HTML/JavaScript (Web Version)

Create an `index.html` file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Dashboard</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
        }
        input, button {
            padding: 10px;
            margin: 5px;
            font-size: 16px;
        }
        #weather-display {
            margin-top: 20px;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <h1>🌤️ Weather Dashboard</h1>
    <div>
        <input type="text" id="cityInput" placeholder="Enter city name">
        <button onclick="getWeather()">Get Weather</button>
    </div>
    <div id="weather-display"></div>

    <script>
        const API_KEY = 'your_api_key_here';
        const BASE_URL = 'https://api.openweathermap.org/data/2.5/weather';

        async function getWeather() {
            const city = document.getElementById('cityInput').value;
            const url = `${BASE_URL}?q=${city}&appid=${API_KEY}&units=metric`;
            
            try {
                const response = await fetch(url);
                const data = await response.json();
                
                if (response.ok) {
                    displayWeather(data);
                } else {
                    document.getElementById('weather-display').innerHTML = 
                        `<p>Error: ${data.message}</p>`;
                }
            } catch (error) {
                document.getElementById('weather-display').innerHTML = 
                    `<p>Error: Could not fetch weather data</p>`;
            }
        }

        function displayWeather(data) {
            // TODO: Format and display the weather data nicely
            const display = document.getElementById('weather-display');
            display.innerHTML = `
                <h2>${data.name}</h2>
                <p>Temperature: ${data.main.temp}°C</p>
                <p>Weather: ${data.weather[0].description}</p>
                <p>Humidity: ${data.main.humidity}%</p>
                <p>Wind Speed: ${data.wind.speed} m/s</p>
            `;
        }
    </script>
</body>
</html>
```

## ✅ Requirements Checklist

Your weather dashboard should:

- [ ] Accept user input for city name
- [ ] Make an API request to a weather service
- [ ] Display the following information:
  - [ ] City name
  - [ ] Current temperature
  - [ ] Weather description (e.g., "partly cloudy")
  - [ ] Humidity percentage
  - [ ] Wind speed
- [ ] Handle errors gracefully:
  - [ ] Invalid city names
  - [ ] Network errors
  - [ ] Invalid API key
- [ ] Format the output in a readable way

## 🎨 Bonus Challenges

Once you've completed the basic requirements, try these enhancements:

1. **Add More Data** (Easy)
   - Display "feels like" temperature
   - Show sunrise and sunset times
   - Add pressure information

2. **Multiple Cities** (Medium)
   - Allow users to check weather for multiple cities
   - Save favorite cities
   - Compare weather between cities

3. **5-Day Forecast** (Medium)
   - Use the forecast endpoint instead of current weather
   - Display weather for the next 5 days
   - Show high and low temperatures

4. **Visual Enhancements** (Medium)
   - Add weather icons based on conditions
   - Use colors to indicate temperature (blue for cold, red for hot)
   - Add a background image that changes based on weather

5. **Geolocation** (Hard)
   - Automatically detect user's location
   - Show weather for current location by default
   - Add a map showing the city location

6. **Historical Data** (Hard)
   - Store previous weather queries
   - Show weather trends over time
   - Create simple charts/graphs

## 🐛 Common Issues and Solutions

### Issue: "Invalid API Key" Error
**Solution**: 
- Check that you've activated your API key in OpenWeatherMap
- New API keys can take a few hours to activate
- Make sure you copied the entire key correctly

### Issue: "City Not Found" Error
**Solution**:
- Check spelling of city name
- Try using city name with country code: "London,UK"
- Use city ID instead of name (see OpenWeatherMap docs)

### Issue: CORS Error (Web Version Only)
**Solution**:
- This happens when testing locally with file:// protocol
- Run a local server: `python -m http.server` (Python 3)
- Or use a proper hosting service

### Issue: Request Returns HTML Instead of JSON
**Solution**:
- Check your API endpoint URL
- Verify you're using the correct API version
- Make sure you're accessing the API endpoint, not the website

## 📖 Learning Resources

- [OpenWeatherMap API Documentation](https://openweathermap.org/api)
- [Understanding JSON](../../modules/06-working-with-json/)
- [HTTP Status Codes Explained](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [Python Requests Library](https://requests.readthedocs.io/)
- [JavaScript Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

## 🎯 Success Criteria

You've successfully completed this project when:
1. Your application runs without errors
2. It correctly fetches and displays weather data
3. It handles errors appropriately
4. The output is easy to read and understand
5. You can explain how the API request works

## 🤔 Reflection Questions

After completing this project, consider:

1. What was the most challenging part of this project?
2. How does the API make this application more powerful than if you stored weather data locally?
3. What would happen if the weather API went down?
4. How could you improve the user experience?
5. What other APIs could you integrate with this weather app?

## 📤 Share Your Work

Once you've completed the project:
- Take screenshots of your working application
- Document any challenges you faced
- Share your code with others learning APIs
- Consider adding your project to GitHub

---

**Need Help?** 
- Review the [modules](../../modules/) for concept refreshers
- Check the API documentation carefully
- Test your API requests in a browser or Postman first
- Debug step-by-step: verify the API call works before adding features

**Ready for more?** Check out [Project 2: GitHub Profile Viewer](../02-github-profile-viewer/) →

---

[← Back to Projects](../README.md) | [Main README](../../README.md)
