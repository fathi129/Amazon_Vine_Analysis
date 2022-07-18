# Amazon_Vine_Analysis
Analyzing the Amazon reviews written by members and non-members of the paid Amazon Vine program. 
## Overview of the Analysis

## Purpose of the Analysis
The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.In this analysis, we have access to approximately 50 datasets. Each one contains reviews of a specific product, from clothing apparel to wireless products. We have picked reviews of wireless products datasets and used PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. we have used PySpark to determine if there is any bias toward favorable reviews from Vine and Non-Vine members in our dataset. 

## Resources
DataSources: [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)<br>
Software used: Google Colaboratory, Amazon Web Services RDS, Postgres SQL.<br>
Language: PySpark<br>




## Deliverable 1: Perform ETL on Amazon Product Reviews
Using your knowledge of the cloud ETL process, you’ll create an AWS RDS database with tables in pgAdmin, pick a dataset from the Amazon Review datasets (Links to an external site.), and extract the dataset into a DataFrame. You'll transform the DataFrame into four separate DataFrames that match the table schema in pgAdmin. Then, you'll upload the transformed data into the appropriate tables and run queries in pgAdmin to confirm that the data has been uploaded.
Follow the instructions below to complete Deliverable 1.

From the following Amazon Review datasets (Links to an external site.), pick a dataset that you would like to analyze. All the datasets have the same schemata, as shown in this image:
Create a new database with Amazon RDS just as you did in this module.

In pgAdmin, create a new database in your Amazon RDS server that you just create.

Download the challenge_schema.sql file to your computer.

In pgAdmin, run a new query to create the tables for your new database using the code from the challenge_schema.sql file.

After you run the query, you should have the following four tables in your database: customers_table, products_table, review_id_table, and vine_table.
Download the Amazon_Reviews_ETL_starter_code.ipynb file, then upload the file as a Google Colab Notebook, and rename it Amazon_Reviews_ETL.
First extract one of the review datasets, then create a new DataFrame.
Next, follow the steps below to transform the dataset into four DataFrames that will match the schema in the pgAdmin tables:




### The customers_table DataFrame

To create the customers_table, use the code in the Amazon_Reviews_ETL_starter_code.ipynb file and follow the steps below to aggregate the reviews by customer_id.

Use the groupby() function on the customer_id column of the DataFrame you created in Step 6.
Count all the customer ids using the agg() function by chaining it to the groupby() function. After you use this function, a new column will be created, count(customer_id).
Rename the count(customer_id) column using the withColumnRenamed() function so it matches the schema for the customers_table in pgAdmin.
The final customers_table DataFrame should look like this:

### The products_table DataFrame
To create the products_table, use the select() function to select the product_id and product_title, then drop duplicates with the drop_duplicates() function to retrieve only unique product_ids. Refer to the code snippet provided in the Amazon_Reviews_ETL_starter_code.ipynb file for assistance.

The final products_table DataFrame should look like this:



### The review_id_table DataFrame
To create the review_id_table, use the select() function to select the columns that are in the review_id_table in pgAdmin (as shown in the following image), and convert the review_date column to a date using the code snippet provided in the Amazon_Reviews_ETL_starter_code.ipynb file.

The final review_id_table DataFrame should look like this:



### The vine_table DataFrame
To create the vine_table, use the select() function to select only the columns that are in the vine_table in pgAdmin (as shown in the following image).

The final vine_table DataFrame should look like this:

### Load the DataFrames into pgAdmin
Make the connection to your AWS RDS instance.
Load the DataFrames that correspond to tables in pgAdmin.
In pgAdmin, run a query to check that the tables have been populated.


## Deliverable 2: Determine Bias of Vine Reviews
Using your knowledge of PySpark, Pandas, or SQL, you’ll determine if there is any bias towards reviews that were written as part of the Vine program. For this analysis, you'll determine if having a paid Vine review makes a difference in the percentage of 5-star reviews.

Using either PySpark, Pandas, or SQL, follow the instructions below to complete Deliverable 2.

Filter the data and create a new DataFrame or table to retrieve all the rows where the total_votes count is equal to or greater than 20 to pick reviews that are more likely to be helpful and to avoid having division by zero errors later on.

Filter the new DataFrame or table created in Step 1 and create a new DataFrame or table to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.

If you use the SQL option below, you’ll need to cast your columns as floats using WHERE CAST(helpful_votes AS FLOAT)/CAST(total_votes AS FLOAT) >=0.5.
Filter the DataFrame or table created in Step 2, and create a new DataFrame or table that retrieves all the rows where a review was written as part of the Vine program (paid), vine == 'Y'.

Repeat Step 3, but this time retrieve all the rows where the review was not part of the Vine program (unpaid), vine == 'N'.

Determine the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid).
Create a new Google Colab Notebook, and name it Vine_Review_Analysis.
Extract the dataset you used in Deliverable 1.
Recreate the vine_table, and perform your analysis using the steps above.
Export your Vine_Review_Analysis Google Colab Notebook as an ipynb file, and save it to your Amazon_Vine_Analysis GitHub repository.

## Results

How many Vine reviews and non-Vine reviews were there?
How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

## Summary

In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.


