# lab3

### Fabric Dataflow M-Code
All Power Query M-code for Lab 3 is included in the branch `fabric_lab3/`.
Each file corresponds to a query used in the Dataflow Gen2 (query, curated_reviews, BookAggregates, AuthorAggregates, final_curated_reviews)


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


Repeat for other columns (e.g., drop nulls in review_id, user_id for integrity).
