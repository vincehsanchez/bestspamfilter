# Spam Filter Machine Learning Project

## Overview

This project aims to develop a machine learning-based spam filter capable of outperforming spam detection of free email providers. 
By using our knowledge and techinques in machine learning we attempt to:
1. identify emerging patterns and trends in spam and phishing tactics
2. enhance our collective ability to recognize phishing content and provide a
   more thorough defense as phishing attacks become increasingly sophisticated.

We aim to make phishing detection more accesible and understandble to more vulnerable groups like the elderly and children.

## Data Collection

Getting the email dataset was simple and we downloaded a corpous from SpamAssassin an open source project that serves as a mail filter to identify Spam.

They offer a public corpus of selected mail messages, suitable for use in testing spam filtering systems.


![Screenshot 2024-02-14 at 7 15 30 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/6d1ecc25-b6e1-4c75-8bfe-397b2b306c2a)


**Hurdles**


Next we needed to read the files and it was not as easy as we thought, this was due to the format of the files becasue even though it was readable in a textedit....the file was in a MIME format in which Zeb was super helpful in providing some starter code to get us going. 



From there we had a seemingly endless hurdle of reading some files because they needed to be decoded and if there were any emails that we could not decode it would skip over them and keep us moving.

![Screenshot 2024-02-14 at 7 13 45 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/715e955c-de5a-4cd4-bb19-8e18359916f6)

next we needed to clean up the data like labeling them and making it radable for later.

- labeling the data as spam or ham

  - "spam" for, well spam
  - "ham" for regular emails

## Preprocessing Data
- needed to tokenize the data, basically find trends or combination os letters, words, phrases, etc. that have some meaning and helpful with tagging or indentifying patterns.
  
- attempted bag of words, but Porter Stemmer yielded more interesting results, we like interesting ;)

Dataset preprocessed with Bag of Words


![Screenshot 2024-02-14 at 7 17 33 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/3235708c-fcbe-4617-9396-400c76c2ef50)



Dataset Preprocessed with Porter Stemmer


![Screenshot 2024-02-14 at 7 16 55 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/a11493ee-2a3e-4517-9793-fb71bb1bc249)



### What can we see now?
Once we picked which nlp 
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


### Visualizing Our Data
- dimensions make it difficult since values are not paired or tuples
- looked to incorporating the use of cosine similarity that produces a value of measure that is between two elements ans useful with NLP analysis.

**We first tried using a heatmap with the cosine similarity matrix that we produced**


![cosine_similarity_heatmap](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/ea0289af-f220-4091-9f32-db98c5dc1cdc)


**Was the heatmap useful?**

No, becuase of how many different emails there are it adds too many dimensions for us to clearly see anything of use here and how our machine learning model will be able to classify anything.


**So what do we do from here?**

We can reduce the number of dimensions to get a better picture that can shows us two things:
1. each point is an email
2. their viscinity to one another gives us perspective of email similarity
         - the closer they are, the more similar they are

- need to reduce, but in order to do so we need to make it dense first and make data "whole" to plot it.
- reduced to emails and their proximity to one another based on cosine similarity

![PCA_of_Email_Vectors](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/e9e11a06-e10e-4b28-a8c8-614ab33093d8)


**What do we see?**
- we can see our extreme outliers, 209, maybe we can see whether why some spam or ham are more likely to be outliers.


**This helped us ask:**
- Why is it shaped like that?
- What are these clusters/dense areas?
- What do these points mean?

**Can we explain the outliers?**

- We tried getting top 20 words and see if anything is different between what is definitely spam or ham versus what is just making the cut:


![Top_20_Ham_Words_from_Email_Outliers](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/393fd5a4-7d2d-48aa-8bc6-09b1358bb523)


![Top_20_Spam_Words_from_Email_Outliers](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/ad9ede6f-cf8f-4e98-a266-b93bd13bcc44)


- ... yeah nothing to intersting here, but maybe if we increased dimensions we could get a picture.


## KNN Model

**Training Our Model**


![Screenshot 2024-02-14 at 6 48 34 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/9ae26430-4407-4e1c-961b-6c7b4ddb2b3c)


**So what?**

- Its doing pretty good!
  
1. Precision:
- For ham (0), the precision is 0.97, meaning that when the model predicts an email as ham, it is correct 97% of the time.
- For spam (1), the precision is 1.00, indicating that every email predicted as spam was actually spam.
- So no ham emails mistakenly classified as spam. YAY!

2. Recall:
- For ham (0), the recall is 1.00, this is what we want, no ham emails are misclassified as spam.
- For spam (1), the recall is 0.94, only 6% of spam emails were missed by the model and possibly classified as ham.

3. F1-Score:
- The F1-score for ham (0) is 0.98, optimal performance between precision and recall in identifying ham emails.
- The F1-score for spam (1) is 0.97, although lower, high performance between precision and recall (keeping in mind spam recall of 0.94).

5. Support:
- The support for ham (0) is 730, actual number of ham emails in the test dataset.
- The support for spam (1) is 358, actual number of spam emails in the test dataset.

6. Accuracy:
- The overall accuracy of the model is 0.98, meaning that 98% of the emails were correctly classified and its effective!

7. Macro Avg:
- The macro average for precision, recall, and F1-score are all 0.98, pretty impressive performance that it was able to perform in a balanced manner even though the data was not balanced.

8. Weighted Avg:
- The weighted average for precision, recall, and F1-score is also 0.98, even with how many ham and spam emails there were, it still performs well


**Takaways:**
- This classification report shows that the KNN model is effective for this spam detection task, with very few errors in classification.
- There could be room for some improvement in spam recall to catch more spam emails without sacrificing the precision.


**Evaluating Our Model**


![Screenshot 2024-02-14 at 6 49 11 PM](https://github.com/vincehsanchez/bestspamfilter/assets/141890646/9a989c2a-a273-4a60-83dd-70d621299af7)

**Still pretty good!**



### Visualizing Our Model

- jupyter notebook demo

**Looking into the KNN gears turning**

Here we use a decision boundary of the reduced dimensioned data of the KNN matrix:

shows us the boundary that separates the different classes in the feature space.
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
