# Amazon_Vine_Analysis
Analyzing the Amazon reviews written by members and non-members of the paid Amazon Vine program.<br>

## Overview of the Analysis
Big data is a combination of structured, semistructured and unstructured data collected by organizations that can be mined for information and used in machine learning projects, predictive modeling and other advanced analytics applications.Spark is an advanced and flexible ecosystem for handling BigData.Natural Language Processing is a critical big data concept and skillset because there is so much spoken and written language that needs to be translated.We use NLP in Spam filters,spell check and voice recognition technologies.PySpark is an interface for Apache Spark in Python. It not only allows you to write Spark applications using Python APIs, but also provides the PySpark shell for interactively analyzing our data in a distributed environment.We will be using Amazon Web Services which is a cloud computing platform that provides customers with a wide array of cloud services. We can define AWS (Amazon Web Services) as a secured cloud services platform that offers compute power, database storage, content delivery and various other functionalities.Here we will be using AWS Relational Database Service for performing ETL operations on the Big data.

## Purpose of the Analysis
The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.In this analysis, we have access to approximately 50 datasets. Each one contains reviews of a specific product, from clothing apparel to wireless products. We have picked reviews of wireless products datasets and used PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. we have used PySpark to determine if there is any bias toward favorable reviews from Vine and Non-Vine members in our dataset. 

## Resources
DataSources: [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)<br>
Software used: Google Colaboratory, Amazon Web Services RDS, Postgres SQL.<br>
Technology: PySpark<br>


## Deliverable 1: Perform ETL on Amazon Product Reviews
Using the knowledge of the cloud ETL process, we have created an AWS RDS database on the cloud,Wireless products review dataset has been picked for the analysis.The dataset has been extracted and converted to DataFrame using PySpark. we will transform the DataFrame into four separate DataFrames that match the table schema in pgAdmin. Then we will upload the transformed data into the appropriate tables and run queries in pgAdmin to confirm that the data has been uploaded.
The Amazon Review datasets would look like the following image<br><br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/dataset.png"  width = 900><br>
We need to create a database for the Amazon RDS server in the pg admin,We need to create the following tables by running the schema,customers_table, products_table, review_id_table, and vine_table.

### The customers_table DataFrame
To create the customers_table, we need to open the Google Colab and import the PySpark Packages and the dataset is read using PySpark and converted to Dataframe.perform the steps below to aggregate the reviews by customer_id.Using the groupby() function on the customer_id column of the DataFrame we created,Count all the customer ids using the agg() function by chaining it to the groupby() function. After we use this function, a new column will be created, count(customer_id).Rename the count(customer_id) column using the withColumnRenamed() function so it matches the schema for the customers_table in pgAdmin.The final customers_table DataFrame would look like this:<br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/customer_df.png"  width = 300><br>

### The products_table DataFrame
To create the products_table,we need to use the select() function to select the product_id and product_title, then drop duplicates with the drop_duplicates() function to retrieve only unique product_ids.The final products_table DataFrame would look like this:<br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/product_df.png"  width = 300><br>

### The review_id_table DataFrame
To create the review_id_table, we use the select() function to select the columns that are in the review_id_table in pgAdmin, and convert the review_date column to a YYYY_M_D date format. The final review_id_table DataFrame would look like this:<br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/review_id_df.png"  width = 600><br>

### The vine_table DataFrame
To create the vine_table, we use the select() function to select only the columns that are in the vine_table in pgAdmin.The final vine_table DataFrame should look like this:<br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/vine_df.png"  width = 600><br>

### Load the DataFrames into pgAdmin
Make the connection to our AWS RDS instance.Load the DataFrames that correspond to tables in pgAdmin.In pgAdmin,we need to run query to check that the tables have been populated.<br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/customers_table.png"  width = 900><br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/products_table.png"  width = 1100><br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/review_id_table.png"  width = 1100><br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/vine_table.png"  width = 1100><br>

## Deliverable 2: Determine Bias of Vine Reviews
Using the knowledge of PySpark we will determine if there is any bias towards reviews that were written as part of the Vine program. For this analysis, we will determine if having a paid Vine review makes a difference in the percentage of 5-star reviews.
First we need to filter the data and create a new DataFrame to retrieve all the rows where the total_votes count is equal to or greater than 20 to pick reviews that are more likely to be helpful and to avoid having division by zero errors later on.
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/greater%20than%2020.png"  width = 900><br>

Next we will filter the greater than 20 vote count DataFrame and create a new DataFrame to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/greaterthan50.png"  width = 900><br>

Filter the greater than or equal to 50% DataFrame and create a new DataFrame that retrieves all the rows where a review was written as part of the Vine program (paid), vine == 'Y'.
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/vine_review_Yes.png"  width = 1000><br>

Filter the greater than or equal to 50% DataFrame and create a new DataFrame that retrieves all the rows where a review was written as part of the Vine program (unpaid), vine == 'N'.
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/non-vine%20review_No.png"  width = 1000><br>

The total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid) is calculated 
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/vinereview.png"  width = 600><br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/non-vine%20reviews.png"  width = 600><br>

## Results
### Paid(Vine) Reviews:
- Total number of Vine reviews:**613**
- The number of Vine reviews were 5 stars:**222**
- The  percentage of Vine reviews were 5 stars:**36.215%**
### Unpaid(Non-Vine) Reviews
- Total number of non-Vine reviews:**64968**
- The number of non-Vine reviews were 5 stars:**30543**
- The percentage of non-Vine reviews were 5 stars:**47.0123%**

## Summary

In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/avg%20vine%20review.png"  width = 900><br>
<img src = "https://github.com/fathi129/Amazon_Vine_Analysis/blob/master/screenshots%20for%20AWS/non-vine%20avg%20mean.png"  width = 900><br>


