# athletic_sales_analysis
Module 5 Challenge

Athletic Sales Analysis:
This project analyzes sales data for athletic products in 2020 and 2021. The goal is to gain insights into sales trends, like the number of products sold and total sales in different regions. We also focus on analyzing sales of women's athletic footwear. The analysis is done using Python and Pandas.

Introduction:
In this project, we analyze sales data for athletic products. We aim to answer questions like which regions sold the most products and which days had the highest sales. We also look at sales of women's athletic footwear specifically.

Data Description:

The project uses two CSV files:
1. athletic_sales_2020.csv: Sales data for the year 2020
2. athletic_sales_2021.csv: Sales data for the year 2021

Columns in the Data
1. retailer: Name of the retailer
2. retailer_id: ID of the retailer
3. invoice_date: Date of the sale
4. region: Region where the sale occurred
5. state: State where the sale occurred
6. city: City where the sale occurred
7. product: Name of the product
8. price_per_unit: Price per unit of the product
9. units_sold: Number of units sold
10. total_sales: Total sales amount
11. operating_profit: Operating profit from the sale
12. sales_method: Method of sale (e.g., online, in-store)

Setup:

First, you need Python installed on your computer. You'll also need the Pandas library. Install Pandas with this command:
1. pip install pandas
2. Download the athletic_sales_2020.csv and athletic_sales_2021.csv files and save them in the same directory as your script.

Follow these steps:

1. Loading Data
    1. We start by loading the sales data from CSV files into Pandas DataFrames.
        2. import pandas as pd
           1. sales_2020 = pd.read_csv('athletic_sales_2020.csv')
           2. sales_2021 = pd.read_csv('athletic_sales_2021.csv')

2. Inspecting Data
    1. To get a quick look at the data, we use the head() method.
        1. print(sales_2020.head())
        2. print(sales_2021.head())
    2. We also check the data types to ensure they're correct.
        1. print(sales_2020.dtypes)
        2. print(sales_2021.dtypes)

3. Combining Data
    1. We combine the data from 2020 and 2021 into one DataFrame and reset the index.
        1. sales = pd.concat([sales_2020, sales_2021]).reset_index(drop=True)

4. Cleaning Data
    1. Check for any missing values in the data.
        1. print(sales.isnull().sum())

5. Convert the invoice_date column to a datetime type.
    1. sales['invoice_date'] = pd.to_datetime(sales['invoice_date'])

6. Analyzing Sales
    1. Group the data by region, state, and city to find out the total products sold.
        1. products_sold = sales.groupby(['region', 'state', 'city'])['units_sold'].sum().reset_index()
        2. products_sold.rename(columns={'units_sold': 'Total_Products_Sold'}, inplace=True)

7. Using Pivot Tables
    1. Create pivot tables to summarize sales data.
        1. pivot_table_total_sales = pd.pivot_table(sales, index=['region', 'state', 'city'], values='total_sales', aggfunc='sum')
        2. pivot_table_total_sales.rename(columns={'total_sales': 'Total Sales'}, inplace=True)

    2. Filter the data to focus on women's athletic footwear.
        1. womens_footwear_sales = sales[sales['product'] == "Women's Athletic Footwear"]
    
    3. Group the filtered data to find out the total women's athletic footwear sold.
        1. womens_footwear_sold = womens_footwear_sales.groupby(['retailer', 'region', 'state', 'city'])['units_sold'].sum().reset_index()
        2. womens_footwear_sold.rename(columns={'units_sold': 'Womens_Footwear_Units_Sold'}, inplace=True)

    4. Create a pivot table for women's athletic footwear sales.
        1. pivot_table_womens_footwear = pd.pivot_table(womens_footwear_sales, index=['retailer', 'region', 'state', 'city'], values='units_sold', aggfunc='sum')
        2. pivot_table_womens_footwear.rename(columns={'units_sold': 'Womens_Footwear_Units_Sold'}, inplace=True)

8. Resampling Data
    1. Resample the data to get daily and weekly sales.
        1. pivot_table_daily_sales = pd.pivot_table(womens_footwear_sales, index='invoice_date', values='total_sales', aggfunc='sum')
        2. pivot_table_daily_sales.rename(columns={'total_sales': 'Total Sales'}, inplace=True)

        3. daily_sales = pivot_table_daily_sales.resample('D').sum()
        4. daily_sales_sorted = daily_sales.sort_values(by='Total Sales', ascending=False)

        5. weekly_sales = pivot_table_daily_sales.resample('W').sum()
        6. weekly_sales_sorted = weekly_sales.sort_values(by='Total Sales', ascending=False)

9. Results
    1. Here are some of the results from the analysis:
        1. Top 5 regions, states, and cities by total products sold:
            1. top_5_results = products_sold.sort_values(by='Total_Products_Sold', ascending=False).head()
                print(top_5_results)
        2. Top 5 regions, states, and cities by total sales:
            1. top_5_sales = pivot_table_total_sales.sort_values(by='Total Sales', ascending=False).head()
                 print(top_5_sales)
        3. Top 5 retailers by women's athletic footwear sales:
            1. top_5_retailers = pivot_table_womens_footwear.sort_values(by='Womens_Footwear_Units_Sold', ascending=False).head()
            2. print(top_5_retailers)
        4. Top 5 days by total sales:
            1. print(daily_sales_sorted.head())
        5. Top 5 weeks by total sales:
            1. print(weekly_sales_sorted.head())

Conclusion:
This analysis helps identify key trends in athletic sales, focusing on the best-selling products, regions, and times for women's athletic footwear. These insights can help businesses make data-driven decisions to optimize their sales strategies.

Contact:
For any questions or feedback, please contact Sandokan Stage at sandokan.stage@du.edu.

