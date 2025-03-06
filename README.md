# Building a Rule-Based AI System in Python project.
---

## Part 1: Initial Project Ideas

### 1. Project Idea 1: Plant Disease Diagnostic Tool
- **Description:** A system where users describe symptoms in their plants, and the AI provides possible diseases and treatment recommendations. 
- **Rule-Based Approach:**  
  - Uses decision trees with IF-THEN rules to match symptom descriptions with diseases.
  - Keywords like "yellow leaves," "spots," or "wilting" trigger specific diagnostic paths.

### 2. Project Idea 2: Movie Recommendation System
- **Description:** Suggests movies based on user preferences and criteria provided.
- **Rule-Based Approach:**  
  - Rules match user inputs (genre preferences, mood, release year, length) against a database of movies, applying filters and priority rules.

### 3. Project Idea 3: Diet Meal Planner
- **Description:** Creates meal suggestions based on dietary restrictions, preferences, and nutritional goals.  
- **Rule-Based Approach:**  
  - Applies rules to filter food options based on constraints (allergies, calories, nutritional requirements) and generates compatible meal combinations.

### **Chosen Idea:** Movie Recommendation System 
**Justification:** I chose this idea because my friends, family, and I are always trying to decide on what to watch and this could help us decide. This project would be applicable to real-world scenarios and allow me to easily categorize movies to recommend based on rules and keywords.

---

## Part 2: Rules/Logic for the Chosen System

The **Recipe Recommender** system will follow these rules:

1. **Exact Match Rule:**  
   - **IF** all ingredients in a recipe are found in the user’s ingredient list → **Recommend the recipe.**

2. **Partial Match Rule:**  
   - **IF** 75% or more of the ingredients in a recipe match the user’s ingredient list →  
     - **Recommend the recipe.**  
     - **Suggest the missing ingredients.**

3. **Common Ingredients Rule:**  
   - Ingredients like salt, pepper, and water are considered optional and will not be counted as missing.

4. **No Match Rule:**  
   - **IF** no recipes match → **Suggest adding more ingredients** for better recommendations.

5. **Low Ingredient Rule:**  
   - **IF** fewer than three ingredients are provided → **Notify the user** and suggest adding more ingredients.

---

## Part 3: Rules/Logic for the Chosen System

Sample input and output: 

Enter your ingredients (comma-separated): chicken, rice, soy sauce
You are close to making Chicken Fried Rice! Missing: garlic.

Enter your ingredients (comma-separated): garlic, soy sauce
No recipes match. Try adding more ingredients.

Enter your ingredients (comma-separated): pasta, tomatoes, garlic, olive oil
You can make Spaghetti Pomodoro!

---

## Part 4: Reflection

### Project Overview:
This project involved designing a practical, rule-based system to recommend recipes based on user inputs. The system uses logical conditions (e.g., exact and partial matches) to evaluate user-provided ingredients against recipes in the dataset.

### Challenges:
- **Handling Partial Matches:**  
  Deciding on a threshold (75%) that balances flexibility with accuracy was challenging.
- **Common Ingredients:**  
  Ensuring common ingredients like salt and water don’t skew the results. I resolved this by excluding them from the missing ingredient list.

### Comparison to Machine Learning:
- Unlike machine learning models, this system relies entirely on prewritten rules rather than learning from data.  
- **Advantages:** Simplicity and transparency.  
- **Limitations:**  
  - Limited scalability.  
  - Adding complex logic or handling ambiguous inputs (e.g., "bread" vs. "whole-grain bread") requires extensive manual rule updates, which machine learning could handle more flexibly.













