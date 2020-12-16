# A NLP binary classification project : Detecting dis-information
## Final Project at Ironhack Data Analytics Part Time Course

Paula Iglesias Barge
*Data Part Time Barcelona June 2020*


<img src="https://cdn.newsday.com/polopoly_fs/1.17995327.1523551866!/httpImage/image.png_gen/derivatives/display_960/image.png" alt="faketweet" width="1000" height="200" align="center"/>

## Project Description <a name="id1"></a>

This project aims to understand the carachteristics of Fake vs Real News and create an algorithm using different NLP techniques to achieve the highest accuracy and results when spotting dis-information. 

Since I started learning about machine learning, I was curious about NLP, how it worked, what was the workflow and how it was really working step to step. By selecting Fake News I was choosing a topic I was familiar too and was easy for me, as I have done studies about it in the past from a more journalistic side. 

<hr style="color: #7acaff;" width="50%" />
<a name="dataset"></a>

## Dataset<a name="id2"></a>

For the Dataset, I selected two different Datasets from Kaggle, aiming to merge both of them. Finally I decided to stick with one exclusive dataset with more cohesive data and accuracy, that already had +20.000 rows of news already classified. You can take a look at the original kaggle link <a href= https://cdn.newsday.com/polopoly_fs/1.17995327.1523551866!/httpImage/image.png_gen/derivatives/display_960/image.png>in here.</a>

* **train.csv**: A full training dataset with the following attributes:

<CODE> id </CODE>: unique id for a news article
<CODE> title </CODE>: the title of a news article
<CODE> author </CODE>: author of the news article
<CODE> text </CODE>: the text of the article; could be incomplete
<CODE> label </CODE>: a label that marks the article as potentially unreliable
<CODE> 1 </CODE>: unreliable
<CODE> 0 </CODE>: reliable

With this data I will be working on my first NLP project and tuning a kaggle dataset to understand how fake news are detected and if I can correctly train it to detect better and more unnacurate articles from wide known media.

## Contenido

**Índice**   
1. [Fake News : A little bit of context](#id1)
2. [Workflow](#id3)
  2.1 Análisis del proyecto
  2.2 EDA
  2.3 Topic Modeling
  2.4 Title Sentiment Analysis
  2.5 NLP : Preprocessing Data
  2.6 Modeling
3. [Conclussions and next steps](#id111)
4. [Bibliography](#id5)

<hr style="color: #7acaff;" width="50%" />

<a name="project"></a>
