# Big-Query---Practical-exercise---Sonali-Matadin
This BigQuery practical exercise uses a Retail Sales dataset to build SQL skills, including filtering, aggregation, grouping, CASE logic, conditional summaries, and calculated fields. Learners query transactions, classify customers and products, analyze sales patterns, and generate insights for retail analytics.


SELECT *
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`
WHERE EXTRACT(YEAR FROM Date) = 2023;



SELECT *
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`
WHERE `Total Amount` > (
    SELECT AVG(`Total Amount`)
    FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`
);



SELECT 
    SUM(`Total Amount`) AS Total_Revenue
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`;


SELECT DISTINCT `Product Category`
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`;



SELECT 
    `Product Category`,
    SUM(Quantity) AS Total_Quantity
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`
GROUP BY `Product Category`;



SELECT 
    `Customer ID`,
    Age,
    CASE
        WHEN Age < 30 THEN 'Youth'
        WHEN Age BETWEEN 30 AND 59 THEN 'Adult'
        ELSE 'Senior'
    END AS Age_Group
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`;



SELECT 
    Gender,
    COUNT(*) AS High_Value_Transactions
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`
WHERE `Total Amount` > 500
GROUP BY Gender;



SELECT 
    `Product Category`,
    SUM(`Total Amount`) AS Total_Revenue
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`
GROUP BY `Product Category`
HAVING SUM(`Total Amount`) > 5000;



SELECT 
    `Transaction ID`,
    `Price per Unit`,
    CASE
        WHEN `Price per Unit` < 50 THEN 'Cheap'
        WHEN `Price per Unit` BETWEEN 50 AND 200 THEN 'Moderate'
        ELSE 'Expensive'
    END AS Unit_Cost_Category
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`;



SELECT 
    `Customer ID`,
    Age,
    `Total Amount`,
    CASE
        WHEN `Total Amount` > 1000 THEN 'High'
        ELSE 'Low'
    END AS Spending_Level
FROM `practical-exercise-big-query.RETAIL_SALES_DATASET.RETAIL_SALES_DATASET`
WHERE Age >= 40;
