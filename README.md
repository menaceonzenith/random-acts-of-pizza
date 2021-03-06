# Predicting Altruism Through Free Pizza with NLP and Classification - Metis Project 4
Rudy Wang

## Background

[R/random_acts_of_pizza](https://www.reddit.com/r/Random_Acts_Of_Pizza/)(RAOP) is a subreddit on Reddit.com that allows users to request free pizza from other users. The subreddit has strict rules and moderators/bots that keep track of each successful transaction that was successfully made on each post. 

But what makes some submissions receive free pizza? And what makes others not receive pizza? 

![Example of a RAOP Submission](example_post.png)

In the example post above, if a submission was successful in receiving a pizza, a flair would show up as "Fulfilled". If a submission was not successful in receiving a pizza, there would be no indication of a flair. 

## Mission

Using NLP, I wanted to explore the potential different topics that may emerge between receiving vs not receiving pizza submissions. Furthermore, I would like to include the topics we derived from the training dataset to be applied on the testing dataset to see if we would be successful in classifying submissions correctly.

## Process

1. Used [PushShiftData API](https://github.com/pushshift/api) to grab the Submission IDs, Request Title, and Request Text (Body) of submissions from January 1, 2014 - August 13, 2020. Extracted out 58,541 extra submissions. 
2. Using [PRAW API](https://praw.readthedocs.io/en/latest/), find the most updated flairs by searching with the Submission IDs extracted from PushShiftData API. Cleaned up the dataframe by removing deleted posts, and flairs that were not designated as either being empty or 'Fulfilled'. 
3. Combined the extracted dataset with the Kaggle dataset (used MongoDB to pull into Pandas DataFrame) and split into training and testing: training with 30,420 entries and testing with 8,227 entries. 
4. Pre-processed training dataset with [spaCy](https://spacy.io/usage/spacy-101) by removing stop words and lemmatization.
5. Applied [VADER Sentiment Analysis](https://github.com/cjhutto/vaderSentiment) to add as extra feature for classification.
6. Applied TF-IDF in combination with NMF to produce viable topics for different data splits: only received pizza, not received pizza, and a combined dataset. 
7. Using the topics I derived from NMF, I trained different classification models to see which model would produce the best accuracy score.
8. Applied the best model on the testing dataset and produced the accuracy score.

## Conclusion

![Training Dataset Topics](training_topics.png)

The top topics for the full training dataset were family, student, money and unemployment. 

![Received Pizza vs Not Received Pizza](received_vs_notreceived.png)

When we split received vs not received, an extra topic emerges in both. For received pizza submissions, requests that asked for favors such as birthdays, treats, or something for their loved ones come up as an extra topic. On the other side, requests that mentioned the user was homeless yielded less favorable results. 

As for my classification model, I went with the KNN model which yielded an accuracy of 0.91 for the testing dataset. 

All in all, most submissions do not get pizza - and the topics for both received and not received submissions are very similar: free lunch is possible, but difficult!

## Tools

- Jupyter Notebook
- Pandas
- PRAW API
- PushShiftData API
- Scikit-Learn
- spaCy
- MongoDB
- Matplotlib
- Seaborn
