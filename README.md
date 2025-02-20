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

**Key Performance Indicators (KPIs)  to calculate Profit and Loss Statement**

The **Gross Price** refers to the total price of a product or service before any deductions, such as taxes, discounts, or other costs, are subtracted.

A **Pre invoice Deductions** refers to a reduction or discount applied to the price of goods or services before the final invoice is issued.

**Net invoice sales** refers to the total amount of sales revenue that a company recognizes on an invoice after accounting for any deductions, such as discounts, allowances, returns, or any other reductions that might apply.

                                              Net invoice sales = Gross Price - Pre invoice Deductions

**Post invoice Deductions** are reductions made to the amount due on an invoice after it has been issued. These deductions usually occur after the sale has been completed and the invoice has been sent, and they can be due to various volumne discounts, returns, product defects, shipping delays etc.

**Net sales** refers to the total revenue a company generates from selling goods or services after accounting for all deductions such as discounts, returns, allowances, and any other adjustments. It represents the actual sales the company made and is an important metric for understanding the business's true revenue.

                                              Net Sales = Net invoice Sales - Post invoice Deductions

**COGS** includes all the costs that are directly tied to the production process, such as the cost of raw materials, labor, and manufacturing expenses.
                                              
                                Cost of Goods Sold (COGS) = Manufacturing Cost + Freight (Transportation Cost) + Other Cost    

**Gross margin** is a financial metric that represents the difference between net sales and cost of goods sold (COGS). It shows how much money a company makes from its core business activities, excluding other expenses such as operating costs, taxes, and interest. It is a key performance indicator for companies to assess their financial health and operational efficiency. It gives :

**Profitability** Insight: A higher gross margin typically indicates a company is more efficient at producing goods or services at a lower cost, which can be a sign of strong management and competitive advantage.

**Pricing Strategy:** It helps assess whether a company is pricing its products effectively to cover production costs and generate a reasonable profit.


                                            Gross Margin = Net Sales - COGS

                                            Gross Margin % = ( GM / NS )*100
                                              

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



                                                




**Data Modelling**

dim_custommer(customer_code) ---> fact_sales_monthly(customer_code) one to many

dim_product(product_code) ---> fact_sales_monthly(product_code) one to many

We cannot connect dim_market directly to fact_sales_monthly as there is no common column between dim_market and fact_sales_monthly table. Hence we connect dim_market to dim_customer

dim_market(market) ---> dim_customer(market) one to many

dim_date(date) ---> fact_sales_monthy(date) one to many



**Recommendations**

Use Report to

Understand customers and market performance over the time

Slice and dice data to drill down the hidden insights

Determine discounts, helps to negotiate with consumers, and identify potential business expansion opportunities in promising countries.
