CREATE DATABASE amazon_database;
use amazon_database;
CREATE TABLE amazon (
`Invoice ID` VARCHAR(30) not null,
 branch VARCHAR(5)not null,
 city VARCHAR(30)not null,
 `customer type` VARCHAR(30) not null,
 gender VARCHAR(10)not null,
 `product line` VARCHAR(100)not null,
 `unit price` DECIMAL(10, 2)not null,
 quantity INT not null,
 `Tax 5%` FLOAT NOT NULL,
 Total DECIMAL(10, 2)NOT NULL,
 Date date not null,
 Time TIME NOT NULL,
 `payment method` VARCHAR(30) NOT NULL,
 cogs DECIMAL(10, 2)NOT NULL,
 gross_margin_percentage FLOAT(11, 9)NOT NULL,
 gross_income DECIMAL(10, 2)NOT NULL,
 rating FLOAT(2, 1) NOT NULL
);

select * from amazon;

#Product Analysis
#"Top Performing Product": "Food and beverages" has the highest total revenue among all product lines,
#with a total revenue of $56,144.96.
#Electronic Accessories: Similar to Fashion Accessories, Electronic Accessories have a decent total sales amount but 
#a lower average revenue per sale compared to other product lines. This could indicate that customers are purchasing 
#lower-priced items within this category.


#Sales Analysis
#"Sales Trends": All product lines seem to have comparable total revenues, 
#but "Food and beverages" has a slightly higher total revenue compared to others. 
#However, "Home and lifestyle" has a slightly higher average transaction value, 
#indicating that customers might be spending more per transaction in that category.

#Customer Analysis
#"Customer Preferences": It appears that "Food and beverages" is the most popular product line 
#based on total revenue.
#Female customers, whether members or normal, tend to spend more compared to male customers.

-- Questions 

-- 1 What is the count of distinct cities in the dataset?
SELECT COUNT(DISTINCT city) AS distinct_city_count
FROM amazon;

-- 2 For each branch, what is the corresponding city?
SELECT branch, city
FROM amazon
GROUP BY branch, city;

-- 3 What is the count of distinct product lines in the dataset?
SELECT COUNT(DISTINCT `product line`) AS distinct_product_lines
FROM amazon;

-- 4 Which payment method occurs most frequently?
select `payment method`, count(*) as frequency
from amazon
group by `payment method`
order by frequency desc
limit 1;

-- 5 Which product line has the highest sales?
select `product line` , sum(total) as total_sales
from amazon
group by `product line`
order by total_sales desc
limit 1; 

-- 6 How much revenue is generated each month?
select date_format(date,'%Y-%m') as month,
sum(total) as total_revenue
from amazon
group by month
order by month;

-- 7 In which month did the cost of goods sold reach its peak?

select date_format(Date,'%y-%m') AS MONTH,
SUM(COGS) AS TOTAL_COGS
from amazon
GROUP BY month
ORDER BY TOTAL_COGS DESC
limit 1;

-- 8 Which product line generated the highest revenue?
select distinct`product line` as distinct_product,
sum(Total) as total_revenue
from amazon
group by distinct_product
order by total_revenue desc
limit 1;

-- 9 In which city was the highest revenue recorded?
select distinct city as distinct_city,
sum(total) as total_revenue
from amazon
group by distinct_city
order by total_revenue desc
limit 1; 

-- 10 Which product line incurred the highest Value Added Tax?
select `product line`,sum(`Tax 5%`) as VAT
FROM AMAZON
GROUP BY `PRODUCT LINE`
ORDER BY VAT DESC
LIMIT 1;

-- 11 For each product line, add a column indicating "Good" if its sales are above average, otherwise "Bad."
SELECT DISTINCT `PRODUCT LINE`,
CASE 
    WHEN gross_income > (SELECT AVG(gross_income)FROM AMAZON) THEN 'GOOD'
    ELSE 'BAD' 
    END AS SALES_PERFORMANCE
    FROM AMAZON;
    
-- 12 Identify the branch that exceeded the average number of products sold.

SELECT BRANCH FROM(SELECT BRANCH , COUNT(*) AS TOTAL_PRODUCT_SOLD
FROM AMAZON GROUP BY BRANCH )AS BRANCH_PRODUCT 
WHERE TOTAL_PRODUCT_SOLD > (SELECT AVG(TOTAL_PRODUCT_SOLD) FROM (SELECT BRANCH , COUNT(*) AS TOTAL_PRODUCT_SOLD
FROM AMAZON GROUP BY BRANCH )AS AVG_PRODUCT_SOLD);

-- 13 Which product line is most frequently associated with each gender?
SELECT `PRODUCT LINE`,GENDER,count(*) AS FREQUENCY
FROM AMAZON
GROUP BY `PRODUCT LINE` ,GENDER
ORDER BY GENDER,FREQUENCY DESC;

-- 14 Calculate the average rating for each product line.
SELECT `PRODUCT LINE`, avg(RATING) AS AVG_RATING
FROM AMAZON
GROUP BY `PRODUCT LINE`
ORDER BY AVG_RATING DESC; 


-- 15 Count the sales occurrences for each time of day on every weekday.
SELECT 
    DATE_FORMAT(date, '%W') AS weekday,
    DATE_FORMAT(time, '%H:%i:%s') AS time_of_day,
    COUNT(*) AS sales_occurrences
FROM 
    amazon
GROUP BY 
    DATE_FORMAT(date, '%W'),
    time
ORDER BY 
    DATE_FORMAT(date, '%W'),
    time
LIMIT 0, 1000;


-- 16 Identify the customer type contributing the highest revenue.
SELECT `customer type`,sum(TOTAL) AS highest_revenue
FROM AMAZON
group by `customer type`
ORDER BY HIGHEST_REVENUE DESC;

-- 17 Determine the city with the highest VAT percentage.
SELECT CITY , AVG(`Tax 5%` / total) * 100 AS HIGHEST_VAT
FROM amazon
group by city
order by highest_vat desc
limit 1;

-- 18 Identify the customer type with the highest VAT payments.
select `customer type`,sum(`Tax 5%`)as highest_vat_payment
from amazon 
group by `customer type`
order by highest_vat_payment desc
limit 1;

-- 19 What is the count of distinct customer types in the dataset?
select count(DISTINCT`customer type`)as distinct_customer_types
from amazon;

-- 20 What is the count of distinct payment methods in the dataset?
select count(distinct`payment method`) as distinct_payment_methods
from amazon;

-- 21 Which customer type occurs most frequently?

select  `customer type`, count(*) as frequency
from amazon 
group by `customer type`
order by frequency desc
limit 1;

-- 22 Identify the customer type with the highest purchase frequency.

select `customer type` , count(distinct `invoice ID`) as frequency
from amazon 
group by `customer type`
order by frequency desc
limit 1;

-- 23 Determine the predominant gender among customers.

select gender,count( gender) as frequent_customer
from amazon 
group by gender
order by frequent_customer desc
limit 1;

-- 24 Examine the distribution of genders within each branch.
select branch, gender, count(*) as branch_gender_count
from amazon 
group by branch,gender
order by branch,gender;

-- 25 Identify the time of day when customers provide the most ratings.

SELECT DATE_FORMAT(time, '%H:00:00') AS Most_rated_time, COUNT(*) AS rating_count
FROM amazon
GROUP BY Most_rated_time
ORDER BY rating_count DESC
LIMIT 1;

-- 26 Determine the time of day with the highest customer ratings for each branch.

SELECT DISTINCT BRANCH,DATE_FORMAT(time, '%H:00:00') AS Most_rated_time, COUNT(*) AS rating_count
FROM amazon
GROUP BY Most_rated_time,BRANCH
ORDER BY BRANCH,rating_count DESC;

-- 27 Identify the day of the week with the highest average ratings.

SELECT date_format(DATE,'%W') AS AVG_RATED_DAY, avg(rating) AS AVG_RATING
FROM AMAZON
GROUP BY AVG_RATED_DAY
ORDER BY AVG_RATING DESC
LIMIT 1;

-- 28 Determine the day of the week with the highest average ratings for each branch.
SELECT BRANCH, date_format(DATE,'%W') AS AVG_RATED_DAY, AVG(rating) AS average_rating
FROM AMAZON
GROUP BY AVG_RATED_DAY,BRANCH
ORDER BY BRANCH,average_rating DESC;










 








 






























