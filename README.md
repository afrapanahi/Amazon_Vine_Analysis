# Amazon_Vine_Analysis

## Overview of Project 
In this project, I am using AWS and google colab to analyze product reviews for amazon. I selected 

https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Books_v1_02.tsv.gz

for my analysis which lists book reviews.
## Results
### ELT Amazon product review
-	1. After setting up pyspark and AWS, I loaded the dataset into a  data frame. (See the image below for the code and the outcome)

![res1](/img/fig1.png?raw=true)

-	2. Then, in pgAdmin a new database in Amazon RDS server was created. After downloading the schema and running the query, 4 tables were created.

-	3. In google colab notebook, a data frame of customer_id and number of reviews written by the customer was generated. (See the image below for the code and the outcome)

![res2](/img/fig2.png?raw=true)

-	4. In google colab notebook, a data frame was generated for product_id and product_title (See the image below for the code and the outcome)

![res3](/img/fig3.png?raw=true)

-	5. In google colab notebook, a data frame with review_id, customer_id, product_id, product_parent and review_date was generated (see the image below for the code and the outcome)

![res4](/img/fig4.png?raw=true)

-	6. Finally, in google colab notebook, a new data frame was generated with review_id, star_rating, helpful_votes, total_votes, vine, and verified_purchases was generated. (See the image below for the code and the outcome)

![res5](/img/fig5.png?raw=true)

-	7. The aforementioned data frames were loaded to pgAdmin. (See the image below for the code)

![res6](/img/fig6.png?raw=true)  

-	8. Vine table from pgAdmin was exported as a csv file and used for further analysis.

### Bias in Amazon product review

In the following, I am using the vine data frame to determine if there is any bias from the paid reviewers to give higher ratings. As was mentioned before, I used a database that contains book reviews. To accomplish this task, first, I loaded the vine csv file into a data frame using pandas.  
-	1. As a quick check, I looked at the number of paid (vine == “Y”) versus unpaid (vine==”N”). A simple check showed me that there are only 2 paid reviews in this data set (See image below). 

![res7](/img/fig7.png?raw=true)

-	Each of these had small number of total votes. Therefore, these paid reviews were eliminated in the future analysis since we are looking at reviews with total votes greater or equal to 20.

-	2.  Next, as was mentioned before, we are only keeping reviews with total votes larger or equal to 20 (which eliminates all the paid reviews!!). (See the image below)

![res8](/img/fig8.png?raw=true)

-	3. Next, I only kept the reviews that were find helpful at least 50% of the time (See the image below)

![res9](/img/fig9.png?raw=true)

-	4. All the remaining reviews are unpaid! (total of 403807)(See the image below)

![res10](/img/fig10.png?raw=true)

-	5. Among total of 403807 remaining reviews (that were found helpful at least 50% of the time) 242889 gave 5 stars (See the image below)

![res11](/img/fig11.png?raw=true)

According to this data (242889/403807*100=%60) of the unpaid reviewes are 5 star. I cannot analyze any paid reviews since there were very little of them in this data set.

## Summary
In this project, I looked at the book reviews from amazon. Due to lack of data, I cannot effectively investigate the effect of bias from the paid reviewers in their voting.  
