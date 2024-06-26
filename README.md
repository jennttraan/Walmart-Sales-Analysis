# Walmart Sales Analysis

![walmart_logo](https://github.com/jennttraan/Walmart-Sales-Analysis/assets/144400508/f6ef8f79-e4c6-42e0-b4b9-21f4203c50a5)


## Business Task
Analyze Walmart sales data to determine what kind of items sell the best and how can Walmart market themselves better to their clientele.

## Data Source
All data sets used can be found [here](https://github.com/jennttraan/Walmart-Sales-Analysis/blob/main/WalmartSalesData.csv.csv). 

## Cleaning And Processing The Data

Complete data cleaning can be found [here](https://github.com/jennttraan/Walmart-Sales-Analysis/blob/main/EDA%20for%20Walmart%20Sales) and [here](https://github.com/jennttraan/Walmart-Sales-Analysis/blob/main/Data%20Cleaning).

I spent some time finding unique differences between items and found the most popular items and the most common customers.

Added a time_of_day column to see when Walmart was the busiest.
```
SELECT
	time,
	(CASE
		WHEN 'time' BETWEEN "00:00:00" AND "12:00:00" THEN "Morning"
        WHEN 'time' BETWEEN "12:01:00" AND "16:00:00" THEN "Afternoon"
        ELSE "Evening"
    END) AS time_of_day
FROM sales;
```
What is the best selling product line?
```
SELECT
	SUM(quantity) as qty,
    product_line
FROM sales
GROUP BY product_line
ORDER BY qty DESC;
```

What product line had the most revenue?
```
SELECT
	product_line,
	SUM(total) as total_revenue
FROM sales
GROUP BY product_line
ORDER BY total_revenue DESC;
```
What is the gender distribution per branch?
```
SELECT
	gender,
	COUNT(*) as gender_cnt
FROM sales
WHERE branch = 'C'
GROUP BY gender
ORDER BY gender_cnt DESC;
-- Gender per branch is more or less the same hence, I don't think has
-- an effect of the sales per branch and other factors.
```

## Conclusion

After cleaning the data, mostly fixing dates and times, we have found insights that will be useful to Walmart management and stakeholders to not only ensure that they have inventory stocked for their most popular products and product lines, but also to know which kind of cutomers to cater to and in what areas.

1. Walmart should consider catering to women and fashion accessories and they sell the most.
2. Walmart should also consider adding in Apple Pay as a form of payment as Ewallets are the second most popular way to pay.
3. Most popular product lines/categories are fashion and food.
4. January had the largest COGS. Perhaps because after holidays.
5. The most revenue made at Walmart was from food and beverages; least was health and beauty.
6. Home and lifestyle products have the most added tax.
7. Best rated products are food and beverages, least is home and lifestyle. Walmart should evaluate the reason why the home and lifestyle items are revied badly and reconsider selling some of those items.
8. Most sales are made during the evenings on Mondays, so each location should be staffed accordingly to ensure the best service. 
