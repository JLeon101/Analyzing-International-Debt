# Analyzing International Debt Statistics
![image](https://github.com/user-attachments/assets/5b36bfee-62c1-4a9d-8434-d3e9c9c4d03e)
In this project, I was able to track the country with the highest amount of debt, count how many countries are in the dataset, as well as query the one country with the lowest principal repayment amount. This experience allowed me to showcase and refine my SQL knowledge and implementation by answering questions that require precision.

## Database Schema
This project uses one main table

1. **international_debt**: Contains information regarding countries and debt amount
   
   - `country_code`: Code representing each country.
   - `country_name`: Name of the country.
   - `indicator_name`: Description of debt indicator.
   - `indicator_code`: Code representing the debt indicator.
   - `debt`: Value of the debt indicator for the given country (in US Dollars).

## Entity Relationship Diagram (ERD)

<img width="600" height="600" alt="Untitled diagram-2026-01-03-231933" src="https://github.com/user-attachments/assets/46703d8b-09e4-4524-ae1b-138a13a487a8" />


## SQL Questions with Answers

1. What is the number of distinct countries in the database?
   ``` sql
   SELECT COUNT(DISTINCT(country_name)) AS total_distinct_countries
   FROM public.international_debt;
   ```
2. What country has the highest amount of debt?
   ``` sql
   SELECT country_name, SUM(debt) AS total_debt
   FROM public.international_debt
   GROUP BY country_name
   ORDER BY total_debt DESC, country_name DESC
   LIMIT 1;
   ```
3. What country has the lowest amount of repayments?
   ``` sql
   SELECT country_name, indicator_name, MIN(debt) AS lowest_repayment
   FROM public.international_debt
   WHERE indicator_code = 'DT.AMT.DLXF.CD'
   GROUP BY country_name, indicator_name
   ORDER BY lowest_repayment
   LIMIT 1;
