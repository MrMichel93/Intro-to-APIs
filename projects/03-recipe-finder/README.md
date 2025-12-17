# Project 3: Recipe Finder App 🍳

**Difficulty**: Intermediate  
**Estimated Time**: 4-6 hours  
**Concepts Used**: Multiple API endpoints, Query parameters, Data filtering, State management

## 📋 Project Overview

Build a recipe finder application that lets users search for recipes by ingredients, dietary restrictions, or cuisine type. This project combines multiple API calls, complex data filtering, and state management to create a practical, real-world application.

## 🎯 Learning Objectives

By completing this project, you will:
- Work with complex API query parameters
- Handle and filter large datasets
- Manage application state across multiple API calls
- Implement search functionality
- Work with nested JSON data structures
- Handle optional parameters and filtering

## 🛠️ What You'll Build

An application that:
1. Searches for recipes by ingredients or name
2. Filters recipes by dietary restrictions (vegetarian, vegan, gluten-free)
3. Displays recipe details including ingredients and instructions
4. Shows nutritional information
5. Allows users to save favorite recipes (locally)
6. Handles missing or incomplete recipe data

## 📚 Prerequisites

Before starting this project, make sure you've completed:
- All modules in [modules/](../../modules/)
- [Project 1: Weather Dashboard](../01-weather-dashboard/)
- [Project 2: GitHub Profile Viewer](../02-github-profile-viewer/)

## 🚀 Getting Started

### Step 1: Choose a Recipe API

We recommend **Spoonacular API** (free tier: 150 requests/day):

1. Go to [Spoonacular API](https://spoonacular.com/food-api)
2. Sign up for a free account
3. Get your API key from the dashboard
4. Explore the [API documentation](https://spoonacular.com/food-api/docs)

**Alternative APIs**:
- [TheMealDB](https://www.themealdb.com/api.php) - Free, simpler but limited
- [Edamam Recipe API](https://developer.edamam.com/edamam-recipe-api) - Free tier available
- [Tasty API](https://rapidapi.com/apidojo/api/tasty/) - Via RapidAPI

### Step 2: Understand the API Endpoints

For Spoonacular, key endpoints include:

**Search Recipes by Ingredients**:
```
GET https://api.spoonacular.com/recipes/findByIngredients
```

**Search Recipes by Query**:
```
GET https://api.spoonacular.com/recipes/complexSearch
```

**Get Recipe Information**:
```
GET https://api.spoonacular.com/recipes/{id}/information
```

**Get Recipe Instructions**:
```
GET https://api.spoonacular.com/recipes/{id}/analyzedInstructions
```

### Step 3: Test the API

**Example: Search for recipes with chicken**:
```
https://api.spoonacular.com/recipes/complexSearch?query=chicken&apiKey=YOUR_API_KEY
```

**Example: Get recipe details** (use an ID from search results):
```
https://api.spoonacular.com/recipes/715538/information?apiKey=YOUR_API_KEY
```

### Step 4: Understand the Response Structure

**Search Response**:
```json
{
  "results": [
    {
      "id": 715538,
      "title": "Bruschetta with Tomato and Basil",
      "image": "https://spoonacular.com/recipeImages/715538-312x231.jpg",
      "imageType": "jpg"
    }
  ],
  "offset": 0,
  "number": 10,
  "totalResults": 86
}
```

**Recipe Details Response**:
```json
{
  "id": 715538,
  "title": "Bruschetta with Tomato and Basil",
  "image": "https://spoonacular.com/recipeImages/715538-556x370.jpg",
  "servings": 6,
  "readyInMinutes": 45,
  "vegetarian": true,
  "vegan": false,
  "glutenFree": false,
  "extendedIngredients": [
    {
      "name": "basil",
      "amount": 5,
      "unit": "leaves",
      "original": "5 basil leaves, julienned"
    }
  ],
  "instructions": "Step-by-step instructions...",
  "nutrition": {
    "nutrients": [
      {
        "name": "Calories",
        "amount": 159.71,
        "unit": "kcal"
      }
    ]
  }
}
```

## 💻 Implementation Guide

### Project Structure

```
recipe-finder/
├── main.py (or index.html + script.js)
├── api_client.py (API interaction)
├── recipe_manager.py (Business logic)
├── display.py (Output formatting)
└── favorites.json (Saved recipes)
```

### Python Implementation

**api_client.py**:
```python
import requests
from typing import List, Dict, Optional

class SpoonacularAPI:
    BASE_URL = "https://api.spoonacular.com"
    
    def __init__(self, api_key: str):
        self.api_key = api_key
        self.session = requests.Session()
    
    def search_recipes(self, 
                      query: str = "", 
                      ingredients: str = "",
                      diet: str = "",
                      cuisine: str = "",
                      number: int = 10) -> List[Dict]:
        """
        Search for recipes with various filters
        
        Args:
            query: Search term (e.g., "pasta")
            ingredients: Comma-separated ingredients (e.g., "chicken,rice")
            diet: Diet type (vegetarian, vegan, etc.)
            cuisine: Cuisine type (italian, mexican, etc.)
            number: Number of results to return
        """
        endpoint = f"{self.BASE_URL}/recipes/complexSearch"
        
        params = {
            'apiKey': self.api_key,
            'number': number,
            'addRecipeInformation': True  # Get basic info in search results
        }
        
        if query:
            params['query'] = query
        if ingredients:
            params['includeIngredients'] = ingredients
        if diet:
            params['diet'] = diet
        if cuisine:
            params['cuisine'] = cuisine
        
        try:
            response = self.session.get(endpoint, params=params)
            response.raise_for_status()
            data = response.json()
            return data.get('results', [])
        except requests.exceptions.RequestException as e:
            print(f"Error searching recipes: {e}")
            return []
    
    def get_recipe_details(self, recipe_id: int) -> Optional[Dict]:
        """Get detailed information about a specific recipe"""
        endpoint = f"{self.BASE_URL}/recipes/{recipe_id}/information"
        
        params = {
            'apiKey': self.api_key,
            'includeNutrition': True
        }
        
        try:
            response = self.session.get(endpoint, params=params)
            response.raise_for_status()
            return response.json()
        except requests.exceptions.RequestException as e:
            print(f"Error fetching recipe details: {e}")
            return None
    
    def get_recipe_instructions(self, recipe_id: int) -> List[Dict]:
        """Get step-by-step instructions for a recipe"""
        endpoint = f"{self.BASE_URL}/recipes/{recipe_id}/analyzedInstructions"
        
        params = {'apiKey': self.api_key}
        
        try:
            response = self.session.get(endpoint, params=params)
            response.raise_for_status()
            return response.json()
        except requests.exceptions.RequestException as e:
            print(f"Error fetching instructions: {e}")
            return []
```

**recipe_manager.py**:
```python
import json
from typing import List, Dict
from pathlib import Path

class RecipeManager:
    def __init__(self, favorites_file: str = "favorites.json"):
        self.favorites_file = Path(favorites_file)
        self.favorites = self._load_favorites()
    
    def _load_favorites(self) -> List[int]:
        """Load favorite recipe IDs from file"""
        if self.favorites_file.exists():
            try:
                with open(self.favorites_file, 'r') as f:
                    return json.load(f)
            except json.JSONDecodeError:
                return []
        return []
    
    def _save_favorites(self):
        """Save favorite recipe IDs to file"""
        with open(self.favorites_file, 'w') as f:
            json.dump(self.favorites, f, indent=2)
    
    def add_favorite(self, recipe_id: int):
        """Add a recipe to favorites"""
        if recipe_id not in self.favorites:
            self.favorites.append(recipe_id)
            self._save_favorites()
            return True
        return False
    
    def remove_favorite(self, recipe_id: int):
        """Remove a recipe from favorites"""
        if recipe_id in self.favorites:
            self.favorites.remove(recipe_id)
            self._save_favorites()
            return True
        return False
    
    def is_favorite(self, recipe_id: int) -> bool:
        """Check if a recipe is in favorites"""
        return recipe_id in self.favorites
    
    def filter_recipes(self, 
                      recipes: List[Dict], 
                      max_time: int = None,
                      min_servings: int = None,
                      max_servings: int = None) -> List[Dict]:
        """Filter recipes by additional criteria"""
        filtered = recipes
        
        if max_time:
            filtered = [r for r in filtered 
                       if r.get('readyInMinutes', float('inf')) <= max_time]
        
        if min_servings:
            filtered = [r for r in filtered 
                       if r.get('servings', 0) >= min_servings]
        
        if max_servings:
            filtered = [r for r in filtered 
                       if r.get('servings', float('inf')) <= max_servings]
        
        return filtered
```

**display.py**:
```python
from typing import List, Dict

class RecipeDisplay:
    @staticmethod
    def display_recipe_list(recipes: List[Dict], favorites: List[int] = []):
        """Display a list of recipes"""
        if not recipes:
            print("\nNo recipes found.")
            return
        
        print(f"\n{'=' * 70}")
        print(f"Found {len(recipes)} recipes:")
        print('=' * 70)
        
        for i, recipe in enumerate(recipes, 1):
            favorite_marker = "⭐" if recipe['id'] in favorites else "  "
            
            print(f"\n{favorite_marker} {i}. {recipe['title']}")
            
            # Display dietary info
            dietary_tags = []
            if recipe.get('vegetarian'):
                dietary_tags.append("🌱 Vegetarian")
            if recipe.get('vegan'):
                dietary_tags.append("🥗 Vegan")
            if recipe.get('glutenFree'):
                dietary_tags.append("🌾 Gluten-Free")
            
            if dietary_tags:
                print(f"   {' | '.join(dietary_tags)}")
            
            # Display time and servings
            if recipe.get('readyInMinutes'):
                print(f"   ⏱️  Ready in: {recipe['readyInMinutes']} minutes")
            if recipe.get('servings'):
                print(f"   🍽️  Servings: {recipe['servings']}")
    
    @staticmethod
    def display_recipe_details(recipe: Dict):
        """Display detailed recipe information"""
        print(f"\n{'=' * 70}")
        print(f"{recipe['title']}")
        print('=' * 70)
        
        # Basic information
        if recipe.get('image'):
            print(f"\n📸 Image: {recipe['image']}")
        
        print(f"\n⏱️  Ready in: {recipe.get('readyInMinutes', 'N/A')} minutes")
        print(f"🍽️  Servings: {recipe.get('servings', 'N/A')}")
        
        # Dietary information
        dietary_info = []
        if recipe.get('vegetarian'):
            dietary_info.append("Vegetarian")
        if recipe.get('vegan'):
            dietary_info.append("Vegan")
        if recipe.get('glutenFree'):
            dietary_info.append("Gluten-Free")
        if recipe.get('dairyFree'):
            dietary_info.append("Dairy-Free")
        
        if dietary_info:
            print(f"🥗 Diet: {', '.join(dietary_info)}")
        
        # Ingredients
        if recipe.get('extendedIngredients'):
            print(f"\n📝 Ingredients:")
            for ingredient in recipe['extendedIngredients']:
                print(f"   • {ingredient.get('original', ingredient['name'])}")
        
        # Instructions
        if recipe.get('instructions'):
            print(f"\n👨‍🍳 Instructions:")
            print(f"{recipe['instructions']}")
        
        # Nutrition (if available)
        if recipe.get('nutrition') and recipe['nutrition'].get('nutrients'):
            print(f"\n📊 Nutrition (per serving):")
            nutrients = recipe['nutrition']['nutrients'][:5]  # Show top 5
            for nutrient in nutrients:
                print(f"   • {nutrient['name']}: {nutrient['amount']:.1f}{nutrient['unit']}")
        
        print(f"\n🔗 Source: {recipe.get('sourceUrl', 'N/A')}")
```

**main.py**:
```python
from api_client import SpoonacularAPI
from recipe_manager import RecipeManager
from display import RecipeDisplay

class RecipeFinderApp:
    def __init__(self, api_key: str):
        self.api = SpoonacularAPI(api_key)
        self.manager = RecipeManager()
        self.display = RecipeDisplay()
        self.current_recipes = []
    
    def search_recipes(self):
        """Interactive recipe search"""
        print("\n🔍 Recipe Search")
        print("-" * 50)
        
        query = input("Search term (or press Enter to skip): ").strip()
        ingredients = input("Ingredients (comma-separated, or press Enter): ").strip()
        
        print("\nDietary restrictions:")
        print("1. None")
        print("2. Vegetarian")
        print("3. Vegan")
        print("4. Gluten-Free")
        diet_choice = input("Choose (1-4): ").strip()
        
        diet_map = {
            '2': 'vegetarian',
            '3': 'vegan',
            '4': 'glutenFree'
        }
        diet = diet_map.get(diet_choice, '')
        
        print("\nSearching...")
        self.current_recipes = self.api.search_recipes(
            query=query,
            ingredients=ingredients,
            diet=diet,
            number=10
        )
        
        if self.current_recipes:
            self.display.display_recipe_list(
                self.current_recipes, 
                self.manager.favorites
            )
            return True
        else:
            print("No recipes found. Try different search terms.")
            return False
    
    def view_recipe_details(self):
        """View detailed information about a recipe"""
        if not self.current_recipes:
            print("No recipes to view. Search first!")
            return
        
        try:
            choice = int(input("\nEnter recipe number to view details: "))
            if 1 <= choice <= len(self.current_recipes):
                recipe = self.current_recipes[choice - 1]
                
                # Fetch full details
                detailed_recipe = self.api.get_recipe_details(recipe['id'])
                
                if detailed_recipe:
                    self.display.display_recipe_details(detailed_recipe)
                    
                    # Ask about favorites
                    if self.manager.is_favorite(recipe['id']):
                        action = input("\n💚 Remove from favorites? (y/n): ")
                        if action.lower() == 'y':
                            self.manager.remove_favorite(recipe['id'])
                            print("Removed from favorites!")
                    else:
                        action = input("\n🤍 Add to favorites? (y/n): ")
                        if action.lower() == 'y':
                            self.manager.add_favorite(recipe['id'])
                            print("Added to favorites!")
                else:
                    print("Could not fetch recipe details.")
            else:
                print("Invalid choice.")
        except ValueError:
            print("Please enter a valid number.")
    
    def view_favorites(self):
        """Display all favorite recipes"""
        if not self.manager.favorites:
            print("\nNo favorite recipes yet!")
            return
        
        print("\nFetching your favorite recipes...")
        favorite_recipes = []
        
        for recipe_id in self.manager.favorites:
            recipe = self.api.get_recipe_details(recipe_id)
            if recipe:
                favorite_recipes.append(recipe)
        
        if favorite_recipes:
            self.display.display_recipe_list(
                favorite_recipes,
                self.manager.favorites
            )
        else:
            print("Could not load favorite recipes.")
    
    def run(self):
        """Main application loop"""
        print("\n" + "=" * 50)
        print("🍳 Recipe Finder App")
        print("=" * 50)
        
        while True:
            print("\n📋 Menu:")
            print("1. Search recipes")
            print("2. View recipe details")
            print("3. View favorites")
            print("4. Exit")
            
            choice = input("\nChoose an option (1-4): ").strip()
            
            if choice == '1':
                self.search_recipes()
            elif choice == '2':
                self.view_recipe_details()
            elif choice == '3':
                self.view_favorites()
            elif choice == '4':
                print("\nHappy cooking! 👨‍🍳")
                break
            else:
                print("Invalid choice. Please try again.")

def main():
    # Get API key from user or config file
    api_key = input("Enter your Spoonacular API key: ").strip()
    
    if not api_key:
        print("Error: API key is required")
        return
    
    app = RecipeFinderApp(api_key)
    app.run()

if __name__ == "__main__":
    main()
```

## ✅ Requirements Checklist

Your Recipe Finder App should:

- [ ] **Search Functionality**:
  - [ ] Search by recipe name/keyword
  - [ ] Search by ingredients
  - [ ] Filter by dietary restrictions
  - [ ] Display search results clearly

- [ ] **Recipe Details**:
  - [ ] Show recipe title and image
  - [ ] Display cooking time and servings
  - [ ] List all ingredients
  - [ ] Show cooking instructions
  - [ ] Display nutritional information

- [ ] **Favorites Management**:
  - [ ] Save favorite recipes locally
  - [ ] Mark favorites in recipe lists
  - [ ] View all favorites
  - [ ] Remove from favorites

- [ ] **Error Handling**:
  - [ ] Invalid API key
  - [ ] No results found
  - [ ] Network errors
  - [ ] Invalid recipe IDs

## 🎨 Bonus Challenges

1. **Advanced Filtering** (Medium)
   - Filter by cooking time (under 30 min, etc.)
   - Filter by servings count
   - Filter by calories
   - Combine multiple filters

2. **Shopping List** (Medium)
   - Generate shopping list from selected recipes
   - Combine ingredients from multiple recipes
   - Allow editing quantities

3. **Meal Planning** (Hard)
   - Plan meals for the week
   - Calendar view of planned meals
   - Automatic shopping list generation

4. **Recipe Collections** (Medium)
   - Create custom collections (e.g., "Quick Dinners")
   - Tag recipes with custom labels
   - Share collections

5. **Ingredient Substitutions** (Hard)
   - Use API to find ingredient substitutions
   - Suggest alternatives for dietary restrictions
   - Calculate adjusted nutritional values

6. **Web Interface** (Medium-Hard)
   - Build HTML/CSS/JavaScript version
   - Display recipe images in grid
   - Implement infinite scroll for results
   - Add print-friendly recipe view

## 🐛 Common Issues and Solutions

### Issue: API Rate Limit
**Solution**:
- Free tier: 150 requests/day
- Cache recipe details locally
- Implement request throttling
- Consider upgrading if needed

### Issue: Missing Recipe Data
**Solution**:
- Always check if fields exist
- Provide default values
- Gracefully handle incomplete recipes

### Issue: Large Response Times
**Solution**:
- Show loading indicators
- Implement timeout handling
- Cache frequently accessed recipes

## 📖 Learning Resources

- [Spoonacular API Documentation](https://spoonacular.com/food-api/docs)
- [Working with Complex JSON](../../modules/06-working-with-json/)
- [API Best Practices](../../modules/03-rest-apis/)
- [Handling State in Applications](https://en.wikipedia.org/wiki/State_(computer_science))

## 🎯 Success Criteria

You've successfully completed this project when:
1. Users can search and filter recipes effectively
2. Recipe details display completely and accurately
3. Favorites persist across application sessions
4. All errors are handled gracefully
5. The application provides a smooth user experience

## 🤔 Reflection Questions

1. How did managing state (favorites) differ from simpler API projects?
2. What strategies did you use to handle complex nested JSON?
3. How would you optimize the app to reduce API calls?
4. What additional features would make this app more useful?
5. How could you implement offline functionality?

## 📤 Share Your Work

- Screenshot your recipe search results
- Share interesting recipes you found
- Document your favorite features
- Consider deploying as a web app

---

**Congratulations!** 🎉

You've completed all three projects and have hands-on experience with:
- Simple API requests (Weather Dashboard)
- REST APIs with multiple endpoints (GitHub Viewer)
- Complex applications with state management (Recipe Finder)

You're now ready to build your own API-powered applications!

---

[← Back to Projects](../README.md) | [Main README](../../README.md)
