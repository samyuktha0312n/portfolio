# Automobile Company Report


## Problem Statement

This dashboard helps the Auto mobile Company understand their customers better. 
To develop the dashboard that displays the key performances metrics for the informed decision-making.
#### Requirement:
- Hourly revenue analysis
- Profit and revenue trends
- Seasonal revenue
- rider demographics

Since, there is increase in the demand compared to the previous year (2021), profit margin increased by 45%.


### Data Analysis workflow
- Create a database
- Develop SQL queries
- Connect power BI to DB 
- Build a Dashboard in Power BI 
- Answer the analysis questions

### Steps followed 

- Step 1 : Collect the required data set.
- Step 2 : Connected the SQL server and Created the new database named bike_data.
- Step 3 : Load the dataset collected into the SQL server and stored inside tables in the form of dbo. files (bike_share_yr_0, bike_share_yr_1, cost_table ).
  ![Screenshot 2024-09-27 202805](https://github.com/user-attachments/assets/96580061-b943-4dd6-9621-6d0de62f6f52)

- Step 4 : Data cleaning steps removed the unwanted column in the table and joined both files (bike_share_yr_0, bike_share_yr_1) by using union.Included the cost_table file by using left join.
- Step 5 : Selected dteday, season, a.yr,weekday, hr, rider_type, riders, price, COGS for analysis.
- Step 6 : Calculated revenue(riders * price) and profit(riders * price - COGS * riders).

        Query

        with cte as (
        select * from bike_share_yr_0
        union 
        select * from bike_share_yr_1)

        select 
        dteday,
        season,
        a.yr,
        weekday,
        hr,
        rider_type,
        riders,
        price,
        COGS,
        riders * price as revenue,
        riders * price - COGS * riders as profit
        from cte a
        left join cost_table b
        on a.yr = b.yr

- Step 7 : After querying, connecting the SQL server to the PowerBI.
- Step 8 : After connecting, load the data into the powerBI - By clicking "home -> get data ->SQL server".Enter server name and database name and required query. 
- Step 9 : Started to Visualize the data, 

       i) Selected " visualization -> Build visual -> matrix ". Entered the required data ( hr as rows, columns as weekdays, values as the average of revenue).
       ii) Displayed sum of revenue and sum of profit.
       iii) Selected " visualization -> Build visual -> Line and clustered column chart ", x axis as year and month, y axis as sum of riders, line y axis as average of profit  and average of revenue.
       iv) Selected " visualization -> Build visual -> clustered Bar chart ", y axis as season, x axis as averages of revenue.
       v) Selected " visualization -> Build visual -> Donut chart ", values as sum of riders.
       vi) stated count of riders and calculated and displayed profit margin.
       vii) Created the slicer for analysing the for specific year.
           

1) To analysis revenue for the hourly and weekdays respectively,

![Screenshot 2024-09-27 105454](https://github.com/user-attachments/assets/654ea362-e57d-4040-83c0-0d594c294050)

2) sum of revenue and sum of profit,


![Screenshot 2024-09-27 105952](https://github.com/user-attachments/assets/b9038f18-c876-48f6-9449-f43f807c7fbc)

3) By comparing Average of profit, average of revenue by year (2021 and 2022), month with the riders. This shows increase in demand in automobiles.


![Screenshot 2024-09-27 110657](https://github.com/user-attachments/assets/24bbb336-667d-4fdc-9bd5-08ca068ffb21)

4) Analysing revenue by season,


![Screenshot 2024-09-27 110945](https://github.com/user-attachments/assets/1fc63a7a-2414-4da3-8701-1d4811775229)

5) Analysing the rider type,

![Screenshot 2024-09-27 111106](https://github.com/user-attachments/assets/347c2b7f-9cbd-4ac6-992f-5749d627a81e)

6) Total riders and profit margin,


![Screenshot 2024-09-27 111208](https://github.com/user-attachments/assets/a32af203-6ad1-4715-a800-51aade32f50c)

7) Slicer  for specific years(2021 and 2022)



![Screenshot 2024-09-27 113232](https://github.com/user-attachments/assets/390b7293-79f0-448c-a026-0169bf33fcc5)



# Measure used:
 Profit margin: 
                                           
        - Profit margin = (SUM(Query1[revenue]) - SUM(Query1[profit]) )/ SUM(Query1[profit])

Transforming data - 0 to 2021, 1 to 2022 in table:
                     
        - = Table.AddColumn(Source, "year", each if [yr] = "0" then 2021 else if [yr] = "1" then 2022 else null)

![Screenshot 2024-09-27 113718](https://github.com/user-attachments/assets/31b61aa0-b78e-4ef4-b984-827e3b61f45e)



 
 


# Snapshot of Dashboard (Power BI Service)

![Screenshot 2024-09-27 111942](https://github.com/user-attachments/assets/09b93007-e0bb-4542-963c-9c4b9a60a774)

 
 # Report Snapshot (Power BI DESKTOP)

 
![Screenshot 2024-09-27 112159](https://github.com/user-attachments/assets/de4bcf83-4c06-476b-a219-e26d9020c03d)

# Insights

Conservative Increase: Considering the substantial increase last year, a more conservative increase might be prudent to avoid hitting a price ceiling where demand starts to drop. An increase in the range of 10-15% could test the market's response without risking a significant loss of customers.

### Price Setting:

If the price in 2022 was $4.99, a 10% increase would make the new price about $5.49.

A 15% increase would set the price at approximately $5.74.

### Recommended Strategy:

Market Analysis: Conduct further market research to understand customer satisfaction, potential competitive changes, and the overall economic environment. This can guide whether leaning towards the lower or higher end of the suggested increase.

### Segmented Pricing Strategy:

 Consider different pricing for casual versus registered users, as they may have different price sensitivities.

### Monitor and Adjust: 
Implement the new prices but be ready to adjust based on immediate customer feedback and sales data. Monitoring closely will allow you to fine-tune your pricing strategy without committing fully to a price that might turn out to be too high.
