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

## Prompt Used:
*I want to create a Movie Recommendation AI System. The system will be rule-based. Can you help me outline the rules and logic needed to make this work? For example, what conditions or keywords should I check for, and what responses or actions should my system take?*

## AI Response:

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

---

## Prompt Used:
*I need help writing Python code for the rule-based movie recommendation system. The system should follow the rules and logic previously outlined. The system should include user input, rule-based decision making using conditional statements, and should output recommendations based on the rules. Please include comments explaining how the rules are implemented and how the code works. Could you help me write the Python code for this?*

## AI Response:

# Rule-Based Movie Recommendation System

Here's a Python implementation of your movie recommendation system following the rules we outlined:

````python
import json
import re
from datetime import datetime

class MovieRecommender:
    def __init__(self):
        # Initialize the movie database
        self.load_movies()
        # Track user preferences
        self.user_preferences = {
            "genres": [],
            "years": [],
            "runtime": None,
            "actors": [],
            "directors": [],
            "mood": None,
            "previous_recommendations": []
        }
        # Define mood to genre mappings
        self.mood_to_genre = {
            "happy": ["comedy", "family", "animation", "musical"],
            "sad": ["drama", "romance"],
            "excited": ["action", "adventure", "sci-fi", "thriller"],
            "scared": ["horror", "thriller"],
            "thoughtful": ["drama", "documentary", "mystery"],
            "relaxed": ["comedy", "romance", "animation"]
        }
        # Define runtime ranges
        self.runtime_ranges = {
            "short": (0, 90),
            "medium": (91, 120),
            "long": (121, 999)
        }

    def load_movies(self):
        """Load the movie database from a JSON file or create a sample one if it doesn't exist."""
        try:
            with open("movies.json", "r") as file:
                self.movies = json.load(file)
        except FileNotFoundError:
            # Create a sample movie database
            self.movies = [
                {
                    "title": "The Shawshank Redemption",
                    "year": 1994,
                    "genres": ["drama"],
                    "director": "Frank Darabont",
                    "actors": ["Tim Robbins", "Morgan Freeman"],
                    "runtime": 142,
                    "plot": "Two imprisoned men bond over a number of years, finding solace and eventual redemption through acts of common decency."
                },
                {
                    "title": "Inception",
                    "year": 2010,
                    "genres": ["action", "sci-fi", "thriller"],
                    "director": "Christopher Nolan",
                    "actors": ["Leonardo DiCaprio", "Joseph Gordon-Levitt"],
                    "runtime": 148,
                    "plot": "A thief who steals corporate secrets through the use of dream-sharing technology is given the inverse task of planting an idea into the mind of a C.E.O."
                },
                {
                    "title": "The Dark Knight",
                    "year": 2008,
                    "genres": ["action", "crime", "thriller"],
                    "director": "Christopher Nolan",
                    "actors": ["Christian Bale", "Heath Ledger"],
                    "runtime": 152,
                    "plot": "When the menace known as the Joker wreaks havoc and chaos on the people of Gotham, Batman must accept one of the greatest psychological and physical tests of his ability to fight injustice."
                },
                {
                    "title": "Finding Nemo",
                    "year": 2003,
                    "genres": ["animation", "adventure", "comedy"],
                    "director": "Andrew Stanton",
                    "actors": ["Albert Brooks", "Ellen DeGeneres"],
                    "runtime": 100,
                    "plot": "After his son is captured in the Great Barrier Reef and taken to Sydney, a timid clownfish sets out on a journey to bring him home."
                },
                {
                    "title": "The Silence of the Lambs",
                    "year": 1991,
                    "genres": ["crime", "thriller", "horror"],
                    "director": "Jonathan Demme",
                    "actors": ["Jodie Foster", "Anthony Hopkins"],
                    "runtime": 118,
                    "plot": "A young F.B.I. cadet must receive the help of an incarcerated and manipulative cannibal killer to help catch another serial killer."
                },
                {
                    "title": "La La Land",
                    "year": 2016,
                    "genres": ["musical", "romance", "drama"],
                    "director": "Damien Chazelle",
                    "actors": ["Ryan Gosling", "Emma Stone"],
                    "runtime": 128,
                    "plot": "While navigating their careers in Los Angeles, a pianist and an actress fall in love while attempting to reconcile their aspirations for the future."
                },
                {
                    "title": "Parasite",
                    "year": 2019,
                    "genres": ["thriller", "drama", "comedy"],
                    "director": "Bong Joon Ho",
                    "actors": ["Song Kang-ho", "Lee Sun-kyun"],
                    "runtime": 132,
                    "plot": "Greed and class discrimination threaten the newly formed symbiotic relationship between the wealthy Park family and the destitute Kim clan."
                },
                {
                    "title": "Up",
                    "year": 2009,
                    "genres": ["animation", "adventure", "comedy"],
                    "director": "Pete Docter",
                    "actors": ["Edward Asner", "Jordan Nagai"],
                    "runtime": 96,
                    "plot": "78-year-old Carl Fredricksen travels to Paradise Falls in his house equipped with balloons, inadvertently taking a young stowaway."
                }
            ]

    def collect_preferences(self):
        """Collect user preferences through interactive prompts."""
        print("\nWelcome to the Movie Recommendation System!")
        print("Let's find you a perfect movie to watch.\n")
        
        # Collect genre preferences
        print("What genres are you interested in? (e.g., action, comedy, drama, sci-fi, thriller, horror, romance)")
        genres_input = input("Enter genres separated by commas: ").lower()
        if genres_input:
            self.user_preferences["genres"] = [genre.strip() for genre in genres_input.split(",")]
        
        # Collect year preferences
        year_input = input("\nPreferred release period? (e.g., '2000-2010', '90s', 'recent', or 'classic'): ").lower()
        self.parse_year_preference(year_input)
        
        # Collect runtime preferences
        runtime = input("\nPreferred movie length? (short, medium, long): ").lower()
        if runtime in self.runtime_ranges:
            self.user_preferences["runtime"] = runtime
        
        # Collect mood
        mood = input("\nWhat's your mood today? (happy, sad, excited, scared, thoughtful, relaxed): ").lower()
        if mood in self.mood_to_genre:
            self.user_preferences["mood"] = mood
            
        # Collect actor/director preferences
        people_input = input("\nAny favorite actors or directors? (separated by commas): ").lower()
        if people_input:
            people = [person.strip() for person in people_input.split(",")]
            # Simple logic to guess if it's an actor or director
            for person in people:
                if "direct" in person or "producer" in person:
                    self.user_preferences["directors"].append(person.replace("director ", "").replace("producer ", ""))
                else:
                    self.user_preferences["actors"].append(person)
                    
        print("\nThank you for your preferences! Finding recommendations...")

    def parse_year_preference(self, year_input):
        """Parse different formats of year preferences and convert to a range."""
        current_year = datetime.now().year
        
        # Handle decade formats
        if re.match(r"(\d{2})s", year_input):
            decade = int(re.match(r"(\d{2})s", year_input).group(1))
            # Convert 2-digit to 4-digit years
            if decade < 50:  # Assume 2000s
                start_year = 2000 + decade
            else:  # Assume 1900s
                start_year = 1900 + decade
            self.user_preferences["years"] = [start_year, start_year + 9]
            
        # Handle specific range formats (e.g., "2000-2010")
        elif re.match(r"(\d{4})-(\d{4})", year_input):
            matches = re.match(r"(\d{4})-(\d{4})", year_input)
            self.user_preferences["years"] = [int(matches.group(1)), int(matches.group(2))]
            
        # Handle relative terms
        elif "recent" in year_input or "new" in year_input:
            self.user_preferences["years"] = [current_year - 5, current_year]
        elif "classic" in year_input or "old" in year_input:
            self.user_preferences["years"] = [1920, 1980]
        else:
            # Try to parse as a specific year
            try:
                specific_year = int(year_input)
                self.user_preferences["years"] = [specific_year - 2, specific_year + 2]
            except ValueError:
                # If we can't parse, don't set any year preference
                pass

    def score_movie(self, movie):
        """
        Score a movie based on how well it matches user preferences.
        Returns a score from 0-10 and reasons for the score.
        """
        score = 0
        reasons = []
        
        # Rule 1: Match genres
        if self.user_preferences["genres"]:
            matching_genres = [genre for genre in movie["genres"] if genre in self.user_preferences["genres"]]
            genre_score = len(matching_genres) * 2  # Each matching genre adds 2 points
            if genre_score > 0:
                score += min(genre_score, 4)  # Cap at 4 points
                reasons.append(f"Matching genres: {', '.join(matching_genres)}")
                
        # Rule 2: Match mood-based genres
        if self.user_preferences["mood"]:
            mood_genres = self.mood_to_genre.get(self.user_preferences["mood"], [])
            matching_mood_genres = [genre for genre in movie["genres"] if genre in mood_genres]
            if matching_mood_genres:
                score += 2
                reasons.append(f"Matches your {self.user_preferences['mood']} mood")
                
        # Rule 3: Match years
        if self.user_preferences["years"]:
            year_range = self.user_preferences["years"]
            if year_range[0] <= movie["year"] <= year_range[1]:
                score += 2
                reasons.append(f"Released in your preferred time period ({year_range[0]}-{year_range[1]})")
                
        # Rule 4: Match runtime
        if self.user_preferences["runtime"]:
            runtime_range = self.runtime_ranges[self.user_preferences["runtime"]]
            if runtime_range[0] <= movie["runtime"] <= runtime_range[1]:
                score += 1
                reasons.append(f"Movie length matches your preference ({self.user_preferences['runtime']})")
                
        # Rule 5: Match actors/directors
        for actor in self.user_preferences["actors"]:
            if any(actor in movie_actor.lower() for movie_actor in movie["actors"]):
                score += 1
                reasons.append(f"Features actor: {actor}")
                
        if self.user_preferences["directors"]:
            for director in self.user_preferences["directors"]:
                if director in movie["director"].lower():
                    score += 1
                    reasons.append(f"Directed by: {director}")
        
        # Rule 6: Penalize previously recommended movies
        if movie["title"] in self.user_preferences["previous_recommendations"]:
            score -= 5
            
        return score, reasons

    def get_recommendations(self, num_recommendations=3):
        """Get movie recommendations based on user preferences."""
        scored_movies = []
        
        for movie in self.movies:
            score, reasons = self.score_movie(movie)
            scored_movies.append((movie, score, reasons))
            
        # Sort by score (highest first)
        scored_movies.sort(key=lambda x: x[1], reverse=True)
        
        # Get top recommendations
        recommendations = []
        for movie, score, reasons in scored_movies[:num_recommendations]:
            if score > 0:  # Only include movies with positive scores
                recommendations.append({
                    "title": movie["title"],
                    "year": movie["year"],
                    "genres": movie["genres"],
                    "score": score,
                    "reasons": reasons,
                    "plot": movie["plot"]
                })
                self.user_preferences["previous_recommendations"].append(movie["title"])
                
        return recommendations

    def display_recommendations(self, recommendations):
        """Display the recommendations to the user."""
        if not recommendations:
            print("\nSorry, I couldn't find any movies matching your preferences.")
            print("Try adjusting your preferences to get better recommendations.")
            return
            
        print("\n🎬 YOUR MOVIE RECOMMENDATIONS 🎬")
        print("-" * 50)
        
        for i, rec in enumerate(recommendations, 1):
            print(f"{i}. {rec['title']} ({rec['year']}) - {', '.join(rec['genres'])}")
            print(f"   Score: {rec['score']}/10")
            print(f"   Why: {', '.join(rec['reasons'])}")
            print(f"   Plot: {rec['plot']}")
            print("-" * 50)
            
        print("\nEnjoy your movie night! 🍿")

    def run(self):
        """Main method to run the recommendation system."""
        self.collect_preferences()
        recommendations = self.get_recommendations()
        self.display_recommendations(recommendations)
        
        # Ask if user wants new recommendations
        while True:
            again = input("\nWould you like more recommendations? (yes/no): ").lower()
            if again != "yes":
                print("Thank you for using the Movie Recommender System! Goodbye!")
                break
                
            # Adjust preferences or start over
            adjust = input("Would you like to adjust your preferences or start over? (adjust/start over): ").lower()
            if adjust == "start over":
                # Reset previous recommendations but keep the rest
                self.user_preferences["previous_recommendations"] = []
                self.collect_preferences()
            else:
                # Allow simple adjustment
                print("\nWhat would you like to adjust?")
                print("1. Genres")
                print("2. Time period")
                print("3. Mood")
                choice = input("Enter your choice (1-3): ")
                
                if choice == "1":
                    genres_input = input("Enter new genres separated by commas: ").lower()
                    self.user_preferences["genres"] = [genre.strip() for genre in genres_input.split(",")]
                elif choice == "2":
                    year_input = input("Enter new time period: ").lower()
                    self.parse_year_preference(year_input)
                elif choice == "3":
                    mood = input("Enter new mood: ").lower()
                    if mood in self.mood_to_genre:
                        self.user_preferences["mood"] = mood
            
            # Get new recommendations
            recommendations = self.get_recommendations()
            self.display_recommendations(recommendations)


if __name__ == "__main__":
    recommender = MovieRecommender()
    recommender.run()
````

## Requirements File

Here's a `requirements.txt` file for your project:

````python
# No external dependencies required for this project
# Standard Python libraries only
````

## How the Code Works

This rule-based movie recommendation system:

1. **Initializes with a movie database** - Either loads from a JSON file or creates a sample database
2. **Collects user preferences** - Asks about genres, years, runtime, mood, and favorite actors/directors
3. **Processes inputs using rules** - Parses time periods and converts moods into related genres
4. **Scores movies** - Each movie gets points based on how well it matches preferences
5. **Generates recommendations** - Returns the highest-scoring movies with explanations
6. **Provides feedback mechanism** - Allows users to refine their preferences

The system applies several rules:
- Genre matching (direct and mood-based)
- Year/time period matching
- Runtime preference matching
- Actor/director matching
- Previously recommended movies are penalized

The scoring system makes this more than a simple filter - it ranks movies by how well they match all criteria combined, providing personalized recommendations without requiring machine learning.