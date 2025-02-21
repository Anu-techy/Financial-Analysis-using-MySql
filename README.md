# Trend Analysis using MySql

**Aim** 

Calculating revenue and analysing trends based on

1. Monthly aggregated Sales Report of Croma in FY 2021 using joins and functions
2. Yearly Sales Report of Croma using stored procedures
3. Stored procedure to Determine Market Badge


**Description:**

**Atliq** is a hardware company which manufactures electronic hardware items like PC, Laptop, Hard Drive, mouse, Keyboards, pendrives etc It has operations all over the globe.

It sells to consumers throught the following **distribution channels:**

                  1. Direct Channel (Atliq E-stroe, Atliq Exclusive)
                  2. Retailer (Croma, amazon)
                  3. Distributer(Eg- Neptune in China)

It has two **platforms**

                  1. Brick and Mortar (like Croma, BestBuy)
                  2. E-commerce ( like Amazon, Flipkart)

**ETL (Extract Transform Load) Process**

Data is imported from Atliq Database

**Dimension tables** : 
1. dim_customer (customer_code, customer, platform, market, sub_zone, region)
2. dim_product (product_code, division, segment, category, product, variant)

**Fact tables/Transaction tables** : 

1. fact_sales_monthly (monthly aggregated data in start of the month date, product_code, customer_code, sold_quantity )
2. fact_freight_Cost (market, fiscal_year, freight_pct, other_cost_pct)
3. fact_gross_price (product_code, fiscal_year, gross_price)
4. fact_manufacturing_cost (product_code, cost_year/fiscal_year, manufacturing_cost)
5. fact_post_invoice_deductions (customer_code, product_code, date, discounts_pct, other_deductions_pct)
6. fact_pre_invoice_deductions (customer_code, fiscal_year, pre_invoice_discount_pct)

=======================================================================
                     
**Recommendations**

Use Report to

1. Understand monthly sales of customers and identify last sales months and strategize to improve sales  

2. Understand yearly sales of customers to get Year over year change percentage and plan accordingly

3. Quickly get the market performance by determining market badge

4. Slice and dice data to drill down the hidden insights


