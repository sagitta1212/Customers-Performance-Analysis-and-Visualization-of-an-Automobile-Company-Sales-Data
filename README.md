# Sales_Analysis_for_an_Automobile_Company_USA

A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.
## PROBLEM STATEMENT:  
Who are their Top 10 Most-Profitable Customers  in the United States ?
## DATA PRE-PROCESSING
#### DATA LOADING

```python
##  importing all the necessary python packages
# solution 

import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt

print("The packages have been successfully imported")
```

```python
# reading the sales data into a pandas dataframe

bikes_df = pd.read_csv("C:/Users/USER/OneDrive/Desktop/data _set/bikes.CSV")
bikes_df.head()
```
####  Data Modification
```python
# Adding the following columns:
# (1). Add the following 3 columns to your pansdas Dataframe:  bikes_df

# TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 


# SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 


# Profit : To be obtained by (SalesRevenue - TotalCostPrice)

bikes_df["Profit"] = bikes_df["SalesRevenue"] - bikes_df["TotalCostPrice"]

bikes_df.head()
```
## Data Analysis
### Data Filtering
```python
# Filtering out irrelevant data needed to solve their problem
is_USA=bikes_df["CustomerCountry"]=="United States"
USA_Data=bikes_df[(is_USA)]
USA_Data.head()
```
#### Data Aggregation
```python
# Aggregating the filtered data (USA sales data) for each customer
Total_profit_by_customer=USA_Data.pivot_table(values="Profit", index="CustomerName", aggfunc=np.sum)
Total_profit_by_customer
```
#### Data Sorting
```python
# sortingthe aggregated data inorder to rank the customers according to the top profit
Total_profit_by_customer.sort_values("Profit", ascending=False)
```
## Result
```python
Top_10_customers=Total_profit_by_customer.sort_values("Profit", ascending=False).head()
Top_10_customers
```
## Data Visualization
```python
# visualizing the result
Top_10_customers.plot(kind="bar")
# adding a title and label
plt.title("Top 10 Most Customers in the United States")
plt.ylabel("Total Profit")
plt.xlabel("CustomerName")
# Showing the results
plt.show()
```




![project2chart](https://github.com/user-attachments/assets/7b3f8fa7-d538-425c-a822-13c964a948ee)






