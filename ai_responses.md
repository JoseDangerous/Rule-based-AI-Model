## Model Used: GitHub Copilot using Claude 3.7 Sonnet (Preview)

## Prompt Used:
*I am working on a Python project to create a simple AI system based on rules or heuristics. This is for an assignment where I need to understand how AI worked before machine learning. Please suggest some project ideas for a rule-based AI system. Please make sure to include examples like chatbots, recommendation systems, diagnostic tools, and any other rule-based AI system. Please provide an overview for each option suggested.*

## AI Response:

# Rule-Based AI Project Ideas

Here are several project ideas for your rule-based AI system:

## 1. Plant Disease Diagnostic Tool
**What it does**: A system where users describe symptoms in their plants, and the AI provides possible diseases and treatment recommendations.
**How it works**: Uses decision trees with IF-THEN rules to match symptom descriptions with diseases. Keywords like "yellow leaves," "spots," or "wilting" trigger specific diagnostic paths.

## 2. Movie Recommendation System
**What it does**: Suggests movies based on user preferences and criteria.
**How it works**: Rules match user inputs (genre preferences, mood, desired release period, length) against a database of movies, applying filters and priority rules.

## 3. Personal Finance Advisor
**What it does**: Provides basic financial advice based on income, expenses, and financial goals.
**How it works**: Uses predefined heuristics to analyze spending patterns, income levels, and goals to suggest budget adjustments or savings strategies.

## 4. Computer Troubleshooting Assistant
**What it does**: Helps users diagnose and fix common computer issues.
**How it works**: Follows a decision tree of symptoms and causes, asking clarifying questions to narrow down problems before suggesting solutions.

## 5. Diet Meal Planner
**What it does**: Creates meal suggestions based on dietary restrictions, preferences, and nutritional goals.
**How it works**: Applies rules to filter food options based on constraints (allergies, calories, nutritional requirements) and generates compatible meal combinations.

Each of these systems can be implemented with straightforward conditional logic and doesn't require machine learning algorithms, making them excellent examples of traditional rule-based AI systems.

---

**Prompt Used:**
*I want to create a Movie Recommendation AI System. The system will be rule-based. Can you help me outline the rules and logic needed to make this work? For example, what conditions or keywords should I check for, and what responses or actions should my system take?*

**AI Response:**

# Movie Recommendation System Rules and Logic

## Core System Components

1. **User Preference Collection**
2. **Rule-Based Filtering**
3. **Recommendation Generation**
4. **Feedback Processing**

## Detailed Rules and Logic

### 1. User Input Processing Rules

```
IF user inputs genre preference
    Add genre to filter criteria
IF user specifies release year/period
    Add year range to filter criteria
IF user indicates mood (e.g., "happy", "scary", "thoughtful")
    Map mood to appropriate genres
IF user sets runtime preferences (e.g., "short", "long")
    Map to specific minute ranges
IF user mentions actors/directors
    Add to preference criteria
```

### 2. Movie Filtering Rules

```
FOR EACH movie in database:
    IF movie.genre matches ANY user genre preferences
        Add points to movie score
    IF movie.year is within user's preferred time period
        Add points to movie score
    IF movie.runtime matches user preference
        Add points to movie score
    IF movie contains preferred actors/directors
        Add points to movie score
    IF user has previously liked similar movies
        Add additional points
```

### 3. Recommendation Logic

```
SORT movies by score (highest to lowest)
SELECT top N movies from sorted list
IF no movies meet minimum threshold
    Request additional preferences OR broaden search
RETURN personalized recommendation list with brief descriptions
```

### 4. Implementation Details

- Store movies in a structured format (dictionary or class)
- Use keyword matching for processing natural language input
- Implement scoring system (0-10) for each movie based on match quality
- Track previous recommendations to avoid repetition
- Include a feedback mechanism to refine future recommendations

### 5. Enhancement Rules

```
IF user rejects recommendation
    Ask for reason and adjust preferences accordingly
IF user has watched >5 movies of a specific genre
    Increase weight for that genre in recommendations
IF user consistently watches movies from specific era/director
    Automatically prioritize similar content
```

This rule-based system doesn't require machine learning but can still provide personalized recommendations by applying logical rules to user inputs and a database of movies with their attributes.
