# Problem 2: Pokemon Data Explorer (Medium)

## Instructions

Use the **PokeAPI** (https://pokeapi.co) to build a Pokemon information tool.

The PokeAPI is a free RESTful API that provides data about Pokemon. No authentication required!

---

## Requirements

Build a program that can fetch and display Pokemon information.

### Minimum Requirements

1. **Function to fetch Pokemon data**
   - Takes a Pokemon name as input
   - Makes API request to: `https://pokeapi.co/api/v2/pokemon/{name}`
   - Returns the Pokemon data

2. **Display Pokemon information**
   - Name
   - Types (e.g., "electric", "water")
   - Abilities
   - Height and weight
   - Base stats (HP, Attack, Defense, Speed, etc.)

3. **Error handling**
   - Handle Pokemon not found (404)
   - Handle network errors
   - Display user-friendly error messages

4. **Search multiple Pokemon**
   - Allow searching for multiple Pokemon in sequence

---

## Your Code

### Python Template
```python
import requests

def get_pokemon_info(pokemon_name):
    """
    Fetch and display information about a Pokemon
    
    Args:
        pokemon_name (str): Name of the Pokemon (e.g., 'pikachu')
    """
    # Your code here
    url = f"https://pokeapi.co/api/v2/pokemon/{pokemon_name.lower()}"
    
    # TODO: Make the API request
    # TODO: Handle errors
    # TODO: Parse and display the data
    
    pass

def main():
    """Main function to run the Pokemon explorer"""
    # Your code here
    pass

if __name__ == "__main__":
    main()
```

### JavaScript Template
```javascript
async function getPokemonInfo(pokemonName) {
  /**
   * Fetch and display information about a Pokemon
   * 
   * @param {string} pokemonName - Name of the Pokemon (e.g., 'pikachu')
   */
  const url = `https://pokeapi.co/api/v2/pokemon/${pokemonName.toLowerCase()}`;
  
  // TODO: Make the API request
  // TODO: Handle errors
  // TODO: Parse and display the data
}

async function main() {
  // Your code here
}

main();
```

---

## Testing

Test your program with these Pokemon:

1. **pikachu** - Should work perfectly
2. **charizard** - Should work perfectly
3. **mewtwo** - Should work perfectly
4. **ditto** - Should work perfectly
5. **invalidname** - Should trigger error handling

---

## Expected Output Example

```
==================================================
Pokemon: Pikachu
==================================================
Types: electric
Abilities: static, lightning-rod
Height: 0.4m
Weight: 6.0kg

Stats:
  hp: 35
  attack: 55
  defense: 40
  special-attack: 50
  special-defense: 50
  speed: 90
```

---

## Part 2: Enhanced Features

Choose at least **2** of these features to add:

### Feature 1: Multiple Pokemon Comparison
```
Allow user to fetch multiple Pokemon and compare their stats side-by-side
```

### Feature 2: Sprite Display
```
Pokemon data includes sprite URLs. Display the sprite URL or download the image
Example: pokemon['sprites']['front_default']
```

### Feature 3: Move List
```
Display the first 5 moves the Pokemon can learn
API endpoint: pokemon['moves']
```

### Feature 4: Color-coded Stats
```
Color-code stats based on values:
- High (>80): Green
- Medium (40-80): Yellow
- Low (<40): Red
(Use terminal colors if possible, or just labels)
```

### Feature 5: Save to File
```
Save Pokemon data to a JSON file for later reference
```

---

## Your Enhanced Feature Code

### Feature #1 (Choose from above):
```python
# Your code here










```

### Feature #2 (Choose from above):
```python
# Your code here










```

---

## Part 3: Bonus Challenge

### Evolution Chain

Fetch and display the Pokemon's evolution chain!

**Steps:**
1. Get the Pokemon species URL from the Pokemon data
2. Fetch the species data
3. Get the evolution chain URL
4. Fetch the evolution chain data
5. Parse and display the evolution path

**Hint:** This requires making 3-4 API calls!

**Your Code:**
```python
# Your code here
















```

**Example Output:**
```
Evolution Chain for Pikachu:
pichu -> pikachu -> raichu
```

---

## Testing Checklist

- [ ] Successfully fetches Pokemon data
- [ ] Displays all required information
- [ ] Handles invalid Pokemon names gracefully
- [ ] Handles network errors
- [ ] Works with multiple Pokemon
- [ ] At least 2 enhanced features implemented
- [ ] Code is well-organized and commented
- [ ] Tested with all 5 test Pokemon

---

## Reflection Questions

1. **What was the most challenging part of this exercise?**
```



```

2. **How did you structure your error handling?**
```



```

3. **If you implemented multiple API calls (like evolution chain), how did you organize them?**
```



```

4. **What would you add to make this tool even more useful?**
```



```

---

## Submission

Save your code as:
- `problem2.py` (for Python) or
- `problem2.js` (for JavaScript)

Include comments explaining your code!

---

**Great job building a real API integration! 🎉**

**Check the main README for solution approaches!**
