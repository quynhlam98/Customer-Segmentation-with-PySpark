# Customer Segmentation with PySpark

## 📌 Overview
This project analyzes e-commerce customer behavior using PySpark, focusing on exploratory data analysis (EDA) and clustering models for customer segmentation. The goal is to optimize marketing strategies and enhance customer engagement.

## 🎯 Objectives
- Understand customer purchasing patterns, spending habits, and transaction frequency.
- Segment customers based on behavior, location, and spending trends.
- Identify high-value customers to personalize promotions and pricing models.
- Improve inventory management by analyzing product performance.
- Enhance customer experience by identifying satisfaction and retention factors.

## 🔧 Technologies Used
- **Apache Spark & PySpark** for large-scale data processing.
- **Machine Learning (MLlib)** for clustering models.
- **Pandas, NumPy, Matplotlib, Seaborn** for EDA and visualization.


**Project Outline**

**I. Get Data**

1. Import Necessary Libraries:
2. Import and Read Data:
    - Load the dataset (e.g., from CSV or database) and view its structure.

**II. Exploratory Data Analysis (EDA) & Data Cleaning**

1\. General Information about the Data

- Inspect Data:
  - Use data.info(), data.shape, and data.describe() to understand the basic structure, size, and distribution of the dataset.
- Check the Number of Columns (Variables):
  - Identify and classify the variables into categorical, numerical, and temporal features:
    - Categorical Features: InvoiceNo, StockCode, Description, CustomerID, Country.
    - Numerical Features: Quantity, UnitPrice.
    - Temporal Feature: InvoiceDate.

2\. Handling Missing Values

- Identify Missing Values:
  - Calculate the percentage of missing values for each column and visualize using a bar chart.
  - Focus on handling missing values in CustomerID.
    - Consider replacing missing CustomerID values based on InvoiceNo or removing rows with missing CustomerID entries.

3\. Data Cleaning

- Remove Duplicates:
  - Identify and drop duplicate rows using data.drop_duplicates().
- Handle Data Types:
  - Convert columns to appropriate data types:
    - Categorical: InvoiceNo, StockCode, Description, CustomerID, Country.
    - Numerical: Quantity, UnitPrice.
    - Temporal: InvoiceDate -> Convert to datetime format.

4\. Handling Outliers in Numerical Variables

- Outlier Detection and Handling:
  - Use the Interquartile Range (IQR) method to detect and handle outliers.
  - Replace outliers with the lower and upper bounds.

5\. Handling Special Cases in Quantity and UnitPrice

- UnitPrice:
  - Replace UnitPrice = 0 with the mode (most common price) for each StockCode.
  - Visualize the distribution of UnitPrice using a boxplot.
- Quantity:
  - Check for Quantity < 0, which might indicate canceled transactions.
  - Calculate the percentage of canceled orders over total orders.
  - Validate two assumptions:
        1. Each canceled order is independent.
        2. Each canceled order has a counterpart with the exact same quantity in the dataset.
  - Remove canceled transactions that have no corresponding orders.

6\. EDA for Categorical Variables

- Summary Statistics for Categorical Variables:
  - Explore categorical variables, such as the number of unique products, customers, and countries.
- Bivariate Analysis:
  - Create visualizations to explore the relationships between Country and CustomerID, as well as Description (Product) and CustomerID.

III. Store Transaction and Product Information into MongoDB

1. Store cleaned transaction and product data into MongoDB.
2. Retrieve data from MongoDB and create a PowerBI Dashboard.

**IV. Feature Engineering (Perform Customer Segmentation)**

1\. Create RFM Model

- Recency (R): Number of days since the last purchase.
- Frequency (F): Total number of invoices submitted by each customer.
- Monetary (M): Total monetary value of each customer’s purchases.
- Create RFM DataFrame:
  - Columns: CustomerID, Recency, Frequency, Monetary.

2\. K-means Clustering

- Preprocessing:
  - Scale the RFM data to bring attributes to the same scale using StandardScaler.
- Determine Optimal Number of Clusters:
  - Use the Elbow Method to choose the optimal number of clusters by plotting distortion scores against the number of clusters.
  - Evaluate the model using the Silhouette Score.
- Model Building:
  - Fit K-means with the selected number of clusters and assign labels to each customer.
- Cluster Analysis:
  - Apply the clustering results back to the RFM DataFrame and analyze the characteristics of each cluster.
- Cluster Characteristics:
  -  Cluster 0: New Customer - Buy recently but few times, low spending
  -  Cluster 1: Potential Customer - Buy is not too often but has the potential to spend
  -  Cluster 2: Churned Customer - Haven’t returned in a long time and have very low purchase activity
  -  Cluster 3: VIP Customer - They purchase frequently and spend a lot

**V. Implementation and Interpretation**

- Create Dashboard:
  - Build visualizations to present cluster insights (Power BI Dashboard)
  - Highlight key characteristics and actionable recommendations for each segment.
- Business Strategy:
Group 0 (New Customers):
Engage them with welcome programs and next-purchase discounts to convert them into loyal customers.
Group 1 (Potential Customers):
Encourage them with special offers, discounts, and incentives to increase purchase frequency.
Group 2 (Churned Customers):
Use reactivation campaigns (emails, promotional vouchers, surveys to understand why they left).
Group 3 (VIP Customers):
Implement VIP benefits, loyalty rewards, and personalized offers to retain them.


