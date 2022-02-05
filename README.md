# Amazon_Vine_Analysis

## Overview of the Analysis

For this project, I'm analyzing Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

For this project, we used a dataset containing Amazon Reviews on home entertainment appliances.  For this, we used PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin (Postgres SQL). We then use PySpark through Google Colab to determine if there is any bias toward favorable reviews from Vine members in our dataset. 


# Results

In order to ensure that the reviews we are analyzing are more likely to be helpful, we filtered our dataset to only include those reviews that had 20 or more votes.  We then filtered again to ensure that of those votes, atleast 50% of them were deemed as helpful.

How many Vine reviews and non-Vine reviews were there?
In order to find out how many Vine Reviews there were within the filtered Database, we filtered the dataframe by the Vine category and indicated "Y" for all of those that were indicated as Vine reviews in the dataset and then ran the same code but replaced the "Y" with a "N" for the non vine reviews.

![Screen Shot 2022-02-05 at 3 34 06 PM](https://user-images.githubusercontent.com/87248687/152658056-ff2a57ee-96aa-4bd7-b4fa-acad85c98282.png)

<img width="1119" alt="Screen Shot 2022-02-05 at 3 41 04 PM" src="https://user-images.githubusercontent.com/87248687/152658227-03cccfa6-7b8a-43ed-b462-9feef348d02d.png">


We then ran the count function on both of these newly created dataframes and assigned the count to a separate variable for each as shown below.

```
total_vine_reviews = yes_vine_df.count()
```
```
total_nonvine_reviews = no_vine_df.count()
```

* There are 261 paid(vine)reviews </br>
* There are 24,040 unpaid(nonvine)reviews

How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?

In terms of 5 star reviews, we can find out the amount of 5 star vine reviews and 5 star non vine reviews, by simply filtering our yes_vine_df and our no_vine_df to include only 5 star reviews and then running the count function.  We also assign this to a variable so we can use in other calculations later.

```
fivestar_vine = yes_vine_df.filter(yes_vine_df['star_rating']== 5).count()
```
```
fivestar_novine = no_vine_df.filter(no_vine_df['star_rating']== 5).count()
```

* There are 106 five star paid(vine) reviews </br>
* There are 10,899 five star unpaid(nonvine) reviews.

What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

In order to calculate the percentage of 5 star vine reviews, we simply can divide the fivestar_vine by total_vine_reviews and multiply it by 100.  We did the same for the non vine reviews by dividiing fivestar_novine by total_nonvine_reviews and multiplying it by 100.  With both of these lines of code, we performed this inside of the round function.

*41% of the paid(vine) reviews were 5-star reviews
*45% of the unpaid(nonvine) reviews were 5-star reviews



## Summary: 

In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.

Based on the summary of our results, we can see that there is not any positivity bias in the paid reviews versus the unpaid reviews.  In fact, there was a higher percentage of unpaid 5 star reviews than there were for the paid reviews.  One additional analysisd that we could conduct with this dataset, would be to analyze the results for the 4,3,2, and 1 star reviews.  I expect that it would follow a similar trend, since people usually right reviews if they feel strongly about a product whether it is good or bad.


