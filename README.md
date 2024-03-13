# Bicycle (AdventureWorks) Store Analysis

This is the first project I created for my Data Analysis portfolio, as a part of Maven Analytics Power BI Course and developed a bit further using some tips from other resources — shout out to Guy In A Cube for some very cool tips and videos.

### The Data
This data comes from Maven Analytics and is hypothetical, as mentioned above. The data was stored in 3 separate tables, with 56,046 rows of sales data, 1,809 rows of returns data and 293 rows of product data. The raw data is provided as part of this course and so is only accessible as part of this course.

### Dashboard Link : https://app.powerbi.com/groups/me/reports/07c60e09-03e3-45f7-a204-3b454075967c/ReportSectiond0276a7b2ed48bb206a0?experience=power-bi

## Problem Statement

The Adventure Works company represents a bicycle manufacturer that sells bicycles and related accessories to global markets. The dataset contains 
* Product data (Product Key, Product Price, SKU Type, etc.,)
* Customer data (Customer Key, First Name, Last Name, Income Level, etc.,)
* Sales data (Order Date, Territory Key, Order Quantity, etc.,)

The following dashboards helps paint a picture as to how the store operates under various circumstances.

* Executive Dashboard - A Holistic View of the overall business
* Geographic Analysis - Region-wise business condition
* Product Details - Real-time  product and accessories report
* Customer Details - Real-time customer report


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present except column named "Customer Table" 
- Step 5 : Null values were replaced by Zeros and errors related to customer's birthdate were not taken into account to eliminate result skewness 
- Step 6 : In the report view, under the view tab, theme was selected
- Step 7 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option company's logo was added to the report design area
- Step 8 : Calculated column was created in which, customer's were segmented into income levels, education categories, and Priority segments (based on annual income)

for creating new column following DAX expression was written;
        
       Customer Priority = 
                    IF(
                        'Customer Lookup'[AnnualIncome] > 100000 &&
                        'Customer Lookup'[Is Parent?] = "Yes", "Priority",
                        "Standard")

![customer_priority_1](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/5150ee52-9016-4251-9b45-f1e0d126f803)

        
- Step 9 : New measure was created to find total revenue, revenue target to name a few (total 40 Measures were calculated for this project)

Following DAX expression was written for the same,
        
        Total Revenue = 
                    SUMX(
                        'Sales Data',
                        'Sales Data'[OrderQuantity]
                        *
                        RELATED(
                        'Product Lookup'[ProductPrice]
                        ))       
A card visual was used to represent Total Revenue (in $)

![snip3_total_revenue](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/83719694-e537-4c9e-851c-41dfc14b7770)

        
 - Step 10 : New measure was created to find  Previous Month Revenue (in $)
 
 Following DAX expression was written to find % of customers,
 
        Previous Month Revenue = 
                            CALCULATE(
                                [Total Revenue],
                                DATEADD(
                                    'Calendar Lookup'[Date],
                                    -1,
                                    MONTH
                                ))
 
 A card visual was used to represent Previous Month Revenue (in $)
 

![snip4_prev_rev](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/4b08bdce-1a04-45f8-9d6e-7ef0aec6281c)

 
 - Step 11 : New measure "Total Return" was created to calculate total number of items retuned & a card visual was used to represent the same
 
 Following DAX expression was written to find total distance,
 
         Return Rate = 
                    DIVIDE(
                        [Quantity Returned],
                        [Quantity Sold],
                        "No Sales")
    
 A card visual was used to represent this total distance.
 
 
 ![snip5_return_rate](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/9485ada0-e3cf-4302-be23-67c330969954)
 
 - Step 18 : The report was then published to Power BI Service.
 
 
![snip6_publish](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/6cf5296e-c107-4f40-aa95-e11e047e1e2f)

# Snapshot of Exec Dashboard

![snip7_exec_dash](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/2f729e43-a7b9-4bb5-b1ac-d33cde5bcc80)

 
 # Snapshot of Geo

![snip8_geo_dash](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/7dae10a2-8f8f-4e8e-bb40-c454877baaf6)

 # Snapshot of Product Details

![snip9_product_dash](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/902c5825-f3c4-4ab6-9999-696ec25323f4)


 # Snapshot of Customer Details

 
![snip10_customer_dash](https://github.com/ZubayerOjhor/E-Commerce-Dashboard/assets/82948527/02491a1e-59d4-4ad5-b28e-d00a71e6e0c2)

# Insights

A multiple page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the 4 dashboards;

### [1] Top Accessory Sold 

  #### Water bottle 30 oz.

   Number of Orders = 3,983

   Revenue = $39,755

   Return Rate = 1.95%

      
           Accessories has the least return rate in comparison 
           to other product types.

### [2] Top Bike Sold 

  #### Road Bike (Mountain-200 Black, 46)

   Number of Orders = 606

   Revenue = $1,241,754

   Return Rate = 2.97%

      
           Bikes has the heighest return rate in comparison 
           to other product types.
           
### [2] Important Metrics

    a) Average Revenue per Customer - $ 1.43k
    b) Average Retail Price - $ 714.4
    c) Adjusted Revenue - $ 24.91M
    d) Adjusted Profit - $ 10.46M
  
  while calculating average rating, null values have been ignored as they were not relevant for some customers. 
  
  These ratings will change if different visual filters will be applied.  
  
  ### [3] Return Metrics 
  
      a) Total Returns - 2k
      b) Bike Returns - 429
      c) Bike Return Rate - 3.08%

 ### [4] Location-based Inferences

  ### Total Customers
 
The heighest number of customers are from the Unied States of America, i.e, 7,235 customers

Canada ranks last for customer count, i.e, 1,499 customers
 
 ### Total Bike Sales (Most Expensive Product Type)
 
The United States holds the record for the most bikes ordered, totaling 4,487

Canada record the least bike orders placed, totaling 858
 
          Thus, USA customers contribute maximum share of profit for the company
 
 ### Top 3 Age Groups 
 
 -  17.83 % customers belong to '50-55' age group
 
 -  15.77 % customers belong to '55-60' age group
 
 -  15.25 % customers belong to '45-50' age group
 
         Thus, maximum customers belong to '50-55' age group
         
### Customer Type

- 71.75 % customers are 'Parents'

- 67.62 % customers are 'Home Owners'
       
       thus, most customers are 'Parents & Home Owners'
