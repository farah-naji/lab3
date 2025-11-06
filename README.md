### lab3

### Fabric Dataflow M-Code

All Power Query M-code for Lab 3 is included in the `fabric_lab3` branch.
These files contain the exact transformation steps used in my Fabric Dataflow Gen2
for the Goodreads pipeline.

- `query`  
  The initial connection/query that reads the curated data from the Gold layer
  (curated_reviews) in Azure Storage / Lakehouse.

- `curated_reviews`  
  Basic shaping of the main reviews table (selecting columns, simple cleanup,
  and preparing the data to be enriched with aggregates).

- `BookAggregates`  
  Power Query logic that groups by `book_id` and computes book-level features,
  such as the average rating per book and number of reviews per book.

- `AuthorAggregates`  
  Power Query logic that groups by `author_name` and computes author-level
  features, such as the average rating per author and number of reviews per author.

- `final_curated_reviews`  
  The final enriched dataset where all aggregations are merged back into the
  main curated_reviews table.

NOTE:
Because the UDST Fabric tenant has reached the maximum number of trial capacities,
I could not fully publish the final table into a Lakehouse. Instead, all
transformation logic is saved here as M-code so it can be re-created or
re-executed later once Fabric capacity is available.



for HomeWork 2 these where the steps :

a. Adjust Data Types:
review_id: Text
book_id: Text
author_id: Text
user_id: Text
rating: Whole Number 
n_votes: Whole Number
title: Text
author_name: Text 
review_text: Text
language: Text
date_added: Date


b. Handle Missing or Invalid Values

For each key column (rating, book_id, review_text, etc.):
Remove Rows: Remove Blank Rows


Create review_length column:
Select review_text Add Column then Text then Length "review_length"
Select review_length Filter then Greater than or equal to 10

For date_added:
Select date_added then Date filters then Before : 2025-11-06

Replace missing values:
n_votes Select then Replace Values then Replace null with 0
language: Select then Replace Values then Replace null with "Unknown"




In this lab, we built a full data preprocessing pipeline using Azure Data Lake, Data Factory, Databricks, and Fabric. We uploaded the Goodreads datasets to the raw layer, transformed them to Parquet in the processed layer using ADF, and used Azure Databricks (Spark) to clean and join books, authors, and reviews into the curated_reviews table. Then, in Fabric Dataflow, we used Power Query (M-code) to create book and author aggregates and merged them into final_curated_reviews. Finally, we cleaned and standardized the data in Databricks (removed duplicates, fixed types, normalized text) and saved the final dataset to the Gold layer (/gold/features_v1/) for analysis and machine learning.


Repeat for other columns (e.g., drop nulls in review_id, user_id for integrity).
