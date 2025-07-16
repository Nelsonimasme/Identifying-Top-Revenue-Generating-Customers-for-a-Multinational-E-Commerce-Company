# Identifying-Top-Revenue-Generating-Customers-for-a-Multinational-E-Commerce-Company
This data science research project presents a comprehensive sales analysis of a leading multinational e-commerce company headquartered in the United States, with operations spanning across North and South America, as well as Europe



# Project Overview
This data science research project presents a comprehensive sales analysis of a leading multinational e-commerce company headquartered in the United States, with operations spanning across North and South America, as well as Europe. 

The objective of the study is to analyze and identify the **Top 10 highest revenue-generating customers**, offering critical business insights into customer value, regional sales dynamics, and strategic growth opportunities.

Leveraging advanced data analytics techniques, including data preprocessing, aggregation, and visualization, this project uncovers key patterns in customer spending behavior across diverse markets. 

By ranking customers based on total revenue contribution, the analysis empowers business stakeholders with actionable intelligence to optimize customer relationship management, tailor marketing strategies, and enhance profitability in a globally competitive landscape.

This project serves as a practical application of data science principles in the domain of e-commerce, showcasing the impact of data-driven decision-making on strategic business outcomes.

### Problem Statement  
**Who are Top 10 Customers of the Company interms of Total Revenue generated since the company started ?**

### Project Objectives 

1. **To Identify Top Revenue-Generating Customers**
   * By Analyzing sales data to determine the top 10 customers contributing the highest total revenue across all regions.

2. **To Understand Revenue Concentration**
   * By Analyzing how much of the company's total revenue is concentrated among top customers.

3. **To Uncover Geographic Patterns**
   * By Assessing the global distribution of high-value customers across the Countries to identify key markets and regional revenue   clusters.

4. **To Support Strategic Decision-Making**
   * By Providing actionable insights to the company’s sales and marketing teams for developing targeted retention, loyalty, and upselling strategies.

5. **To Demonstrate Real-World Data Science Application**
   * By Showcasing the use of data science tools and techniques (data preprocessing, aggregation, visualization) in solving a real-world business problem.

6. **To Enable Stakeholder Communication**
   * By Creating intuitive visualizations and summaries that allow non-technical stakeholders to understand key findings and insights.

7. **To Lay the Groundwork for Predictive Modeling**
   * By Establishing a foundational dataset and insights that could be extended into customer lifetime value prediction or churn modeling in future phases.


 ### Data Source
  **The Company's central transaction database**

### Project Methodology
  **Data Collection**: Data was collected from the Company's Central Transaction Database

- **Data Pre-processing**: Loaded the data from a CSV file into a Pandas Dataframe

- **Data Inspection and Cleaning**: Checked for Missing values, Checked for Duplicates.
- - Handled missing values
  - Handled duplicate values

- **Data Modification**: generated some  core metrics which were NOT provided from the dataset, and would be required for the purpose of the data   analysis

- **Data Aggregation**: To Compute the major metric : Total Revenue by Customer**

- **Data Sorting/ Data Ranking**: To Determine the Most Importat Metric:  **Top 10 highest revenue-generating customers**

- **Data Visualization**: To uncover the **Top 10 highest revenue-generating customers** in a pictorial form.

- **Data Interpretation**:

- **Key Findings**

- **Conclusions**

- **Recommendation**

### Data Collection
Sales data was obtained from a central transaction database of the company representing orders placed by customers across multiple countries. Each record included attributes such as:

* `Customer ID`
* `OrderNo`
* `OrderQuantity`
* `CostPrice_usd`
* `SellingPrice_usd`
* `OrderDate`
* `CustomerName`
* `CustomerCity`
* `CustomerState`
* `CustomerCountry`
* `ProductCategory`
* `ProductColor`
* `Model`

### Data Pre-processing
**Data Loading**: 
Reading the Raw Dataset which originally existed as a CSV file into a Pandas Dataframe

__Task:__ Follow the appropriate steps in reading a CSV file into a pandas Dataframe, 

and  Read the data stored  in the csv file named:  `bikes` From your computer.
The resulting Dataframe should be named : `bikes_df`

```python
# solution
import pandas as pd
bikes_df = pd.read_csv("C:/Users/HP/Downloads/bikes.csv")

bikes_df.head()

```


<img width="887" height="239" alt="data_pre_processing" src="https://github.com/user-attachments/assets/a44375bf-e542-471c-b23d-dadf36210685" />



### Data Inspection and Cleaning

- **1. Check for Missing values**:


```python
# solution 
bikes_df.isna().any()

```
<img width="209" height="202" alt="checking_for_missing_value" src="https://github.com/user-attachments/assets/a37309f3-dbdf-4a4a-b195-7e6c6060cd8e" />





```python
# counting the number of missing values 

# solution 
total_number_of_missing_values_by_columns = bikes_df.isna().sum()

total_number_of_missing_values_by_columns
```

<img width="181" height="182" alt="counting_number_of_missing_values" src="https://github.com/user-attachments/assets/ef4fcc1c-d50a-44af-aacb-3443f03dcd3f" />



**2.# visualizing total numbers of missing values**:

```python



import matplotlib.pyplot as plt


total_number_of_missing_values_by_columns.plot(kind = "bar")

# to show yoyr plot

plt.show() 


```


<img width="508" height="359" alt="visualizing _no_of_missing_values" src="https://github.com/user-attachments/assets/464bdac2-09dc-4bea-a26c-ee97b2cb512d" />



 **2.Handling Missing values**: 

```python
# solution 

# how to get the most popular value
# solution
bikes_df["ProductColor"].mode()

# bikes_df.fillna()
```

<img width="339" height="186" alt="most_popular_value" src="https://github.com/user-attachments/assets/3e215523-d562-4743-974a-0310d693c4cf" />



 ```python
# replacing the missing Value
# solution

bikes_df = bikes_df.fillna("Black")
bikes_df
```

<img width="839" height="263" alt="replacing_missing_values" src="https://github.com/user-attachments/assets/834f481b-5eda-44b7-8e22-2c08253f0b29" />



```python
# to veryfiy that there are no more  missing Values

bikes_df.isna().any()

```

<img width="226" height="178" alt="verifying_missing_values" src="https://github.com/user-attachments/assets/f92fc2c9-bb61-468a-890e-c5dca6047a77" />



- **3. Check for  Duplicates**:

```python
# Dropping any duplicates if any exists

# solution

bikes_df.drop_duplicates(inplace = True)

```



- **4. Handling Duplicates**:

```python
# re-counting our data point again

# solution
len(bikes_df)
```

<img width="358" height="135" alt="recounting_data_point" src="https://github.com/user-attachments/assets/565d065f-cc63-4141-8321-57237e6a382f" />



### Data Modification

```python
# generating some core metrics which were NOT provided from the dataset, which would be required for the purpose of the data analysis

# solution 

# (1) TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 


# (2) SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 


# (3) Profit : To be obtained by (SalesRevenue - TotalCostPrice)


bikes_df["Profit"] = bikes_df["SalesRevenue"]  - bikes_df["TotalCostPrice"]


# Displaying the result

bikes_df

```

<img width="548" height="222" alt="data_modification" src="https://github.com/user-attachments/assets/f9115bc7-723e-41ef-8879-0b21c13dc542" />


### Data Aggregation

```python

# Computing/ Aggregating the sales data to show Total Revenue by Customer , including their City, State and Country. 

# solution



# Computing the total revenue by customers

total_revenue_by_customer = bikes_df.groupby(["CustomerName", "CustomerCity", "CustomerState",
                                              "CustomerCountry"])["SalesRevenue"].sum().reset_index()


total_revenue_by_customer
```


<img width="458" height="304" alt="data_aggregation" src="https://github.com/user-attachments/assets/9f45883a-43a6-47de-abaa-40aa5f303c0e" />




### Data Sorting/ Data Ranking

```python
# To Determine the Most Importat Metric: Top 10 highest revenue-generating customers 

# solution 

The_top_10_customers = total_revenue_by_customer.sort_values("SalesRevenue", ascending = False).head(10)


The_top_10_customers

```


<img width="502" height="254" alt="data_sorting_data_ranking" src="https://github.com/user-attachments/assets/d9c5aaa9-6c5b-4261-ab56-6427d95948d7" />



### Comparison of the total Revenue Generated by the  Top 10 Customers to the entire Total Revenue of The Company

```python
# total Revenue Generated by the Top 10 Customers
# Solution 

revenue_sum_of_top_10_customers = The_top_10_customers["SalesRevenue"].sum().round(2)

revenue_sum_of_top_10_customers

```


```python
# entire Total Revenue of The Company

revenue_sum_of_the_entire_company = bikes_df["SalesRevenue"].sum().round(2)

revenue_sum_of_the_entire_company

```

```python

Percentage_rev_top_10_customers = (revenue_sum_of_top_10_customers/revenue_sum_of_the_entire_company)*100

ratio = Percentage_rev_top_10_customers.round(2)

ratio

```


<img width="653" height="319" alt="total_revenue_of_the_top_10_customers" src="https://github.com/user-attachments/assets/b6176bcd-4ac5-40e8-915b-d912c6373066" />



```python
print(f"The Total Revenue generated by the top customers , account for {ratio}% of the company total revenue")

```

<img width="709" height="56" alt="print_call" src="https://github.com/user-attachments/assets/6a42274e-a482-437a-b17c-1c0d9a6a6bb8" />




### Data Visualization

```python
#  To uncover the Top 10 highest revenue-generating customers in a pictorial form.

# solution 

import matplotlib.pyplot as plt

The_top_10_customers.plot(kind = "bar", x = "CustomerName", y = "SalesRevenue", color = "Green")

# Axis Label
plt.xlabel("Customer Name")
plt.ylabel("Total Sales Revenue in US DOLLARS $")


# Title label
plt.title("Top 10 Customers By Total Revenue Since The Company Started")

# to show the plot
plt.show()

```



<img width="391" height="333" alt="data_visualization" src="https://github.com/user-attachments/assets/6d8f97c5-5a11-4261-bfa0-e086350df881" />



### Data Interpretation

The Result from the data visualization above, shows that all the **Top 10 customers** are all based in **France**

### Key Findings

---

1. **France Dominates among Top-Tier-High-Value-Customers**: 
   All **The Top 10 Customers** are based in **France**, indicating a strong customer base and market penetration in this region.


2. The Company's **Top 10 Customers** Contribute Less Than **1% of Total Revenue of the  entire company**.

   
   Despite **France** being the **top revenue generators**, these customers collectively account for a **very small fraction** of the company's overall sales — indicating **broad and diversified revenue streams**.

4. **Revenue is Distributed, Not Concentrated**
   Unlike typical e-commerce businesses that follow the Pareto Principle (80% of revenue from 20% of customers), this company’s revenue is **evenly spread across thousands of customers**, highlighting a mass-market model.


5. **High-Value Customers Are Geographically Clustered**
   The top revenue-generating customers are concentrated in specific cities and departments such as:

   * **Tremblay-en-France**, **Les Ulis**, and **Saint-Denis** in **Seine Saint Denis** and **Essonne**
   * Major urban centers like **Paris**, **Metz**, and **Dunkerque**

6. **Narrow Revenue Spread Among Top Customers**
   The revenue range of the top 10 customers is relatively narrow—from **\$13,144.88** to **\$13,708.12**, suggesting consistent purchasing behavior across the top customer tier.

7. **Top Customers Still Exhibit Stable Purchasing Behavior**
   While their individual contribution is small relative to total revenue, the top customers show **stable, high-value purchasing patterns** — useful for identifying ideal customer personas or retention targets.

8. **Customer Loyalty and Repeat Purchases Likely**
   Given the similar revenue volumes, it’s likely that these customers have regular or subscription-based purchasing behavior.

---


### Conclusions


The company's sales data analysis reveals that the company operates a **high-volume, low-concentration revenue model**, where no single customer or small group significantly influences total revenue. 

This suggests a **wide customer base**, possibly driven by individual, one-time, or small-ticket purchases.

Furthermore, the sales data reveals that the company’s **top 10 most valuable customers are concentrated entirely in France**, with a significant cluster in **Île-de-France** and surrounding regions. 


This concentration indicates a **strong local market presence**, but also highlights a **potential risk** if the company's sales efforts are overly dependent on a single region.

While the **top 10 customers** do not represent a **major share of total sales**, understanding their behavior is still useful for profiling ideal, repeat-purchase customers. Moreover, the fact that all top performers are from France indicates a **regional pattern** in customer loyalty or market engagement.


However, the **absence of high-revenue customers** from other regions such as the **United States, Canada, Germany, UK, and Australia** points to a **potential gap in customer acquisition** or expansion strategy.

---


### Reconmendation


### 1. **Expand High-Value Customer Acquisition Beyond France**

* Launch targeted marketing campaigns in **United States, Canada, Germany, UK, and Australia** to balance regional revenue dependency.
* Use the profile of these French customers to find “look-alike” customers in other countries.

### 2. **Focus on Scaling Average Customer Spend**

* Instead of concentrating only on top customers, create **broad-based incentives** (e.g., product bundles, loyalty points) to **lift the average order value** across all customers.

### 3. **Replicate High-Value Customer Traits Across the Base**

* Analyze what makes the top 10 customers spend more (location, product type, frequency) and **apply that insight to encourage similar behavior** in the general customer base.


### 4. **Strengthen Customer Retention in France**

* Reward top customers in France with loyalty programs, premium services, or early-access deals.
* Consider customer interviews or surveys to understand what keeps them engaged.


### 5. **Run Regional A/B Tests**

* Test localized marketing efforts in other regions using the same product mix that appeals to French customers.

### 6. **Mitigate Regional Risk**

* Relying heavily on France puts the company at risk in the event of regional disruptions (economic, political, or logistical).
* Diversify revenue sources across other major European and American markets.

```

