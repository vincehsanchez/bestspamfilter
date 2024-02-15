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

Next we needed to read the files and it was not as easy as we thought it was going to be becuase even though it was readable in a text file it was in a MIME format in which Zeb was super helpful in providing some starter code to get us going. 

From there we had some hurdles of reading some files because they needed to be decoded and if there were any emails that we could not decode it would skip over them and keep us moving.

next we needed to clean up the data like labeling them and making it radable for later.

label the data

## Preprocessing Data
- attempted bag of words, but Porter Stemming yielded more interesting results, we like interesting

### What can we see now?

**We asked ourselves what is "spammy"?**


![Top_20_Spam_Words](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/6f579cc0-ff3b-4f62-8580-c726555d642d)


**What is not spammy?**


![Top_20_Ham_Words](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/4e85f14a-270a-43ef-9027-17ae5825b90f)


**Vectorization**
- shuffled and split up between 75% and 25% (25% is reserved for after training)

  
![Screenshot 2024-02-14 at 6 41 50 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/ce700464-1f00-41aa-a556-651c5054b7cd)


- need to make our values readable for the model to do what we ask of it


![Screenshot 2024-02-14 at 6 42 34 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/2a4387ed-3910-407a-8848-b907910bc377)


- need to make our values to readable for the model to do what we ask of it

## Exploring Our Data


**Visualizing Our Data**
-dimensions make it difficult since values are not paired or tuples
- need to reduce, but in orde to do so we need to make dense and make data whole-ish?
- reduced to emails and their proximity to one aonther based on cosine similarity

## KNN Model

**Training Our Model**


![Screenshot 2024-02-14 at 6 48 34 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/9ae26430-4407-4e1c-961b-6c7b4ddb2b3c)


**Evaluating Our Model**


![Screenshot 2024-02-14 at 6 49 11 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/9a989c2a-a273-4a60-83dd-70d621299af7)


**Visualizing Our Data**

- jupyter notebook demo

**Looking into the KNN gears turning**

Here we use a decision boundary of the reduced dimensioned data of the KNN matrix:

shows us the boundary that separtes the different classes in the feature space.
paints a different picture of how the KNN model is functioning
incorporates or derived from the logistic function which predicts the relatinoship between input features and the probabililty of the positive class using a linear function
while keeping in mind..

KNN relies on the idea that similar data points are related and should be in the same class
similar to our EDA with cosine similarity visual, we can have a better understanding of how the KNN model relates between elements and classifies them
we would need to provide evidence, but the outliers could be an essential piece when the KNN model differentiates between emails.


![KNN_Decision_Boundary](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/2ed88660-35c5-4a15-a210-550f51f7027d)


## Analysis

The purpose of the analysis is to explore our data and identify what makes an efficient spam detector. Our goal is to achieve at least an 80% accuracy rate in filtering spam and indentifying spam trends to help improve educatinal efforts on spam recognition. We were able to exceed that goal, but there is still room for improvment. Possibly trying different preprocessing techniques or having the capacity to show multidimensional datasets that can offer more insight into how the data is grabbed.

## Summary

The KNN model shows to be the best machine learning model to achieve a accuracy rate above 80%. From our exploratory data analysis we were able 
to only scratch the surface of how KNN was able to classify from our dataset and interestingly give us insight into the extreme outliers of the datset 
which was a valuble tool in identifying what emails are spammy or not.

**Were we able to learn anything from this?**
Sort of, even though our machine learning model falls under classification, we came to realize that Natural language Processing adds dimensions (a lot) which requires more exploratory analysis because its a little difficult to justify how the data is classified and what/how is conceptualized as the starting point. We tried using cosine similarity to help see (possibly) where that starting point is at least.


## Considerations
For future developement, exploring or incorporating deep learning approaches for text classification could imporove performance.
Incorporating user feedback to update and/or evolve the model based on new spam trends could improve the effectiveness of classification.
