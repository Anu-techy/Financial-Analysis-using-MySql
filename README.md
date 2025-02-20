# Financial-Analysis-using-MySql

**Aim** To Analyze sales of the company to unveal hidden insights and give actionable recommendations

Analysing Sales of a Hardware company based on

Customer Performance Report
Market Performance Report
KPI (Key Performance Indicators)

**Description:**

**Atliq** is a hardware company which manufactures electronic hardware items like PC, Laptop, Hard Drive, mouse, Keyboards, pendrives etc It has operations all over the globe.

It sells to consumers throught the following **distribution channels:**

                  1. Direct Channel (Atliq E-stroe, Atliq Exclusive)
                  2. Retailer (Croma, amazon)
                  3. Distributer(Eg- Neptune in China)

It has two **platforms**

                  1. Brick and Mortar (like Croma, BestBuy)
                  2. E-commerce ( like Amazon, Flipkart)

**Key Values to calculate Profit and Loss Statement**

The **Gross Price** refers to the total price of a product or service before any deductions, such as taxes, discounts, or other costs, are subtracted.

A **Pre invoice Deductions** refers to a reduction or discount applied to the price of goods or services before the final invoice is issued.

**Net invoice sales** refers to the total amount of sales revenue that a company recognizes on an invoice after accounting for any deductions, such as discounts, allowances, returns, or any other reductions that might apply.

                                              Net invoice sales = Gross Price - Pre invoice Deductions

**Post invoice Deductions** are reductions made to the amount due on an invoice after it has been issued. These deductions usually occur after the sale has been completed and the invoice has been sent, and they can be due to various volumne discounts, returns, product defects, shipping delays etc.

**Net sales** refers to the total revenue a company generates from selling goods or services after accounting for all deductions such as discounts, returns, allowances, and any other adjustments. It represents the actual sales the company made and is an important metric for understanding the business's true revenue.

                                              Net Sales = Net invoice Sales - Post invoice Deductions

**COGS** includes all the costs that are directly tied to the production process, such as the cost of raw materials, labor, and manufacturing expenses.
                                              
                                              Cost of Goods Sold (COGS) = Manufacturing Cost + Freight (Transportation Cost) + Other Cost    

**Gross margin** is a financial metric that represents the difference between net sales and cost of goods sold (COGS). It shows how much money a company makes from its core business activities, excluding other expenses such as operating costs, taxes, and interest.

                                              Gross Margin = Net Sales - COGS


Gross margin is a key performance indicator for companies to assess their financial health and operational efficiency.
It gives :

**Profitability** Insight: A higher gross margin typically indicates a company is more efficient at producing goods or services at a lower cost, which can be a sign of strong management and competitive advantage.

**Pricing Strategy:** It helps assess whether a company is pricing its products effectively to cover production costs and generate a reasonable profit.

                                            Gross Margin % = ( GM / NS )*100
                                              

**ETL (Extract Transform Load) Process**

Data is given in various excel sheets. Extracted Data through various sources

Dimension tables : dim_customer, dim_product, dim_market

Fact table/Transaction table : fact_sales_monthly

**Data Transformations in Power Query**

Removed duplicate values

Removed data with missing values (only 3 rows)

Identified, replaced spelling mistakes in customer names

Replaced nan category in market table to NA (North American Region) ater confirming with business owners

Few rows have negative quantity , Replaced with positive after clear confirmation

Named all the data transformation steps

Load the data to data model

Created dim_date table with date, month, FY (fiscal_year) columns.

The Dim_Date table helps in analysis by providing a structured way to categorize and group data based on time (e.g., by day, month, quarter, or year), enabling easier and more flexible time-based analysis, such as trend analysis, period-over-period comparisons, and time-based calculations (like YTD or MTD). Fiscal year of Atliq hardware is from september through August.

**Data Modelling**

dim_custommer(customer_code) ---> fact_sales_monthly(customer_code) one to many

dim_product(product_code) ---> fact_sales_monthly(product_code) one to many

We cannot connect dim_market directly to fact_sales_monthly as there is no common column between dim_market and fact_sales_monthly table. Hence we connect dim_market to dim_customer

dim_market(market) ---> dim_customer(market) one to many

dim_date(date) ---> fact_sales_monthy(date) one to many

DAX Measures created for Customer Performance Report

In the Power Pivot, Created the following DAX measures in the fact_sales_monthly table

Measure 1: Net Sales = SUM(fact_sales_monthly[net_sales_amount])

To create net sales measure for 2019,2020 and 2021, got FY column of dim_date to fact_sales_monthly table using the formula =RELATED(dim_date[FY])

Measure 2: Net Sales 19 = CALCULATE ( [Net Sales], dim_date[FY]="2019")

Measure 3: Net Sales 20 = CALCULATE ( [Net Sales], dim_date[FY]="2020")

Measure 4: Net Sales 21 = CALCULATE ( [Net Sales], dim_date[FY]="2021")

Measure 5: 21 vs 20 = DIVIDE([Net Sales 21],[Net Sales 20],0)

Final Customer Performance Report Designing

In the Power Pivot:

Row : Customer (dim_customer)

Values: Net Sales 19

                    Net Sales 20
      
                    Net Sales 21

                    21 vs 20
Filters: Region (dim_market)

                    Market  (dim_market)
      
                    Division (dim_product)
Added conditional formatting and improved aesthetics

===============================================================

Objective To Create a Market Performance Report

Note: Here market is the country name where the sales are analyzed.

ETL (Extract Transform Load) Process

Separate ns_target_2021 table in .csv file is provided by the business owner. Extracted the same and loaded to the Data model after transformation in power query.

Data Modelling

dim_market(market) ---> ns_targets_2021(market) one to many

dim_date(date) ---> ns_targets_2021(date) one to many

DAX Measures created for Market Performance Report

In the Power Pivot, Created the following DAX measures in the fact_sales_monthly table

Measure 1: Target 21 = SUM(ns_targets_2021[ns_target])

Measure 2: 2021 target = [Net Sales 21] - [Target 21]

Measure 3: % Change = DIVIDE([2021 target],[Net Sales 21],0)

Final Market Performance Report Designing

In the Power Pivot:

Row : market (dim_market)

Values: Net Sales 19

                    Net Sales 20
      
                    Net Sales 21

                    2021 target
Filters: Region (dim_market)

                    Division (dim_product)
Added conditional formatting and improved aesthetics

Recommendations

Use Report to

Understand customers and market performance over the time

Slice and dice data to drill down the hidden insights

Determine discounts, helps to negotiate with consumers, and identify potential business expansion opportunities in promising countries.
