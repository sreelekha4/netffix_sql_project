# Netflix Movies and TV Shows Data Analysis using SQL

![](https://github.com/sreelekha4/netffix_sql_project/blob/main/netflix%20image.jpg)

## Overview
This project is about analysis of Netflix's movies and TV shows data using SQL. The goal is to find useful insights and answer business-related questions based on the dataset. This README explains the project's goals, business questions, solutions, key findings, and conclusions in detail.

## Objectives

- Analyze the distribution of content types (movies vs TV shows).
- Find the most common ratings for movies and TV shows.
- List and analyze content based on release years, countries, and durations.
- Analyze and group content based on specific criteria and keywords.

## Dataset

The data for this project is sourced from the Kaggle dataset:

- **Dataset Link:** [Movies Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)

## Schema

```sql
DROP TABLE IF EXISTS netflix;
CREATE TABLE netflix
(
    show_id      VARCHAR(5),
    type         VARCHAR(10),
    title        VARCHAR(250),
    director     VARCHAR(550),
    cast        VARCHAR(1050),
    country      VARCHAR(550),
    date_added   VARCHAR(55),
    release_year INT,
    rating       VARCHAR(15),
    duration     VARCHAR(15),
    listed_in    VARCHAR(250),
    description  VARCHAR(550)
);
```

## Business Problems and Solutions

### 1. Count the Number of Movies vs TV Shows

```sql
SELECT 
    type,
    COUNT(*) as COUNT
FROM netflix
GROUP BY type;
```

**Objective:** Determine the distribution of content types on Netflix.

### 2. Find the Rating for Movies and TV Shows

```sql
SELECT 
    type,
    rating,
    COUNT(*) AS rating_count
    FROM netflix
    GROUP BY type, rating
```

**Objective:** Identify the most frequently occurring rating for each type of content.

### 3. List All Movies Released in a Specific Year (e.g., 2020)

```sql
SELECT * 
FROM netflix
WHERE release_year = 2020;
```

**Objective:** Retrieve all movies released in a specific year.
### 4. find Content Added within the past 5 Years

```sql
SELECT *
FROM netflix
WHERE year(date_added) >= year(getdate())-5;
```

**Objective:** find content added to Netflix in the past 5 years.

### 5. Find All Movies/TV Shows by Director 'Rajiv Chilaka'

```sql
SELECT *
FROM netflix
WHERE director_name = 'Rajiv Chilaka';
```

**Objective:** List all content directed by 'Rajiv Chilaka'.

### 6. List All TV Shows with 5 Seasons

```sql
select * 
from netflix
where duration='5 seasons';
```

**Objective:** Identify TV shows with 5 seasons.

### 7. Count the Number of Content Items in Each Genre

```sql
SELECT 
    listed_in as genre,
    COUNT(*) as total_content
FROM netflix
GROUP BY listed_in;
```
###

**Objective:** Count the number of content items in each genre.

### 8. List All Movies that are Documentaries

```sql
SELECT * 
FROM netflix
WHERE listed_in LIKE '%Documentaries';
```

**Objective:** Retrieve all movies classified as documentaries.

### 9. Find All Content Without a Director

```sql
SELECT * 
FROM netflix
WHERE director IS NULL;
```

**Objective:** List content that does not have a director.

### 10. Find How Many Movies Actor 'Salman Khan' Appeared in the Last 10 Years

```sql
SELECT * 
FROM netflix
WHERE casts LIKE '%Salman Khan%'
  AND release_year > year(getdate())-10;
```

**Objective:** Count the number of movies featuring 'Salman Khan' in the last 10 years.

### 11. Categorize Content Based on the Presence of 'Kill' and 'Violence' Keywords

```sql
SELECT 
    category,
    COUNT(*) AS content_count
FROM (
    SELECT 
        CASE 
            WHEN description ILIKE '%kill%' OR description ILIKE '%violence%' THEN 'Bad'
            ELSE 'Good'
        END AS category
    FROM netflix
) AS categorized_content
GROUP BY category;
```

**Objective:** Categorize content as 'Bad' if it contains 'kill' or 'violence' and 'Good' otherwise. Count the number of items in each category.

## Findings and Conclusion

- **Content Distribution:** The dataset contains a variety range of movies and TV shows with varying ratings and genres.
- **Common Ratings:** Insights into the most common ratings provide an understanding of the content's target audience.
- **Geographical Insights:** The top countries and the average content releases by India highlight regional content distribution.
- **Content Categorization:** Categorizing content based on specific keywords helps in understanding the nature of content available on Netflix.

This analysis provides a comprehensive view of Netflix's content and can help inform content strategy and decision-making.
