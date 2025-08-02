# SQL-case-study-portfolio
A portfolio of SQL projects demonstrating beginner to advanced analytics skills.

As part of my journey to deepen my SQL expertise for data analytics, I completed a hands-on project that explored a range of real-world business problems using structured queries.

This portfolio demonstrates my ability to:

Filter and manipulate complex datasets
Join multiple tables and use CTEs
Perform aggregations, subqueries, and profitability analysis
Draw insights from both entertainment and retail-based data models

📁 Project Structure & Key Questions Solved

Q- How can you find the movies with the highest and lowest IMDb ratings?
Q- How would you use pattern matching to search for movies with specific keywords in the title?
Q- How would you filter movies based on industry and release year criteria?
Q- How do you calculate profit from movie financials using SQL expressions?
Q- How can you join fact and dimension tables to perform advanced sales analytics?
Q- How do you aggregate and group data to derive meaningful business metrics?
Q- How do you use subqueries to find records with extreme values in a dataset?

select title, release_year from movies	where studio= 'Marvel Studios';
select title from movies where title like '%Avenger%';
select title, release_year from movies where title='The Godfather';
select distinct(studio) from movies where industry ='Bollywood';

select * from movies where imdb_rating>=9;
select * from movies where release_year in (2018,2019,2022);
select * from movies where studio in ("marvel studios", "ZEE Studios");
select * from movies where imdb_rating is not null;
      
select * from movies where imdb_rating between 5 and 9;
select * from movies where industry="bollywood"	
order by imdb_rating desc limit 5;
select * from movies where industry="hollywood"
order by imdb_rating desc limit 5 offset 1;

select * from movies
order by release_year desc;
select * from movies where release_year=2022;
select * from movies where release_year>2020;
select * from movies where release_year>2020 and imdb_rating>8;
select * from movies where studio="Marvel studios" or studio="Hombale Films";
select * from movies where title like '%Thor%' order by release_year;
select * from movies where studio <>"Marvel studios";

select round(avg(imdb_rating),2) from movies where studio="Marvel Studios";
select  min(imdb_rating) as min_rating,
max(imdb_rating) as max_rating,
round(avg(imdb_rating),2) as avg_rating from movies where studio="marvel studios";
select count(*) from movies where industry="bollywood";
select industry, count(*) title from movies -- where industry in ('hollywood','bollywood')
group by industry;
select studio, count(*), round(avg(imdb_rating),2) as avg_rating from movies where studio !=""
group by studio
order by avg_rating desc;

select release_year, count(*) from movies where release_year between 2015 and 2022
group by release_year;
select max(release_year), min(release_year) from movies;
select release_year, count(release_year) as total_movies from movies
group by release_year
order by release_year desc;

select release_year, count(*) as total_movies from movies
group by release_year
having total_movies>2;

select *, year(curdate())-birth_year as Age from actors;
select *, 
CASE
WHEN UNIT='BILLIONS' THEN REVENUE*1000
WHEN UNIT='THOUSANDS'THEN REVENUE/1000
WHEN unit='MILLIONS' THEN revenue
END as revenue_MILN
from financials;
SELECT * FROM FINANCIALS;
SELECT *,
((revenue-budget)/budget)*100 AS PROFIT FROM financials;

SELECT COUNT(distinct IMDB_RATING) FROM MOVIES;
SELECT stddev(IMDB_RATING) FROM movies;

SELECT * FROM CUSTOMERS WHERE CUSTOMERS_ID;
SELECT * FROM PLAYERS order by DESC LIMIT 3 OFFSET 1;
SELECT * FROM MOVIES WHERE title like "THE%" AND IMdb_rating>5 and imdb_rating<=6;

select * from moviesdb.movies
cross join moviesdb.financials



Q- How can you find the movies with the highest and lowest IMDb ratings?
Q- How can Common Table Expressions (CTEs) be used to structure complex queries in a clean and readable way?
Q- How can you join fact and dimension tables to perform advanced sales analytics?
Q- How do you use subqueries to find records with extreme values in a dataset?

select * from movies where imdb_rating= (select max(imdb_rating) from movies);
----- movie with min & max imdb
select * from movies where imdb_rating in ((select min(imdb_rating) from movies) , (select max(imdb_rating) from movies));

# SELECT ALL ACTORS WHOSE AGE >70 AND < 85
select * from
(SELECT name , year(curdate())- birth_year as yrs 
FROM actors) as actor_age
where yrs>70 and yrs<85;

##select actors who acted in any of movies (101 110 121)
select * from movie_actor;
select * from movies;
select * from actors;

select * from
(select m.movie_id, m.title, ma.actor_id, a.name
from movies m
left join movie_actor ma
on m.movie_id=ma.movie_id
left join actors a 
on ma.actor_id=a.actor_id) as main
where main.movie_id in (101,110,121);

select * from actors where actor_id= any (
select actor_id from movie_actor where movie_id in (101,110,121))

SELECT title, industry FROM moviesdb.movies;
select count(*) from movies where industry= 'bollywood';
select distinct (industry) from movies where industry= 'hollywood';

select title, release_year from movies	where studio= 'Marvel Studios';
select title from movies where title like '%Avenger%';
select title, release_year from movies where title='The Godfather';
select distinct(studio) from movies where industry ='Bollywood';

select * from movies where imdb_rating>=9;
select * from movies where release_year in (2018,2019,2022);
select * from movies where studio in ("marvel studios", "ZEE Studios");
select * from movies where imdb_rating is not null;
      
select * from movies where imdb_rating between 5 and 9;
select * from movies where industry="bollywood"	
order by imdb_rating desc limit 5;
select * from movies where industry="hollywood"
order by imdb_rating desc limit 5 offset 1;

select * from movies
order by release_year desc;
select * from movies where release_year=2022;
select * from movies where release_year>2020;
select * from movies where release_year>2020 and imdb_rating>8;
select * from movies where studio="Marvel studios" or studio="Hombale Films";
select * from movies where title like '%Thor%' order by release_year;
select * from movies where studio <>"Marvel studios";

select round(avg(imdb_rating),2) from movies where studio="Marvel Studios";
select  min(imdb_rating) as min_rating,
max(imdb_rating) as max_rating,
round(avg(imdb_rating),2) as avg_rating from movies where studio="marvel studios";
select count(*) from movies where industry="bollywood";
select industry, count(*) title from movies -- where industry in ('hollywood','bollywood')
group by industry;
select studio, count(*), round(avg(imdb_rating),2) as avg_rating from movies where studio !=""
group by studio
order by avg_rating desc;

select release_year, count(*) from movies where release_year between 2015 and 2022
group by release_year;
select max(release_year), min(release_year) from movies;
select release_year, count(release_year) as total_movies from movies
group by release_year
order by release_year desc;

select release_year, count(*) as total_movies from movies
group by release_year
having total_movies>2;

select *, year(curdate())-birth_year as Age from actors;
select *, 
CASE
WHEN UNIT='BILLIONS' THEN REVENUE*1000
WHEN UNIT='THOUSANDS'THEN REVENUE/1000
WHEN unit='MILLIONS' THEN revenue
END as revenue_MILN
from financials;
SELECT * FROM FINANCIALS;
SELECT *,
((revenue-budget)/budget)*100 AS PROFIT FROM financials;

SELECT COUNT(distinct IMDB_RATING) FROM MOVIES;
SELECT stddev(IMDB_RATING) FROM movies;

SELECT * FROM CUSTOMERS WHERE CUSTOMERS_ID;
SELECT * FROM PLAYERS order by DESC LIMIT 3 OFFSET 1;
SELECT * FROM MOVIES WHERE title like "THE%" AND IMdb_rating>5 and imdb_rating<=6;

select * from moviesdb.movies
cross join moviesdb.financials
select * from movies;
select * from financials;

select movies.movie_id, movies.title, financials.budget, financials.revenue, financials.currency, financials.unit
from movies
left join financials
on movies.movie_id=financials.movie_id

union
select movies.movie_id, movies.title, financials.budget, financials.revenue, financials.currency, financials.unit
from movies
right join financials
on movies.movie_id=financials.movie_id;

select * from movies;
select * from languages;


select m.language_id, m.title, l.name
from movies m
left join languages l
on m.language_id=l.language_id
union
select m.language_id, m.title, l.name
from movies m
right join languages l
on m.language_id=l.language_id;


select m.title, m.language_id, l.name
from movies m 
left join languages l
on m.language_id=l.language_id
where l.name='Telugu';

select l.name, count(m.title), m.language_id
from movies m 
left join languages l
on m.language_id=l.language_id
group by l.name, m.language_id
