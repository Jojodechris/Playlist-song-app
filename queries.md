Make sure you download the starter code and run the following:

```sh
  psql < movies.sql
  psql movies_db
```

In markdown, you can place a code block inside of three backticks (```) followed by the syntax highlighting you want, for example

\```sql

SELECT \* FROM users;

\```

Using the `movies_db` database, write the correct SQL queries for each of these tasks:

1.  The title of every movie.
SELECT * title FROM movie;


2.  All information on the G-rated movies.
SELECT * FROM movie WHERE rating = 'G';

3.  The title and release year of every movie, ordered with the
    oldest movie first.
    SELECT title,release_year FROM movie;

4.  All information on the 5 longest movies.

SELECT * FROM(
SELECT title, release_year,runtime,rating DENSE_RANK() 
over(ORDER BY runtime desc) As alias_for_nested_query FROM movie) As alias_for_first_query
WHERE alias_for_nested_query=5;


5.  A query that returns the columns of `rating` and `total`, tabulating the
    total number of G, PG, PG-13, and R-rated movies.
SELECT rating, COUNT(*) AS total
FROM movies
GROUP BY rating
ORDER BY rating;


6.  A table with columns of `release_year` and `average_runtime`,
    tabulating the average runtime by year for every movie in the database. The data should be in reverse chronological order (i.e. the most recent year should be first).
SELECT release_year, AVG(runtime) AS average_runtime
FROM movies
GROUP BY release_year
ORDER BY release_year DESC;


7.  The movie title and studio name for every movie in the
    database.
SELECT m.title, s.name AS studio_name
FROM movies m
JOIN studios s ON m.studio_id = s.id;



8.  The star first name, star last name, and movie title for every
    matching movie and star pair in the database.
SELECT st.first_name, st.last_name, m.title
FROM stars st
JOIN roles r ON st.id = r.star_id
JOIN movies m ON r.movie_id = m.id;



9.  The first and last names of every star who has been in a G-rated movie. The first and last name should appear only once for each star, even if they are in several G-rated movies. *IMPORTANT NOTE*: it's possible that there can be two *different* actors with the same name, so make sure your solution accounts for that.
SELECT DISTINCT st.first_name, st.last_name
FROM stars st
JOIN roles r ON st.id = r.star_id
JOIN movies m ON r.movie_id = m.id
WHERE m.rating = 'G';


10. The first and last names of every star along with the number
    of movies they have been in, in descending order by the number of movies. (Similar to #9, make sure
    that two different actors with the same name are considered separately).
SELECT DISTINCT st.first_name, st.last_name
FROM stars st
JOIN roles r ON st.id = r.star_id
JOIN movies m ON r.movie_id = m.id
WHERE m.rating = 'G';

### The rest of these are bonuses

11. The title of every movie along with the number of stars in
    that movie, in descending order by the number of stars.
SELECT m.title, COUNT(r.star_id) AS star_count
FROM movies m
LEFT JOIN roles r ON m.id = r.movie_id
GROUP BY m.title
ORDER BY star_count DESC;

12. The first name, last name, and average runtime of the five
    stars whose movies have the longest average.
SELECT st.first_name, st.last_name, AVG(m.runtime) AS avg_runtime
FROM stars st
JOIN roles r ON st.id = r.star_id
JOIN movies m ON r.movie_id = m.id
GROUP BY st.first_name, st.last_name
ORDER BY avg_runtime DESC
LIMIT 5;

13. The first name, last name, and average runtime of the five
    stars whose movies have the longest average, among stars who have more than one movie in the database.
WITH star_avg_runtime AS (
  SELECT st.id, st.first_name, st.last_name, AVG(m.runtime) AS avg_runtime
  FROM stars st
  JOIN roles r ON st.id = r.star_id
  JOIN movies m ON r.movie_id = m.id
  GROUP BY st.id, st.first_name, st.last_name
  HAVING COUNT(m.id) > 1
)
SELECT first_name, last_name, avg_runtime
FROM star_avg_runtime
ORDER BY avg_runtime DESC
LIMIT 5;

14. The titles of all movies that don't feature any stars in our
    database.
SELECT title
FROM movies
WHERE id NOT IN (SELECT DISTINCT movie_id FROM roles);

15. The first and last names of all stars that don't appear in any movies in our database.
SELECT first_name, last_name
FROM stars
WHERE id NOT IN (SELECT DISTINCT star_id FROM roles);

16. The first names, last names, and titles corresponding to every
    role in the database, along with every movie title that doesn't have a star, and the first and last names of every star not in a movie.
SELECT st.first_name, st.last_name, m.title
FROM stars st
JOIN roles r ON st.id = r.star_id
JOIN movies m ON r.movie_id = m.id
UNION ALL
SELECT NULL AS first_name, NULL AS last_name, m.title
FROM movies m
WHERE m.id NOT IN (SELECT DISTINCT movie_id FROM roles)
UNION ALL
SELECT st.first_name, st.last_name, NULL AS title
FROM stars st
WHERE st.id NOT IN (SELECT DISTINCT star_id FROM roles);
