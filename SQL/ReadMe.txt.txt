
Sqlbolt https://sqlbolt.com

Day 1:
Id	Title	Director	Year	Length_minutes

Find the title of each film ✓
SELECT Title  FROM movies;

Find the director of each film ✓
SELECT Director  FROM movies;

Find the title and director of each film ✓
SELECT Title, Director  FROM movies;

Find the title and year of each film ✓
SELECT Title, Year  FROM movies;

Find all the information about each film 
SELECT *  FROM movies;

==========================================================================
Day 2:
Find the movie with a row id of 6
SELECT *  FROM movies
WHERE Id=6;

Find the movies released in the years between 2000 and 2010
SELECT *  FROM movies
WHERE Year>=2000 AND Year<=2010;

Find the movies not released in the years between 2000 and 2010
SELECT *  FROM movies
WHERE Year NOT BETWEEN 2000 AND 2010;

Find the first 5 Pixar movies and their release year
SELECT title, year FROM movies
WHERE year <= 2003;

==========================================================================

Day 3:

Find all the Toy Story movies
SELECT * FROM movies
WHERE Title LIKE 'Toy%'

Find all the movies directed by John Lasseter
SELECT * FROM movies
WHERE Director='John Lasseter';

Find all the movies (and director) not directed by John Lasseter
SELECT * FROM movies
WHERE NOT Director='John Lasseter';

Find all the WALL-* movies
SELECT * FROM movies
WHERE Title LIKE "WALL-%"

==========================================================================

Day 4:
List all directors of Pixar movies (alphabetically), without duplicates ✓

SELECT DISTINCT director FROM movies
ORDER BY director ASC;

List the last four Pixar movies released (ordered from most recent to least)
SELECT * FROM Movies
ORDER BY Year DESC
LIMIT 4;

List the first five Pixar movies sorted alphabetically
SELECT * FROM Movies
ORDER BY Title ASC
LIMIT 5;

List the next five Pixar movies sorted alphabetically
SELECT * FROM Movies
ORDER BY Title ASC
LIMIT 5 OFFSET 5

==========================================================================

Day 5:
City	Country	Population	Latitude	Longitude

List all the Canadian cities and their populations
SELECT * FROM north_american_cities
WHERE Country='Canada'

Order all the cities in the United States by their latitude from north to south
SELECT * FROM north_american_cities
WHERE Country='United States'
ORDER BY Latitude DESC

List all the cities west of Chicago, ordered from west to east
SELECT city, longitude FROM north_american_cities
WHERE longitude < -87.629798
ORDER BY longitude ASC;

List the two largest cities in Mexico (by population)
SELECT city, population FROM north_american_cities
WHERE country="Mexico"
ORDER BY population DESC
LIMIT 2;

List the third and fourth largest cities (by population) in the United States and their population
SELECT city, population FROM north_american_cities
WHERE country="United States"
ORDER BY population DESC
LIMIT 2 OFFSET 2;

==========================================================================

Day 6:
Id	Title	Director	Year	Length_minutes

Movie_id	Rating	Domestic_sales	International_sales

Find the domestic and international sales for each movie
SELECT Title, Domestic_sales,International_sales FROM Movies
INNER JOIN Boxoffice  
    ON Movies.Id = Boxoffice.Movie_id


Show the sales numbers for each movie that did better internationally rather than domestically
SELECT Title, Domestic_sales,International_sales FROM Movies
INNER JOIN Boxoffice  
    ON Movies.Id = Boxoffice.Movie_id
    WHERE International_sales > Domestic_sales

List all the movies by their ratings in descending order
SELECT Title, Domestic_sales,International_sales FROM Movies
INNER JOIN Boxoffice  
    ON Movies.Id = Boxoffice.Movie_id
    ORDER BY Rating DESC

==========================================================================

Day 7:
Building_name	Capacity
Role	Name	Building	Years_employed

Find the list of all buildings that have employees (Employees , Buildings )
SELECT DISTINCT building FROM employees;

Find the list of all buildings and their capacity
SELECT * FROM Buildings;

List all buildings and the distinct employee roles in each building (including empty buildings)
SELECT DISTINCT building_name, role 
FROM buildings 
  LEFT JOIN employees
    ON building_name = building;

==========================================================================


Day 8:
Find the name and role of all employees who have not been assigned to a building ✓
SELECT Name, Role FROM employees
WHERE Years_employed=0;


Find the names of the buildings that hold no employees
SELECT DISTINCT building_name
FROM buildings 
  LEFT JOIN employees
    ON building_name = building
WHERE role IS NULL;

==========================================================================

Day 9:
List all movies and their combined sales in millions of dollars
SELECT title, (domestic_sales + international_sales) / 1000000 AS gross_sales_millions
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id;

List all movies and their ratings in percent
SELECT title, (Rating)*10
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id;

List all movies that were released on even number years
SELECT title, Year
FROM movies
WHERE Year%2=0

==========================================================================

Day 10:

Find the longest time that an employee has been at the studio ✓
SELECT MAX(Years_employed) FROM employees;

For each role, find the average number of years employed by employees in that role
SELECT Role,AVG(Years_employed) FROM employees
GROUP BY Role;

Find the total number of employee years worked in each building
SELECT building, SUM(years_employed) as Total_years_employed
FROM employees
GROUP BY building;

==========================================================================
Day 11:

Find the number of Artists in the studio (without a HAVING clause) ✓

SELECT COUNT(*) FROM employees
WHERE Role='Artist'

Find the number of Employees of each role in the studio
SELECT Role, COUNT(*) FROM employees
GROUP BY Role

Find the total number of years employed by all Engineers
SELECT role, SUM(years_employed)
FROM employees
GROUP BY role
HAVING role = "Engineer";

==========================================================================

Day 12:
Find the number of movies each director has directed ✓
SELECT Director,COUNT(*) FROM movies
GROUP BY Director;

Find the total domestic and international sales that can be attributed to each director
SELECT Director, SUM(Domestic_sales)+ SUM(International_sales) 
FROM movies
INNER JOIN Boxoffice 
ON Id=Movie_id
GROUP BY Director;

==========================================================================



