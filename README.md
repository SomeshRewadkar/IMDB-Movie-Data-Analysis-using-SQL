# IMDb Movie Data Analysis using SQL

## Project Overview
This project involves analyzing IMDb movie data using SQL to gain insights into various aspects of the film industry, such as top-rated movies, popular genres, director performance, and revenue trends.

## Dataset
The dataset includes information about movies, genres, directors, actors, and box office collections. It is structured in multiple tables:

- **movie** (id, title, year, date_published, duration, country, worldwide_gross_income, languages, production_company)
- **genre** (movie_id, genre)
- **director_mapping** (movie_id, director_id)
- **director** (id, name)
- **actor_mapping** (movie_id, actor_id)
- **actor** (id, name, birth_year)
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
FROM movie m 
JOIN ratings r ON m.id = r.movie_id 
ORDER BY average_rating DESC, votes DESC 
LIMIT 10;
```

### 2. Most Popular Genres
```sql
SELECT g.genre, AVG(r.average_rating) AS avg_rating 
FROM genre g 
JOIN ratings r ON g.movie_id = r.movie_id 
GROUP BY g.genre 
ORDER BY avg_rating DESC;
```

### 3. Top Directors by Average Movie Rating
```sql
SELECT d.name, AVG(r.average_rating) AS avg_director_rating 
FROM director d 
JOIN director_mapping dm ON d.id = dm.director_id 
JOIN movie m ON dm.movie_id = m.id 
JOIN ratings r ON m.id = r.movie_id 
GROUP BY d.name 
ORDER BY avg_director_rating DESC 
LIMIT 10;
```

### 4. Revenue Analysis
```sql
SELECT title, worldwide_gross_income 
FROM movie 
WHERE worldwide_gross_income IS NOT NULL 
ORDER BY worldwide_gross_income DESC;
```

### 5. Number of Movies Released Per Year
```sql
SELECT year, COUNT(*) AS movie_count 
FROM movie 
GROUP BY year 
ORDER BY year;
```

## Tools Used
- **Database**: MySQL
- **Query Execution**: SQL Workbench / Jupyter Notebook with SQL extensions

## Results & Insights
- The highest-rated movies tend to have a high number of votes, indicating audience engagement.
- Some genres consistently perform well in ratings, such as drama and thrillers.
- A few directors have consistently high-rated movies, proving their strong influence in the industry.
- Movie production trends show fluctuations over the years, with peaks during certain decades.

## Future Improvements
- Expand the dataset to include more years and international films.
- Integrate additional data sources like streaming performance.
- Use machine learning for predictive analysis on box office success.

## Conclusion
SQL is a powerful tool for analyzing movie data, helping us uncover valuable trends and insights in the film industry.
