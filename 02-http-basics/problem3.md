# Problem 3: Design an API Conversation (Hard)

## Instructions

You're building a **Recipe API** that lets users search for recipes, save favorites, and submit their own recipes.

For each feature below, design the complete HTTP request and response. Be as detailed as possible!

---

## Feature 1: Search for Recipes

Design an API endpoint that allows users to search for recipes with filters.

### HTTP Request

**Method:**
```

```

**Full URL (with example parameters):**
```

```

**Headers:**
```




```

**Body (if needed):**
```




```

---

### Successful Response

**Status Code:**
```

```

**Headers:**
```


```

**Body:**
```json







```

---

### Error Response (No Recipes Found)

**Status Code:**
```

```

**Body:**
```json




```

---

## Feature 2: Save a Recipe to Favorites

Design an endpoint for saving a recipe to a user's favorites list.

### HTTP Request

**Method:**
```

```

**URL:**
```

```

**Headers:**
```




```

**Body:**
```json




```

---

### Successful Response

**Status Code:**
```

```

**Body:**
```json






```

---

### Error Response (Recipe Doesn't Exist)

**Status Code:**
```

```

**Body:**
```json




```

---

## Feature 3: Submit a New Recipe

Design an endpoint for users to submit their own recipes.

### HTTP Request

**Method:**
```

```

**URL:**
```

```

**Headers:**
```




```

**Body (Sample Recipe Data):**
```json













```

---

### Successful Response

**Status Code:**
```

```

**Headers:**
```


```

**Body:**
```json






```

---

### Error Response (Missing Required Data)

**Status Code:**
```

```

**Body:**
```json




```

---

### Error Response (Unauthorized User)

**Status Code:**
```

```

**Body:**
```json




```

---

## Feature 4: Update a Recipe's Rating

Design an endpoint for users to rate a recipe.

### HTTP Request

**Method:**
```

```

**URL:**
```

```

**Headers:**
```




```

**Body:**
```json



```

---

### Successful Response

**Status Code:**
```

```

**Body:**
```json






```

---

### Error Response (Recipe Not Found)

**Status Code:**
```

```

**Body:**
```json




```

---

### Error Response (Unauthorized)

**Status Code:**
```

```

**Body:**
```json




```

---

## Reflection Questions

1. **Why did you choose those specific HTTP methods for each feature?**
```




```

2. **What headers did you include and why are they important?**
```




```

3. **How would you organize the URL structure for related endpoints?**
```




```

4. **What other features could you add to this Recipe API?**
```




```

5. **If you were building the actual API, what security measures would you implement?**
```




```

---

## Bonus Challenge

Design one more feature of your choice for the Recipe API:
- Feature name:
- HTTP request design:
- Response design:
- Possible errors:

---

**Great work! You're thinking like an API designer! 🎉**

**Check the main README for detailed solution examples!**
