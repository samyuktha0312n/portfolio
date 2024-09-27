# Auto mobile Company Report


## Problem Statement

This dashboard helps the airlines understand their customers better. It helps the airlines know if their customers are satisfied with their services. Through different ratings, they get to know their improvement area, & thus they can improve their services by identifying these area. It also lets them know the average delay & departure time, thus since by using this dashboard they have identified this problem, they can further work on factors responsible for these unwanted delays.

Since, number of neutral/dissatisfied customers (almost 57 %) are more than satisfied customers (around 43 %), thus in all they must work on improving their services. 

Also since average delay in arrival & departure both is 15 minutes, thus they must try to reduce it.

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
           

1) To analysis revenue for the hour and weekdays respectively,

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

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Customers = 129880

   Number of satisfied Customers (Male) = 28159 (21.68 %)

   Number of satisfied Customers (Female) = 28269 (21.76 %)

   Number of neutral/unsatisfied customers (Male) = 35822 (27.58 %)

   Number of neutral/unsatisfied customers (Female) = 37630 (28.97 %)


           thus, higher number of customers are neutral/unsatisfied.
           
### [2] Average Ratings

    a) Baggage Handling - 3.63/5
    b) Check-in Service - 3.31/5
    c) Cleanliness - 3.29/5
    d) Ease of online booking - 2.88/5
    e) Food & Drink - 3.21/5
    f) In-flight Entertainment - 3.36/5
    g) In-flight service - 3.64/5
    h) In-flight Wifi service - 2.81/5
    i) Leg room service - 3.37/5
    j) On-board service - 3.38/5
    k) Online boarding - 3.33/5
    l) Seat comfort - 3.44/5
    m) Departure & arrival convenience - 3.22/5
  
  while calculating average rating, null values have been ignored as they were not relevant for some customers. 
  
  These ratings will change if different visual filters will be applied.  
  
  ### [3] Average Delay 
  
      a) Average delay in arrival(minutes) - 15.09
      b) Average delay in departure(minutes) - 14.71
Average delay will change if different visual filters will be applied.

 ### [4] Some other insights
 
 ### Class
 
 1.1) 47.87 % customers travelled by Business class.
 
 1.2) 44.89 % customers travelled by Economy class.
 
 1.3) 7.25 % customers travelled by Economy plus class.
 
         thus, maximum customers travelled by Business class.
 
 ### Age Group
 
 2.1)  21.69 % customers belong to '0-25' age group.
 
 2.2)  52.44 % customers belong to '25-50' age group.
 
 2.3)  25.57 % customers belong to '50-75' age group.
 
 2.4)  0.31 % customers belong to '75-100' age group.
 
         thus, maximum customers belong to '25-50' age group.
         
### Customer Type

3.1) 18.31 % customers have customer type 'First time'.

3.2) 81.69 % customers have customer type 'returning'.
       
       thus, more customers have customer type 'returning'.

### Type of travel

4.1) 69.06 % customers have travel type 'Business'.

4.2) 30.94 % customers have travel type 'Personal'.

        thus, more customers have travel type 'Business'.


