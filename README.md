# Spam Filter Machine Learning Project

## Overview

This project aims to develop a machine learning-based spam filter capable of outperforming spam detection of free email providers. 
By using our knowledge and techinques in machine learning we attempt to:
1. identify emerging patterns and trends in spam and phishing tactics
2. enhance our collective ability to recognize phishing content and provide a
   more thorough defense as phishing attacks become increasingly sophisticated.

We aim to make phishing detection more accesible and understandble to more vulnerable groups like the elderly and children.

## Data Collection

Getting the email dataset was simple and we downloaded a corpous from the SpamAssassin an open source spam filter that has also have a public corpus for anyone to use as reference that inlcudes folders that are designated as spam or not and are filled with emails of their respective folder type (spam or ham).
Next we needed to read the files and it was not as easy as we thought it was going to be becuase even though it was readable in a text file it was in a MIME format in which Zeb was super helpful in providing some starter code to get us going. From there we had some hurdles of reading some files because they needed to be decoded and if there were any emails that we could not decode it would skip over them and keep us moving.

next we needed to clean up the data like labeling them and making it radable for later.

label the data

## Preprocessing Data
- attempted bag of words, but Porter Stemming yielded more interesting results, we like interesting
- shuffled and split up between 75% and 25% (25% IS RESERVED FOR AFTER TRAINING)

**what do we see with our data right now?**
- top 20 words


**vectorized**
- need to make our values to readable for the model to do what we ask of it

## Exploring Our Data 


## KNN Model

**Training Our Model**

**Evaluating Our Model**

**Visualizing Our Data**

## Analysis

The purpose of the analysis is to explore our data and identify what makes an efficient spam detector. Our goal is to achieve at least an 80% accuracy rate in filtering spam and indentifying spam trends to help improve educatinal efforts on spam recognition.

## Summary

The KNN model shows to be the best machine learning model to achieve a accuracy rate above 80%. From our exploratory data analysis we were able 
to only scratch the surface of how KNN was able to classify from our dataset and interestingly give us insight into the extreme outliers of the datset 
which was a valuble tool in identifying what emails were not 


## Considerations
For future developement, exploring or incorporating deep learning approaches for text classification could imporove performance.
Incorporating user feedback to update and/or evolve the model based on new spam trends could improve the effectiveness of classification.
