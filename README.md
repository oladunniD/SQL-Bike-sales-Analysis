# Bike Sales Analysis

![images alt](https://github.com/oladunniD/SQL-Bike-sales-Analysis-Project/blob/2aa7ab5689ae2981daef238083e0300d8ec79b0e/images%20(18)1.png)

## Table of contents

- [Introduction](#introduction)
- [Data Overview](#data-overview)
- [Data Preparation and Cleaning](#data-preparation-and-cleaning)
- [Data Analysis](#data-analysis)
- [Sales Performance Analysis](#sales-performance-analysis)
- [Product Category Sales Performance](#product-category-sales-performance)
- [Profit and Cost Analysis](#profit-and-cost-analysis)
- [Conclusion](#conclusion)
- [Overall Recommendations](#overall-recommendations)	

### 1. Introduction
This report presents an exploratory and descriptive analysis of the bike sales dataset using SQL server, originally sourced from [Kaggle](https://www.kaggle.com/datasets/ma12492002/bike-market-sales-data) as an Excel file and later imported into SQL Server after being converted into a flat file. During the import process, data types were adjusted to ensure accurate analysis, and data cleaning was conducted, particularly to standardize customer gender information. This report highlights key insights derived from the dataset through various SQL queries.


### 2. Data Overview
The dataset spans six years of sales transactions, containing 18 columns and 112,036 rows. Key information includes Date, Day, Month, Year, Customer Age, Age Group, Customer Gender, Country, State, Product Category, Sub Category, Product, Order Quantity, Unit Cost, Unit Price, Revenue, Cost, and Profit. The company offers 3 Product Categories, 17 Product Subcategories, 130 Products, and sells these products across 6 countries: the United States, the United Kingdom, France, Germany, Australia, and Canada.
![sales data overview](sales%20data%20overview.png)

### 3. Data Preparation and Cleaning
A database named “sales data” was created, and the dataset was imported into SQL Server after conversion to a flat file. During the import, the following changes were made:
-	Data types were adjusted to match the appropriate formats for analysis:

-	The 'customer gender' column values were updated from 'M' to 'Male' and 'F' to 'Female' for clarity:
  ``` Sql
update salesdata set Customer_Gender=replace(replace(customer_gender,'M', 'Male'),'F','Female' )
```

### 4. Data Analysis

#### 4.1 Sales Performance Analysis
##### Objective:
Determine sales revenue distribution among geographical locations and identify the age group and gender that generated the highest sales revenue.
```Sql
select Country, sum(revenue) 'Total sales'
from dbo.salesdata
group by Country
order by sum(revenue)desc
```

```
select Age_Group,customer_gender, sum(Revenue) 'total sales'
from dbo.salesdata
group by Age_Group,customer_gender
order by sum(revenue) desc
```
##### Results and Interpretation: 
-	The United States generated the highest sales revenue with $27,777,098, followed by Australia ($21,196,395), the United Kingdom ($10,575,628), Germany ($8,956,724), France ($8,414,745), and Canada ($7,906,182).
-	The age group 34-64 years old, with male customers, generated the highest sales revenue of $21,207,395. Female customers within the same age group generated $21,159,786. The next significant contributors were male customers aged 25-34 with $15,391,679 and female customers of the same age group with $15,075,353.
  
##### Recommendation:
Focus marketing efforts on the United States and Australia, especially targeting the 34-64 age group, which has shown the highest sales potential across genders.

#### 4.2 Product Category Sales Performance

##### Objective: Analyse the variation between product category sales revenue and order quantity.
```Sql
select Product_Category, sum (revenue) 'total sales', sum (order_quantity) 'total order'
from dbo.salesdata
group by product_category
order by sum(Revenue) desc, sum(profit) desc
```
##### Results and Interpretation

-	Bikes generated the highest sales revenue with $61,434,484, followed by Accessories ($15,022,766), and Clothing ($8,369,522).
-	Accessories had the highest order quantity (1,042,791), followed by Clothing (254,713), and Bikes (36,201). The lower order quantity for bikes could be due to their higher unit price compared to accessories and clothing.
##### Recommendation:
Consider introducing promotions or financing options for bikes to increase their order quantity. Additionally, focus on upselling accessories alongside bike purchases to maximize revenue.
#### 4.3 Profit and Cost Analysis
##### Objective:
Assess the total sales, cost, and profit over the sales period.
``` Sql
select year,sum(revenue) 'Total sales',sum(cost) 'Total cost' , sum(profit) 'Total profit'
from dbo.salesdata
group by year
order by year asc
```

##### Results and Interpretation:
- Both sales and profits increased steadily over the years, with a significant spike in sales revenue in 2013, suggesting the impact of a potential change in marketing strategy.
- In 2014 there was a decrease in sales and the corresponding cost and profit, however, the sales and profit increased in the subsequent years.
  
##### Recommendation:
Investigate the marketing strategies implemented in 2013 to replicate successful tactics in future campaigns. Additionally, maintain a close watch on cost management to ensure profitability continues to grow alongside sales.

### 5. Conclusion
The SQL queries executed on the bike sales dataset have provided valuable insights into customer behaviour, sales performance, and financial trends. These findings can inform strategic decisions related to product offerings, marketing efforts, and regional sales focus.

### Overall Recommendations
-Prioritize high-revenue regions and customer segments in marketing strategies.
-Explore pricing and promotional strategies for high-value products like bikes.
-Continuously analyze market trends to adjust strategies for sustained growth and profitability.

### References
1. SQl with Practices Exercise by D Armstrong
2. [chatGPT](https://chatgpt.com/)


