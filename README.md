# SQL-case-study-portfolio
A portfolio of SQL projects demonstrating beginner to advanced analytics skills.
-- Assumed Database Tables  
  -  fct_order: order_id | order_timestamp | user_id | vertical | location_id
dim_location: location_id | area | city | country
dim_date: date | month | year

Multi Vertical users
P1: Count of Active Users who have placed at least 1 order in the past 90 days from each vertical per Country
Expected Output: Country, MVA_users_count

WITH recent_orders AS (
SELECT user_id, country, vertical
from fct_order
JOIN dim_location 1 ON location_id= 1.location_id
where
order_timestamp >= CURRENT_DATE - INTERVAL '90 days'
GROUP BY user_id, country, vertical),
multi_vertical_users AS (
SELECT user_id, country, COUNT(DISTINCT vertical) AS vertical_count
FROM recent_orders
GROUP BY user_id, country
HAVING COUNT (Distinct vertical)>1)
SELECT country, COUNT (DISTINCT user_id) AS MVA_users_count
FROM multi_vertical_users
GROUP BY country

WITH date_series AS (
SELECT date 
from dim_date
where date >= '2024-01-01' ),
recent orders AS (
SELECT user_id, country, vertical, 
MVA_users_count
from date_series 
LEFT Join multi_vertical_users mv 
ON mv.order
select * 
from parks_and_recreation.employee_demographics
where gender NOT LIKE '%Female%'
;
SELECT gender, avg(age), max(age)
from parks_and_recreation.employee_demographics
group by 1;

select *
from parks_and_recreation.employee_demographics
order by gender, age;

select gender, avg(age)
from parks_and_recreation.employee_demographics
group by gender
having avg(age) > 40;

select occupation, avg(salary)
from parks_and_recreation.employee_salary
where occupation like '%manager%'
group by occupation;

select *
from parks_and_recreation.employee_demographics
limit 3;

SELECT *
FROM SQLTutorial.dbo.employee_demographics

select * 
from parks_and_recreation.employee_demographics
where gender NOT LIKE '%Female%'
;
SELECT gender, avg(age), max(age)
from parks_and_recreation.employee_demographics
group by 1;

select *
from parks_and_recreation.employee_demographics
order by gender, age;

select gender, avg(age)
from parks_and_recreation.employee_demographics
group by gender
having avg(age) > 40;

select occupation, avg(salary)
from parks_and_recreation.employee_salary
where occupation like '%manager%'
group by occupation;

select *
from parks_and_recreation.employee_demographics
limit 3;

SELECT *
FROM SQLTutorial.dbo.employee_demographics


-- Assumed Database Tables  
  -  fct_order: order_id | order_timestamp | user_id | vertical | location_id
dim_location: location_id | area | city | country
dim_date: date | month | year

Multi Vertical users
P1: Count of Active Users who have placed at least 1 order in the past 90 days from each vertical per Country
Expected Output: Country, MVA_users_count

WITH recent_orders AS (
SELECT user_id, country, vertical
from fct_order
JOIN dim_location 1 ON location_id= 1.location_id
where
order_timestamp >= CURRENT_DATE - INTERVAL '90 days'
GROUP BY user_id, country, vertical),
multi_vertical_users AS (
SELECT user_id, country, COUNT(DISTINCT vertical) AS vertical_count
FROM recent_orders
GROUP BY user_id, country
HAVING COUNT (Distinct vertical)>1)
SELECT country, COUNT (DISTINCT user_id) AS MVA_users_count
FROM multi_vertical_users
GROUP BY country

WITH date_series AS (
SELECT date 
from dim_date
where date >= '2024-01-01' ),
recent orders AS (
SELECT user_id, country, vertical, 
MVA_users_count
from date_series 
LEFT Join multi_vertical_users mv 
ON mv.order

select * from sales;
select SaleDate, Amount, Customers
from sales;
select SaleDate, amount, Boxes, amount/Boxes as 'amount per box' from sales;
select *
 from sales 
 where Amount>10000
 order by amount;
 select * from sales
 where GeoID='G1'
 order by PID, Amount DESC;
 
 SELECT * FROM SALES
 WHERE amount>10000 and saledate >= '2022-01-01';
 
 select amount, saledate from sales
 where Amount>10000 and year(saledate)=2022;
 
 select * from sales 
 where Boxes between 0 and 50
 >0 and Boxes<= 50;
 
 
 select * from people;
 
 select * from people;
 
 select * from people where Team = 'delish' or 'yummies'
 
 select * from people
 where team in ('delish', 'jucies');
 select SaleDate, Amount,
	case when amount <1000 then 'Under 1k'
		when amount<5000 then 'Under 5k'
        when amount<10000 then 'Under 10k'
        else '10k or more'
        end as 'Amount category'
  from sales;
 
 select * from sales;
 select * from people;
  
 select  S.SPID, S.Amount, S.SaleDate, P.Salesperson
 from sales as S
 JOIN people AS P ON P.SPID=S.SPID;
 
 SELECT * FROM products;
  select * from sales;
   select * from people;
  
SELECT S.SaleDate, S.Amount, S.PID, P.Product
FROM SALES AS S
JOIN products AS P ON P.PID=S.PID;
  
 SELECT S.SPID, S.SALESDATE, S.AMOUNT, P.SALESPERSON
 FROM SALES AS S
JOIN PEOPLE AS P ON P.SPID=S.SPID
LEFT JOIN products AS PR ON PR.PID=S.PID;

SELECT geoID, sum(AMOUNT) 
FROM SALES
group by GEOID;

select * from actors where actor_id = any (
select actor_id from movie_actor where movie_id in (101,110,121));

##movie rating > any of the marvel movie
select * from movies where studio not like 'Marvel studios' and imdb_rating>'8.4'
order by imdb_rating desc;

##select actor id actor name and total nos of movies they acted in 
select * from actors;
select * from movie_actor;
select * from movies;

select 
	actor_id, 
    name,
    (select count(*) from movie_actor
    where actor_id=actors.actor_id) as movies_count
    from actors ;
    
    select * from movies where release_year in(
    (select min(release_year) from movies), (select max(release_year) from movies));
    
    ##select all rows from movies whose imdb rating is higher than the average rating
    select * from movies where imdb_rating > (
    select avg(imdb_rating) from movies) ;
    
explain analyze
select a.actor_id, a.name, count(*) as movies_count from movie_actor ma
join actors a
on a.actor_id=ma.actor_id
group by a.actor_id
order by movies_count desc;
  
##get all actors between age 70 and 85
select * from movie_actor;
select actor_name, age from (
select name as actor_name, (year(curdate())-birth_year) as age from actors) as actor_age where age >70 and age<85;
  
 with actor_age as(select name as actor_name, (year(curdate())-birth_year) as age from actors) 
  select actor_name, age from actor_age where age>;

WITH actors_age AS (  select name as actor_name, (year(curdate())-birth_year) as age from actors)
select actor_name, age FROM actors_age where age >70 and age<85;

##movies that produce 500 % profit and their rating was less than avg rating for all movies;
select * from movies;
select * from financials;

WITH x AS(
select 
	*, 	
    (revenue-budget)*100/budget as pft_percent 
    from financials
    where (revenue-budget)*100/budget>=500),
 y AS(
select * from movies
where	imdb_rating<(select avg(imdb_rating) from movies)
)

select x.pft_percent, x.movie_id,
	y.title, y.imdb_rating
 from x
join y
on x.movie_id=y.movie_id


##using sub query
select M.pft_percent, M.movie_id,
	F.title, F.imdb_rating
from (select 
	*, 	
    (revenue-budget)*100/budget as pft_percent 
    from financials
    where (revenue-budget)*100/budget>=500) M
join (select * from movies
where	imdb_rating<(select avg(imdb_rating) from movies)
) F 
ON M.movie_id=F.movie_id;

##all hollywood movies after 2000
select * from movies where release_year>2000
##made pft equal to and more than 500 milliom

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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies

SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code

SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

[UpSELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_codeloading 13.sql…]()
SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;

SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date

SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2

-- DATA CLEANING--

select *
from layoffs;

-- remove duplicates
-- standardize the data
-- null or blank values
-- remove any columns --

CREATE TABLE layoffs_staging
LIKE layoffs;

select *
from layoffs_staging;

INSERT layoffs_staging
SELECT *
FROM layoffs;

select *
from layoffs_staging;

-- for dupe --

select *,
ROW_NUMBER() OVER(
PARTITION BY company, industry, total_laid_off, percentage_laid_off, 'date') AS row_num
from layoffs_staging;

WITH duplicate_cte AS
(
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging
)
SELECT
FROM duplicate_cte
WHERE row_num > 1;

SELECT *
from layoffs_staging
where company= 'Casper';



CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SELECT *
from layoffs_staging2
WHERE row_num > 1;
INSERT INTO layoffs_staging2
select *,
ROW_NUMBER() OVER(
PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, 'date', stage, country, funds_raised_millions) AS row_num
from layoffs_staging;

DELETE
from layoffs_staging2
WHERE row_num > 1;

SELECT *
from layoffs_staging2;





-- STANDARDIZING data --

SELECT company, TRIM(company)
FROM layoffs_staging2;

UPDATE layoffs_staging2
SET company = TRIM(company);

SELECT DISTINCT industry
from layoffs_staging2
ORDER BY 1;

SELECT *
from layoffs_staging2
WHERE industry LIKE 'Crypto%';

update layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

select DISTINCT country
from layoffs_staging2
order by 1;

select DISTINCT country
from layoffs_staging2
where country LIKE 'United States%';
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


##all hollywood movies after 2000
select * from movies  
where industry='Hollywood' 
and release_year>2000;

##made pft equal to and more than 500 milliom
select *, (revenue-budget) as pft from financials where (revenue-budget)>=500;

##using CTE
WITH X AS(select * from movies  
where industry='Hollywood' 
and release_year>2000
),
	Y AS (select *, (revenue-budget) as pft from financials where (revenue-budget)>=500
    )
select X.title, X.industry,  
	Y.pft
	from X
join Y
on x.movie_id=y.movie_id		

with deptt_avg as (select deptt, avg(salary) as avg_sal
from salaries
grp by deptt)

select *
from salaries s
join deptt_avg
on s.deptt=deptt_avg.deptt
where s.salary > deptt_avg.avg_salmovies
SELECT * FROM gdb0041.dim_customer;

-- MONTH
-- PRODUCT NAME
-- VARIANT
-- SOLD QTY
-- GROSS PRICE PER ITEM
-- GROSS PRICE TOTAL
-- CUST CODE 90002002
SELECT * FROM gdb0041.dim_customer WHERE CUSTOMER LIKE 'CROMA';

##top market
##top product
##top customer

with cte1 as(
SELECT FSM.date, FSM.sold_quantity, DP.product,FSM.customer_code, FSM.product_code, FGP.fiscal_year, FGP.gross_price, 
round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total,
PID.pre_invoice_discount_pct
-- ((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct) as net_invoice_sales,
-- (((round (FGP.gross_price*FSM.sold_quantity,2))-PID.pre_invoice_discount_pct)-(PIDS.discounts_pct+ PIDS.other_deductions_pct)) as net_saless
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=FSM.fiscal_year
JOIN fact_pre_invoice_deductions AS PID 
ON PID.customer_code=FSM.customer_code and PID.fiscal_year=FSM.fiscal_year
WHERE FSM.fiscal_year=2021)
select *, (gross_price_total- gross_price_total*pre_invoice_discount_pct) as net_invoice_sales
from cte1
-- limit 1000000;
-- join fact_post_invoice_deductions as PIDS on PIDS.customer_code=FSM.customer_code


SELECT FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.product_code, FGP.fiscal_year, FGP.gross_price, round (FGP.gross_price*FSM.sold_quantity,2) as gross_price_total
 FROM gdb0041.fact_sales_monthly FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code and FGP.fiscal_year=get_fiscal_year(FSM.date)
-- WHERE customer_code=90002002 
-- AND GET_FISCAL_YEAR(DATE)=2021 
ORDER BY DATE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
JOIN gdb0041.fact_gross_price AS FGP
JOIN gdb0041.fact_manufacturing_cost AS FMC
ON FSM.product_code= DP.product_code AND FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

SELECT SUM(FSM.SOLD_QUANTITY) AS TOTAL_QTY
FROM fact_sales_monthly AS FSM
JOIN dim_customer AS DC
ON FSM.customer_code=DC.customer_code
WHERE GET_FISCAL_YEAR(FSM.DATE)=2021 AND  DC.MARKET="India"
GROUP BY DC.MARKET;GET_MARKET_BADGE;

SELECT FSM.product_code, FSM.date, FSM.sold_quantity, DP.product, DP.variant, FSM.customer_code, FGP.gross_price, FGP.fiscal_year, FMC.manufacturing_cost, FMC.cost_year 
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.dim_product AS DP
ON FSM.product_code= DP.product_code
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.FISCAL_YEAR=GET_FISCAL_
JOIN gdb0041.fact_manufacturing_cost AS FMC
 FGP.product_code=FSM.product_code AND FMC.product_code=FSM.product_code
WHERE FSM.customer_code=90002002 AND YEAR(date_add(DATE, INTERVAL 4 MONTH))=2021
ORDER BY date DESC;

select * from fact_sales_monthly
SELECT FSM.DATE , SUM(ROUND(FGP.gross_price*FSM.sold_quantity)) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FSM.DATE
ORDER BY FSM.DATE ASC;

SELECT FGP.fiscal_year , SUM(FGP.gross_price*FSM.sold_quantity) AS GROSS_PRICE_TOTAL
FROM gdb0041.fact_sales_monthly AS FSM 
JOIN gdb0041.fact_gross_price AS FGP
ON FGP.product_code=FSM.product_code AND
FGP.fiscal_year=GET_FISCAL_YEAR(FSM.DATE)
WHERE customer_code=90002002
GROUP BY FGP.fiscal_year
ORDER BY FGP.fiscal_year ASC;

SELECT * FROM fact_sales_monthly
SELECT * ,
(1-pre_invoice_discount_pct)*gross_price_total as net_invoice_sales,
(PID.discounts_pct+PID.other_deductions_pct) as post_invoice_discount_pct
FROM gdb0041.sales_preinv_discount as SPD
join fact_post_invoice_deductions AS PID
on PID.DATE=SPD.DATE AND
PID.CUSTOMER_CODE=SPD.CUSTOMER_CODE AND
PID.PRODUCT_CODE=PID.product_code
SELECT MARKET, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales
WHERE FISCAL_YEAR=2021
GROUP BY MARKET
ORDER BY net_sales_MLN
LIMIT 5;

SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE FISCAL_YEAR=2021
GROUP BY c.customer
ORDER BY net_sales_MLN
LIMIT 5;

SELECT s.product, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM net_sales s
JOIN dim_product p
ON s.product_code=p.product_code 
where s.fiscal_year=2019
group by s.product
order by NET_SALES_MLN
limit 5;
##percentage sales for global net sales
with cte1 as (
SELECT c.customer, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer)
select *, sum(net_sales_mln) over(partition by customer) from cte1
ORDER BY net_sales_MLN desc;

with cte1 as (
SELECT c.customer, c.region, ROUND(sum(net_sales)/1000000,2) AS NET_SALES_MLN
FROM gdb0041.net_sales n
join dim_customer c
on c.customer_code=n.customer_code
WHERE n.fiscal_year=2021 -- and n.market=in_market
GROUP BY c.customer, c.region)
select *, net_sales_mln*100/sum(net_sales_mln) over(partition by region) as pct_share_region from cte1
ORDER BY region, net_sales_MLN desc;


SELECT * FROM random_tables.expenses
order by category, date;

select *, sum(amount) over(partition by category order by date) as am
from random_tables.expenses
order by category, date
SELECT * FROM random_tables.expenses
ORDER BY category;

## show top 2 exp in each category

with cte1 as
(select 
*,
row_number() over(partition by category order by amount desc) as rn,
rank() over(partition by category order by amount desc) as rnk,
dense_rank() over(partition by category order by amount desc) as dnk
from expenses
order by category)
select * 
from cte1
where rn<3
SELECT * ,
row_number() over(order by marks desc) as rn,
rank () over(order by marks desc) as rnk,
dense_rank() over(order by marks desc) AS dnk
FROM random_tables.student_marks 
where dnk>6;
SELECT * 
FROM gdb0041.dim_product;

with cte1 as
(SELECT p.division, p.product, sum(sold_quantity) AS total_qty
FROM fact_sales_monthly s
JOIN dim_product p
ON s.product_code=p.product_code 
where fiscal_year=2021
group by p.division, p.product),
cte2 as(
select *, row_number() OVER(partition by division order by total_qty desc) as rn,
rank() over(partition by division order by total_qty desc) as rnk,
dense_rank() over(partition by division order by total_qty desc) as dnk
from cte1)
select * from cte2
where dnk<=3;

with cte1 as (SELECT c.market, c.region, round(sum(gross_price_total)/1000000,2) as gross_sales_mln
FROM gdb0041.gross_sales s
join dim_customer c
on s.customer_code=c.customer_code
where fiscal_year=2021
group by c.market, c.region
order by gross_sales_mln desc),
cte2 as(
select *, dense_rank() over(partition by region order by gross_sales_mln) as dnk
from cte1)
select * from cte2 where dnk<=2
create table fact_act_es
(
SELECT fm.date as date,
fm.fiscal_year as fiscal_year,
fm.product_code as product_code,
fm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
FROM gdb0041.fact_forecast_monthly AS FM
left JOIN fact_sales_monthly AS SM
using(date,product_code,customer_code)
union
select sm.date as date,
sm.fiscal_year as fiscal_year,
sm.product_code as product_code,
sm.customer_code as customer_code,
sm.sold_quantity as sold_quantity,
fm.forecast_quantity as forecast_quantity
from fact_sales_monthly as sm
right join gdb0041.fact_forecast_monthly AS FM
using(date,product_code,customer_code)
);
