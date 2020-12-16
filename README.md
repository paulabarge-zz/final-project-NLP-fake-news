# A NLP binary classification project : Detecting dis-information
## Final Project at Ironhack Data Analytics Part Time Course

Paula Iglesias Barge
*Data Part Time Barcelona June 2020*


<img src="https://cdn.newsday.com/polopoly_fs/1.17995327.1523551866!/httpImage/image.png_gen/derivatives/display_960/image.png" alt="faketweet" width="100%" height="" align="center"/>

## Project Description <a name="id1"></a>

This project aims to understand the carachteristics of Fake vs Real News and create an algorithm using different NLP techniques to achieve the highest accuracy and results when spotting dis-information. 

Since I started learning about machine learning, I was curious about NLP, how it worked, what was the workflow and how it was really working step to step. By selecting Fake News I was choosing a topic I was familiar too and was easy for me, as I have done studies about it in the past from a more journalistic side. 

<hr style="color: #7acaff;" width="50%" />
<a name="dataset"></a>

## Dataset<a name="id2"></a>

For the Dataset, I selected two different Datasets from Kaggle, aiming to merge both of them. Finally I decided to stick with one exclusive dataset with more cohesive data and accuracy, that already had +20.000 rows of news already classified. You can take a look at the original kaggle link <a href= https://cdn.newsday.com/polopoly_fs/1.17995327.1523551866!/httpImage/image.png_gen/derivatives/display_960/image.png>in here.</a>

* **train.csv**: A full training dataset with the following attributes:

<CODE> id </CODE>: unique id for a news article <br>
<CODE> title </CODE>: the title of a news article <br> 
<CODE> author </CODE>: author of the news article <br> 
<CODE> text </CODE>: the text of the article; could be incomplete <br> 
<CODE> label </CODE>: a label that marks the article as potentially unreliable <br>
<CODE> 1 </CODE>: unreliable <br>
<CODE> 0 </CODE>: reliable <br>

With this data I will be working on my first NLP project and tuning a kaggle dataset to understand how fake news are detected and if I can correctly train it to detect better and more unnacurate articles from wide known media.

## Contenido

**Índice**   
1. [Fake News : A little bit of context](#id1)
2. [Workflow](#id3)<br>
  2.1 [EDA] (#id4) <br>
  2.2 [NLP : Preprocessing Data] (#id5) <br>
  2.3 [Modeling] (#id6) <br>
3. [Conclussions and next steps](#id7)
4. [Bibliography](#id8)

<hr style="color: #7acaff;" width="50%" />

<a name="project"></a>

<a name="workflow"></a>

## Fake News : A little bit of context <a name="id1"></a>

Before we go deep in the Dataset and the NLP problem, I want to give you a little bit of context.<br>

Fake News aren't simple. According to <a href= https://firstdraftnews.org/latest/fake-news-complicated/>FirsDraftNews.org </a>, there are 7 different types of Fake News. In this project, we are mostly going to tackle satire or parody, since we will be working on detecting sentiment in the titles of the news, 
and when classificating the news in fake or not, we will be looking at unnacurate content or misleading information. 

On the other side, besides what a machine tell us about a specific information, there are also some trust indicators, that helps us detect unnacurate information or fake news in general. I choose to follow the Trust Project indicators of truth for my exploration of the dataset, but there are plenty of them around. If you are curious, <a href = https://secureservercdn.net/72.167.242.48/n36.08b.myftpupload.com/wp-content/uploads/2020/07/7.29.20The-Trust-Indicators-Handout.pdf>here you can find their manifesto.</a>

Last but not least, my data is mainly focused on news and articles from the United States, so I am aare that my classification application will likely only work with such type of news. 

Now that you know a little bit more about my approach, let's dive in! 

## EDA <a name="id3"></a>

I follow a certain pattern of question when doing the Data Exploration. My initial hypothesis was that Fake News are articles who lack of authors, source, and have some sentiment attached to them, being hate, sensationalism or excessive use of adjectives. Therefore, when taking a look at my Dataset, I follow a certain pattern to differentiate both types of news. 

My train dataset was from the beginnning completely balanced. 

1. Do Fake News have authors?

I found out that more than almost 2000 rows had no Author at all, belonging more than 1750 rows to Fake News and less than 100 to Real News. Therefore, Anonymous authors was an important feature to take into account. 

2. What about the source?

By looking into the columns I had, I was able to scrape more than 500 different sources, but not enough to make a significant difference between fake and real news. 

2. What topics are they talking about?

I built and LDA model using the pyLDAvis library to find cluster in my articles that could help me identify the news and their subject. With a 50% level of coherence, my model was able to find 35 different clusters, being the most important ones the following:
- Political global news.
- Regular news involving people and cities
- US election
- Wikileaks and Hillary scandal
- Syria and Afghanistan

However, these topics were equally distributed between fake and real news, and there were no significant differences to take into account that there were some topics including predominantly fake or real news. 

I went ahead and decided to perfom a word cloud of the most used words in our articles, and the most used words in real vs fake news. ALthough somewhat similar, I did found some clear diferent patterns.

3. Do fake news have a sentiment attached in their title? Do fake news tend to yellow press journalism?

To discover if fake news were indeed attached to some type of sentiment, I used the VADER sentiment analysis. VADER is a model used for text sentiment analysis that is sensitive to both polarity (positive/negative) and intensity (strength) of emotion. However, the results were contrary to my initial thoughts and actually, not a lot of my news had a sentiment attached to it, and real news had slightly a little bit more of sentiment than fake news, actually. 

Other considerations I took into account were the lenght of the news depending on its accuracy, duplicates, and date. 

## NLP : Preprocessing Data <a name="id4"></a>

But, how does my algorithm take all these features and text into account? How is going to interpretate my data? 

First of all, although we had already preprocessed our data to perform the Topic Modeling analysis with pyLDAvis using the nltk library, let me explaing a little but the workflow of NLP. 


We start with a text file, that independently from the steps and libraries and mechanisms we choose to use, performs a language detection and after that, gets each sentence and word and tokenizes it, lowercase and clean according to the rules we choose and if we think is important, stemmatizes it, which basically, turns the word into its root forms. 

After that, the words get converted into numbers, being these numbers the weight of each word in its sentence, if you use the TFIDF matrix, or gets converted into a multidimensional vector where Deep Learning mechanisms such as Word2Vec or FastText, assign each word a position, and therefore and importance and relationship between the words depending on how they form sentences. 

I chose to approach my data on two different ways: 
- With the Classical NLP approach; where I performed most of the steps individually, first detecting the language of my artciles using CLDR3, a neural network model for language identification, and used NLTK and SPACY as two different libraries to preprocess my text, tokenize, clean and stemmatize my words, among other rules you can observe in my cleaning function at the Preprocessing Data notebook. 

After that, I converted each sentence and word into a number by using the TFIDF matrix, where each word gets assigned a certain weigth. After that, I had two different approached on how to process my text columns and pass them along to my chosen models. 

- Using Deep Learning Algorithms; since Deep Learning was completely new for me, I chose to give it a try. I started with Word2Vec, a neural network model used to learn word association from large junks of text. This models turns each word into a vector, chosen carefully by the cosine similarity mathematical function, which basically indicates the semantic similarity between each word. Word2Vec was created by google. 

<img src= =https://miro.medium.com/max/3496/1*jpnKO5X0Ii8PVdQYFO2z1Q.png alt="fasttextword2vec" width="100%" height="" align="center"/>

After starting with Word2Vec, I discovered FastText, which is basically an extension of Word2Vec created by Facebook and doesn't use gensim. The main difference is that it treats each word as composed of character n-grams. So the vector for a word is made of the sum of this character n-grams. 

I sticked with FastText to try one of the two models and preprocessed my text columns with it to prepare it for the modeling part. 

To give some more clarity, this is what my dataset looked in the beginning, and how it looked before I started training models. 


## Modeling <a name="id4"></a>

Once I had my data converted to numbers, I chose four different models to train my dataset. Logistic Regression, Supper Vector Machine, Naive Bayes and Random Forest. 

I feed all of them my dataset in different versions: just the text columns converted to numbers with the target and my dataset with the author and topic modeling features. It turns out, my best results were using Logistic Regression and SVC with just the text features, no other features such as author or topic added. 

In the end I accomplished to create and application that: 
- Has a 97% of accuracy when predicting fake or real news. 
- Only misses 3% of the fake news
- Only misses 2% of the real news. 

## Next Steps and Room for improvement <a name="id4"></a>

Although I am beyond proud of understanding and applying everything I have learned about Data and moreover, NLP, in the last three weeks, since Deep Learning and NLP was not a known topic for me, I realized I spent a lot of time trying to understand and apply the preprocessing part and not as much as I would have liked trying different approached and trying to train my data with a Neural Model such as BERT. 

I have tested my application with the given data but I would like to try it our with other news and fine tune my model to actually build a classification algorithm that it's accurate and approachable to every US based new. 

I will keep working and learning more about NLP for sure, I can't wait to make it better!


## Bibliography <a name="id4"></a>
- The Different Types of Mis and Disinformation - First Draft News:
<a href= https://firstdraftnews.org/latest/fake-news-complicated/>https://firstdraftnews.org/latest/fake-news-complicated/</a>
- Michigan State University - Research Guides : 
<a href=https://guides.lib.umich.edu/c.php?g=283063&p=4471741>https://guides.lib.umich.edu/c.php?g=283063&p=4471741</a>
- Getting Real with Fake News - Ria Ghandi:
<a href=https://radiant-brushlands-42789.herokuapp.com/towardsdatascience.com/getting-real-with-fake-news-d4bc033eb38a>https://radiant-brushlands-42789.herokuapp.com/towardsdatascience.com/getting-real-with-fake-news-d4bc033eb38a</a>
- Spacy - English models : 
<a href=https://spacy.io/models/en#en_core_web_md> https://spacy.io/models/en#en_core_web_md</a>
- Gensim - Topic Modeling:
<a href= https://www.machinelearningplus.com/nlp/topic-modeling-gensim-python/> https://www.machinelearningplus.com/nlp/topic-modeling-gensim-python/</a>
- Using Word2Vec to analyze news headlines and predict article success:
<a href=https://towardsdatascience.com/using-word2vec-to-analyze-news-headlines-and-predict-article-success-cdeda5f14751>https://towardsdatascience.com/using-word2vec-to-analyze-news-headlines-and-predict-article-success-cdeda5f14751</a>
