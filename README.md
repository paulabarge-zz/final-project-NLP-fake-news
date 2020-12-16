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


