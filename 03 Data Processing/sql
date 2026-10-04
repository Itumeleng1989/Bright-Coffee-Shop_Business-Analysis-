--Bright Coffee Shop Sales Analysis

-- Determine No. of store locations  
select distinct store_location
from workspace.default.bright_coffee_shop_sales_dataset ; 

--What is the period of my data 
select min(transaction_date) as min_date, 
max(transaction_date) as max_date
from workspace.default.bright_coffee_shop_sales_dataset;

--what time does shop open; business hours 
select min(transaction_time) as opening_time, 
max(transaction_time) as closing_time
from workspace.default.bright_coffee_shop_sales_dataset;

--show number of product sold by store location 
select store_location,
count(distinct product_id) as no_of_products
from workspace.default.bright_coffee_shop_sales_dataset 
group by store_location
order by no_of_products desc;

--show number of product sold
select count(distinct product_id) as no_of_products
from workspace.default.bright_coffee_shop_sales_dataset;

-- Determine No. of product categories   
select distinct product_category
from workspace.default.bright_coffee_shop_sales_dataset; 

--variants of coffee 
select distinct product_category, product_type, product_detail
from workspace.default.bright_coffee_shop_sales_dataset
where product_category = 'Coffee';

--variants of tea
select distinct product_category, product_type, product_detail
from workspace.default.bright_coffee_shop_sales_dataset
where product_category = 'Tea';

--Total revenue by store location 
select store_location,
sum(transaction_qty*unit_price) as revenue
from workspace.default.bright_coffee_shop_sales_dataset 
group by store_location
order by revenue desc;

--Total revenue 
select sum(transaction_qty*unit_price) as revenue
from workspace.default.bright_coffee_shop_sales_dataset;

--Total transactions 
select count(transaction_qty) as total_transactions
from workspace.default.bright_coffee_shop_sales_dataset;

--average sale 
select sum(transaction_qty*unit_price)/count(transaction_id) as avg_sale
from workspace.default.bright_coffee_shop_sales_dataset;

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
--Big Code for Bright Coffee Shop Sales Analysis 

select * 
from workspace.default.bright_coffee_shop_sales_dataset;

select transaction_date,--from orginal table 
transaction_time,
dayname(transaction_date) as Day_name, --dayname function gives specific day Extract day of week e.g. Monday, Tuesday, Wednesday etc
monthname (transaction_date) as Month_name, --Monthname function gives specific month
count (transaction_id) as no_of_sales,--Count function gives total number of transactions id
sum(transaction_qty) as no_of_units_sold,--aggregate function gives sum of transaction qty
count (distinct product_id) as no_of_unique_products,--count the number of unique products
count (store_id) as no_of_stores,--count all of the rows
sum(transaction_qty*unit_price) as revenue,--sum the product of transaction qty and unit price
--Case statement always create buckets fpr enhanced analyses 
--This case statement is used to classify the Dayname column into classification buckets 
case 
when Day_name in ('Mon','Tue','Wed','Thu','Fri') then 'Weekday'
when Day_name in ('Sat','Sun') then 'Weekend'
end as Day_Classification,
--Classifying the transaction time 
case 
when hour(transaction_time) between 6 and 11 then '01.Morning'
when hour(transaction_time) between 12 and 17 then '02.Afternoon'
when hour(transaction_time) between 18 and 21 then '03.Evening'
end as Time_Classification,
monthname(transaction_date) as Month_name, --Extract month of year e.g. January, February, March etc
store_location,
product_category,
product_type,
product_detail
from workspace.default.bright_coffee_shop_sales_dataset
group by transaction_date,
transaction_time,
dayname(transaction_date),
case 
when dayname(transaction_date) in ('Mon','Tue','Wed','Thu','Fri') then 'Weekday'
when dayname(transaction_date) in ('Sat','Sun') then 'Weekend'
end,
case 
when hour(transaction_time) between 6 and 11 then '01.Morning'
when hour(transaction_time) between 12 and 17 then '02.Afternoon'
when hour(transaction_time) between 18 and 21 then '03.Evening'
end,
monthname(transaction_date),
store_location,
product_category,
product_type,
product_detail;
