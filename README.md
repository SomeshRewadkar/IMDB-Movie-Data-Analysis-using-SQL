# IMDb Movie Data Analysis using SQL

## Project Overview
This project involves analyzing IMDb movie data using SQL to gain insights into various aspects of the film industry, such as top-rated movies, popular genres, director performance, and revenue trends.

## Dataset
The dataset includes information about movies, directors, actors, genres, ratings, and box office collections. It is structured in multiple tables:

- **movies** (movie_id, title, release_year, duration, genre, director_id, budget, revenue)
- **directors** (director_id, name, country)
- **actors** (actor_id, name, birth_year, nationality)
- **movie_actors** (movie_id, actor_id, role)
- **ratings** (movie_id, average_rating, votes)

## Objectives
- Identify the highest-rated movies.
- Find the most popular genres based on average ratings.
- Determine top-performing directors.
- Analyze the relationship between budget and revenue.
- Identify trends in movie production over time.

## SQL Queries
Some key SQL queries used in this analysis:

### 1. Top 10 Highest Rated Movies
```sql
SELECT title, average_rating, votes 
FROM movies m 
JOIN ratings r ON m.movie_id = r.movie_id 
ORDER BY average_rating DESC, votes DESC 
LIMIT 10;
```

### 2. Most Popular Genres
```sql
SELECT genre, AVG(average_rating) AS avg_rating 
FROM movies m 
JOIN ratings r ON m.movie_id = r.movie_id 
GROUP BY genre 
ORDER BY avg_rating DESC;
```

### 3. Top Directors by Average Movie Rating
```sql
SELECT d.name, AVG(r.average_rating) AS avg_director_rating 
FROM directors d 
JOIN movies m ON d.director_id = m.director_id 
JOIN ratings r ON m.movie_id = r.movie_id 
GROUP BY d.name 
ORDER BY avg_director_rating DESC 
LIMIT 10;
```

### 4. Budget vs. Revenue Analysis
```sql
SELECT title, budget, revenue, (revenue - budget) AS profit 
FROM movies 
WHERE budget > 0 AND revenue > 0 
ORDER BY profit DESC;
```

### 5. Number of Movies Released Per Year
```sql
SELECT release_year, COUNT(*) AS movie_count 
FROM movies 
GROUP BY release_year 
ORDER BY release_year;
```

## Tools Used
- **Database**: MySQL
- **Query Execution**: SQL Workbench 

## Results & Insights
- The highest-rated movies tend to have a high number of votes, indicating audience engagement.
- Some genres consistently perform well in ratings, such as drama and thrillers.
- A few directors have consistently high-rated movies, proving their strong influence in the industry.
- Budget and revenue correlation shows that high-budget movies often generate more profit, but not always.
- Movie production trends show fluctuations over the years, with peaks during certain decades.

## Future Improvements
- Expand the dataset to include more years and international films.
- Integrate additional data sources like streaming performance.
- Use machine learning for predictive analysis on box office success.

## Conclusion
SQL is a powerful tool for analyzing movie data, helping us uncover valuable trends and insights in the film industry.
