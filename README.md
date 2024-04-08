# Sales Analysis

## Bike Stores Business in America

### Project Overview

This data analysis project aims to provide insights into the sales performance of a bike stores company of three years (2016, 2017, 2018). By analysing various aspects of the sales data, we seek to identify trends, make data-driven recommendations, and fgain a deeper understanding of the company's performance.

### Data Sources

Sales Data: The primery dataset used for this analysis contains SQL server  database of 9 tables that captures the orders, stores, categories, brands, sales, customers and sales reps.

### Tools 

- SQL Server: Database set up, data cleaning.
- MS Excel: Analysis, capturing trends and creating a primilnary interactive dashboard.
- Tableau: For creating an interactive dashboard as an Executive summary for top management.

### Data Cleaning/Preperation

In the initial data preperation phase, we have performaed the following tasks:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer our main business questions, such as:

- What is the over all sales trend?
- Which brands are top seller?
- what are the peak sales periods?
- Is there any seasonality that impacts the sales?

### Data Analysis

Luckily the database was cleaned previously and at this point it was ready for preperation:

```sql
SELECT
	ord.order_id,
	concat (cus.first_name,' ' , cus.last_name) AS 'customers',
	cus.city,
	cus.state,
	ord.order_date,
	SUM (ite.quantity) AS 'total_units',
	SUM (ite.quantity* ite.list_price) AS 'revenue',
	pro.product_name,
	cat.category_name,
	bra.brand_name,
	sto.store_name,
	concat (sta.first_name,' ' ,sta.last_name) AS 'sales_rep'
FROM sales.orders ord
join sales.customers cus
on ord.customer_id = cus.customer_id
join sales.order_items ite
on ord.order_id = ite.order_id
join production.products pro
on ite.product_id = pro.product_id
join production.categories cat
on pro.category_id = cat.category_id
join production.brands bra
on pro.brand_id = bra.brand_id
join sales.stores sto
on ord.store_id = sto.store_id
join sales.staffs sta
on ord.staff_id = sta.staff_id

GROUP BY
	ord.order_id,
	concat (cus.first_name,' ' , cus.last_name),
	cus.city,
	cus.state,
	ord.order_date,
	pro.product_name,
	cat.category_name,
	bra.brand_name,
	sto.store_name,
	concat (sta.first_name,' ' ,sta.last_name)
```
### Results/Findings
The analysis results are summarized as follows:
1. The company have seen an improvement in sales revenue by 30 percent from 2016 to 2017 but then it dropped again from 2017 to 2018 by about 40% especially in H2 of 2018. The reasons of the drop was not validated by the data available to me.
2. Mountain bikes are the best performing category accross all verticals.
3. Trek brand holds around 60% of the companies revenue over the three years duration.
4. New york's store is the best performing store among others.
5. The dashboard is also showing the top customers for each stores which executives wanted to run a loyalty programs for them.
6. Top sales reps as well can be clearly spotlighted by the dashboard for future awards or bonuses.

### Recommendation:

Based on the analysis, we recommend the below:

1. We have to gather more data to understand what happend in the H2, 2018 and why it shows a huge decline in sales accross stores. Was it inventory issue? liquidity issue? it is very crutuial to understand.
2. I recommend focusing in second and third top selling categories and brands through out our marketing activities to work on scaling them up.
3. we have to gather more data from customers to understand why is New york's store is performing better than others and take a data driven decision for next recommendation.
4. Loyalty program for cutomers is important to improve cross/up selling.
