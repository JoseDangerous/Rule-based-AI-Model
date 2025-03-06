# Building a Rule-Based AI System in Python project.
---

## Part 1: Initial Project Ideas

### Project Idea 1: Plant Disease Diagnostic Tool
- **Description:** A system where users describe symptoms in their plants, and the AI provides possible diseases and treatment recommendations. 
- **Rule-Based Approach:**  
  Uses decision trees with IF-THEN rules to match symptom descriptions with diseases.
  Keywords like "yellow leaves," "spots," or "wilting" trigger specific diagnostic paths.

### Project Idea 2: Movie Recommendation System
- **Description:** Suggests movies based on user preferences and criteria provided.
- **Rule-Based Approach:**  
  Rules match user inputs (genre preferences, mood, release year, length) against a database of movies, applying filters and priority rules.

### Project Idea 3: Diet Meal Planner
- **Description:** Creates meal suggestions based on dietary restrictions, preferences, and nutritional goals.  
- **Rule-Based Approach:**  
  Applies rules to filter food options based on constraints (allergies, calories, nutritional requirements) and generates compatible meal combinations.

### Chosen Idea: Movie Recommendation System 
**Justification:** I chose this idea because my friends, family, and I are always trying to decide on what to watch and this could help us decide. This project would be applicable to real-world scenarios and allow me to easily categorize movies to recommend based on rules and keywords.

---

## Part 2: Rules/Logic for the Chosen System

The **Movie Recommendation System** will function as follows:

1. **User Input Processing Rules:**  
  - **IF** user inputs genre preference
    Add genre to filter criteria
  - **IF** user specifies release year/period
    Add year range to filter criteria
  - **IF** user indicates mood (e.g., "happy", "scary", "thoughtful")
    Map mood to appropriate genres
  - **IF** user sets runtime preferences (e.g., "short", "long")
    Map to specific minute ranges
  - **IF** user mentions actors/directors
    Add to preference criteria

2. **Movie Filtering Rules:**  
  - **FOR EACH** movie in database:
    - IF movie.genre matches ANY user genre preferences
      - Add points to movie score
    - IF movie.year is within user's preferred time period
      - Add points to movie score
    - IF movie.runtime matches user preference
      - Add points to movie score
    - IF movie contains preferred actors/directors
      - Add points to movie score
    - IF user has previously liked similar movies
      - Add additional points

3. **Recommendation Logic:**  
  - SORT movies by score (highest to lowest)
  - SELECT top N movies from sorted list
  - IF no movies meet minimum threshold
    - Request additional preferences OR broaden search
  - RETURN personalized recommendation list with brief descriptions

4. **Implementation Details:**
  - Store movies in a structured format (dictionary or class)
  - Use keyword matching for processing natural language input
  - Implement scoring system (0-10) for each movie based on match quality
  - Track previous recommendations to avoid repetition
  - Include a feedback mechanism to refine future recommendations

5. **Enhancement Rules:**  
  - IF user rejects recommendation
    - Ask for reason and adjust preferences accordingly
  - IF user has watched >5 movies of a specific genre
    - Increase weight for that genre in recommendations
  - IF user consistently watches movies from specific era/director
    - Automatically prioritize similar content

---

## Part 3: System Input and Output Results

1. **Sample 1:**

Welcome to the Movie Recommendation System!
Let's find you a perfect movie to watch.

What genres are you interested in? (e.g., action, comedy, drama, sci-fi, thriller, horror, romance)
Enter genres separated by commas: action

Preferred release period? (e.g., '2000-2010', '90s', 'recent', or 'classic'): recent

Preferred movie length? (short, medium, long): short

What's your mood today? (happy, sad, excited, scared, thoughtful, relaxed): excited

Any favorite actors or directors? (separated by commas):

Thank you for your preferences! Finding recommendations...

🎬 YOUR MOVIE RECOMMENDATIONS 🎬

1. Inception (2010) - action, sci-fi, thriller
   Score: 4/10
   Why: Matching genres: action, Matches your excited mood
   Plot: A thief who steals corporate secrets through the use of dream-sharing technology is given the inverse task of planting an idea into the mind of a C.E.O.

2. The Dark Knight (2008) - action, crime, thriller
   Score: 4/10
   Why: Matching genres: action, Matches your excited mood
   Plot: When the menace known as the Joker wreaks havoc and chaos on the people of Gotham, Batman must accept one of the greatest psychological and physical tests of his ability to fight injustice.

3. Finding Nemo (2003) - animation, adventure, comedy
   Score: 2/10
   Why: Matches your excited mood
   Plot: After his son is captured in the Great Barrier Reef and taken to Sydney, a timid clownfish sets out on a journey to bring him home.

Enjoy your movie night! 🍿


2. **Sample 2:**

What genres are you interested in? (e.g., action, comedy, drama, sci-fi, thriller, horror, romance)
Enter genres separated by commas: action, sci-fi, comedy

Preferred release period? (e.g., '2000-2010', '90s', 'recent', or 'classic'): 2000-2010

Preferred movie length? (short, medium, long): medium

What's your mood today? (happy, sad, excited, scared, thoughtful, relaxed): happy

Any favorite actors or directors? (separated by commas): christopher nolan

Thank you for your preferences! Finding recommendations...

🎬 YOUR MOVIE RECOMMENDATIONS 🎬

1. Finding Nemo (2003) - animation, adventure, comedy
   Score: 7/10
   Why: Matching genres: comedy, Matches your happy mood, Released in your preferred time period (2000-2010), Movie length matches your preference (medium)
   Plot: After his son is captured in the Great Barrier Reef and taken to Sydney, a timid clownfish sets out on a journey to bring him home.

2. Up (2009) - animation, adventure, comedy
   Score: 7/10
   Why: Matching genres: comedy, Matches your happy mood, Released in your preferred time period (2000-2010), Movie length matches your preference (medium)
   Plot: 78-year-old Carl Fredricksen travels to Paradise Falls in his house equipped with balloons, inadvertently taking a young stowaway.

3. Inception (2010) - action, sci-fi, thriller
   Score: 6/10
   Why: Matching genres: action, sci-fi, Released in your preferred time period (2000-2010)
   Plot: A thief who steals corporate secrets through the use of dream-sharing technology is given the inverse task of planting an idea into the mind of a C.E.O.

Enjoy your movie night! 🍿


3. **Sample 3:**

What genres are you interested in? (e.g., action, comedy, drama, sci-fi, thriller, horror, romance)
Enter genres separated by commas: horror

Preferred release period? (e.g., '2000-2010', '90s', 'recent', or 'classic'): 90s

Preferred movie length? (short, medium, long): long

What's your mood today? (happy, sad, excited, scared, thoughtful, relaxed): scared

Any favorite actors or directors? (separated by commas):

Thank you for your preferences! Finding recommendations...

🎬 YOUR MOVIE RECOMMENDATIONS 🎬

1. The Silence of the Lambs (1991) - crime, thriller, horror
   Score: 6/10
   Why: Matching genres: horror, Matches your scared mood, Released in your preferred time period (1990-1999)
   Plot: A young F.B.I. cadet must receive the help of an incarcerated and manipulative cannibal killer to help catch another serial killer.

2. The Shawshank Redemption (1994) - drama
   Score: 3/10
   Why: Released in your preferred time period (1990-1999), Movie length matches your preference (long)
   Plot: Two imprisoned men bond over a number of years, finding solace and eventual redemption through acts of common decency.

3. Inception (2010) - action, sci-fi, thriller
   Score: 3/10
   Why: Matches your scared mood, Movie length matches your preference (long)
   Plot: A thief who steals corporate secrets through the use of dream-sharing technology is given the inverse task of planting an idea into the mind of a C.E.O.

Enjoy your movie night! 🍿

---

## Part 4: Reflection

### Project Overview:
This rule-based movie recommendation system uses a series of logical rules rather than machine learning to provide personalized movie suggestions. The system maintains a collection of movies with attributes like title, year, genres, director, actors, runtime, and plot summary. The system gathers user preferences such as preferred genres, release year/period, runtime preferences, current mood, etc. through interactive prompts. Each movie is evaluated against user preferences using clearly defined rules and movies matching preferences earn points. Afterward, movies are sorted by score and the top-scoring options are presented with explanations of why they were recommended. Users can then adjust their preferences for new recommendations or start over completely.

### Challenges:
Surprisingly, I encountered no challenges when prompting the AI to create this project and Python code. Using the right prompts was a crucial aspect, but the AI model created a robust logical structure and well functioning code after only 1 prompt.