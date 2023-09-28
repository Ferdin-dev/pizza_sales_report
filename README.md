# Pizza Sales Report

## Project Overview

The goal of this project was to analyze the sales data of a pizza restaurant to identify trends and patterns, and to provide actionable insights that could help the restaurant improve its sales and profitability.

![Project_2_Dashboard_1](https://github.com/Ferdin-dev/pizza_sales_report/assets/55439765/2f2caf39-7c83-4bd9-953a-100d7248b8b6)


## Table of Contents
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data cleaning preparation](#data-cleaning-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Key Findings](#key-findings)
- [Recommendations](#recommendations)
- [Conclusion](#conclusion)
- [Difficulties](#difficulties)
- [Screenshots](#screenshots)
- [Demo](#demo)


## Data Sources

Pizza Sales Data: The primary dataset used for this analysis is the “pizza_sales.csv” file, containing detailed information about the company employee.


## Tools
- Excel – Data cleaning
- SQL Server – Data Analysis
- Power BI – Creating reports

## Data cleaning preparation

In the initial data preparation phase, we performed the following tasks:
- Imported the data to SQL Server
- Data loading and inspection in Power BI
- Handling missing values and errors
- Data cleaning and formatting

## Exploratory Data Analysis
EDA involved exploring the sales data to answer key questions, such as:
- Are there any specific days with exceptionally high order counts?
- Which category of pizzas is ordered the most?
- What is the average value of each order?
- What are the peak ordering hours during the day?
- Can you identify different types of customers based on their ordering behavior?

## Data Analysis
Include some interesting code/features worked with:

### Power BI Code

#### All Measures

```
Avg. Order Value = DIVIDE([Total Revenue],[Total Qty Ordered])
```
```
Avg. Pizza Per Order = DIVIDE([Total Pizza Sold],[Total Qty Ordered])
```
```
Day time with the most order = TOPN(1,VALUES(pizza_sales[Day_Time]),[Total Qty Ordered],DESC)
```
```
First day with highest orders = 
                    SWITCH(TOPN(1,VALUES(pizza_sales[Day]),[Total Qty Ordered],DESC),
                    "MON","monday",
                    "TUE","tuesday",
                    "WED","wednesday",
                    "THU","thursday",
                    "FRI","friday",
                    "SAT","saturday",
                    "SUN","sunday")
```

```
month with highest orders = 
                            SWITCH(TOPN(1,VALUES(pizza_sales[Month]),[Total Qty Ordered],DESC),
                            "JAN","january",
                            "FEB","february",
                            "MAR","march",
                            "APR","april",
                            "MAY","may",
                            "JUN","june",
                            "JUL","july",
                            "AUG","august",
                            "SEP","september",
                            "OCT","october",
                            "NOV","november",
                            "DEC","december")
```
```
most sold and ordered category = TOPN(1,VALUES(pizza_sales[pizza_category]),[Total Qty Ordered],DESC,[Total Pizza Sold],DESC)
```
```
most sold pizza size = TOPN(1,VALUES(pizza_sales[pizza_size]),[Total Pizza Sold],DESC)
```
```
pizza with the highest revenue = TOPN(1,VALUES(pizza_sales[pizza_name]),[Total Revenue],DESC)
```
```
pizza with the lowest revenue = TOPN(1,VALUES(pizza_sales[pizza_name]),[Total Revenue],ASC)
```
```
Total Pizza Sold = SUM(pizza_sales[quantity])
```
```
Total Qty Ordered = DISTINCTCOUNT(pizza_sales[order_id])
```
```
Total Revenue = SUM(pizza_sales[total_price])
```
```
worst sold pizza size = TOPN(1,VALUES(pizza_sales[pizza_size]),[Total Pizza Sold],ASC)

```
#### All Calculated Columns
```
Month = SWITCH(MONTH(pizza_sales[order_date].[Date]),
                        1,"JAN",
                        2,"FEB",
                        3,"MAR",
                        4,"APR",
                        5,"MAY",
                        6,"JUN",
                        7,"JUL",
                        8,"AUG",
                        9,"SEP",
                        10,"OCT",
                        11,"NOV",
                        12,"DEC")
```
```
Day_Time = 
var mor_text = "Morning"
var aft_text = "Afternoon"
var eve_text = "Evening"
return IF(pizza_sales[order_time] <= TIME(11,59,59),
                mor_text,
            IF(pizza_sales[order_time] <= TIME(17,59,59),
                aft_text, eve_text))
```
```
Day = SWITCH(WEEKDAY(pizza_sales[order_date].[Date]),
                1, "SUN",
                2, "MON",
                3, "TUE",
                4, "WED",
                5, "THU",
                6, "FRI",
                7, "SAT")
```

### SQL Code

Total revenue
```
SELECT SUM(total_price) as total_revenue
   FROM [Pizza_Sales].[dbo].[pizza_sales]
```

Total qty ordered
```
SELECT count(distinct(order_id)) as total_qty_ordered
   FROM [Pizza_Sales].[dbo].[pizza_sales]
```
Total Pizza Sold
```
SELECT SUM(quantity) as total_pizza_sold
   FROM [Pizza_Sales].[dbo].[pizza_sales]
```
Pizza name with the highest revenue
```
SELECT top 1 pizza_name, SUM(total_price) as total_revenue
   FROM [Pizza_Sales].[dbo].[pizza_sales]
   GROUP BY pizza_name
   ORDER BY total_revenue desc
```
Day of week with the highest order
```
SELECT TOP 1 DATENAME(DW,order_date) as order_day, count(distinct order_id) as total_qty_ordered
   FROM [Pizza_Sales].[dbo].[pizza_sales]
   GROUP BY DATENAME(DW,order_date)
   ORDER BY total_qty_ordered desc
```
Month with the highest orders
```
SELECT TOP 1 DATENAME(MONTH,order_date) as order_month, count(distinct order_id) as total_qty_ordered
   FROM [Pizza_Sales].[dbo].[pizza_sales]
   GROUP BY DATENAME(MONTH,order_date)
   ORDER BY total_qty_ordered desc
```

## Key Findings
The analytics results are summarized as follows:
- The busiest day of the week for the restaurant was Friday, followed by Saturday and Thursday.
- The peak time for orders was at the afternoon.
- The most ordered category of pizza was classic.
- The average order value was $38.31.
- Customers who ordered multiple pizzas tended to spend more money.

## Recommendations

Based on the findings of the analysis, the following recommendations were made to the restaurant management:
- Increase staff levels on Fridays, Saturday, and Thursday, and during the peak time for orders.
- Offer special promotions on less popular types of pizza category to increase sales.
- Consider offering a loyalty program to reward customers who order multiple pizzas.

## Conclusion

The pizza restaurant sales analysis project was successful in identifying trends and patterns in the data, and in providing actionable insights that could help the restaurant improve its sales and profitability. The recommendations made to the restaurant management were based on the findings of the analysis, and were tailored to the specific needs of the business.

## Difficulties

- I didn’t know how to use Box plot chart, so I had to google it to find a solution on how to use, so that it would play a great impact on this project.
- I also googled the topic of Smart Narrative.

## Screenshots

![Project_2_Dashboard_2](https://github.com/Ferdin-dev/pizza_sales_report/assets/55439765/e2156857-5cc1-4bcb-b4b2-99a9d619366c)
![Project_2_Dashboard_1](https://github.com/Ferdin-dev/pizza_sales_report/assets/55439765/8182ef42-04f7-41aa-8c20-f23b5b87315a)

## Demo

https://github.com/Ferdin-dev/pizza_sales_report/assets/55439765/14082435-e196-4252-91ab-26964bc40d5b


