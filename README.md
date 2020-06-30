# Boston Media Sentiment Analysis

# Introduction

This repo is part of a BU Spark! project for the office of the mayor of Boston and its main goal is to identify the public's opinion about the mayor as well as the way he hanled a variety of his agenda topics. 

The repo contains a full pipeline from the collection of the datasets to the agenda definition and sentiment extraction. The datasets used here are collected by the _./Scraper_ from various Boston media outlets and in order to be able to distinguish between quality data and noise, without having to manually label hundreds of thousands of articles, I've implemented and incorporated in the preprocessing part a small Feed Forward Neural Network which manages to achieve an accuracy of 99.83% in the test set. Also, since I didn't have the exact topics of the mayor's agenda, I approximated them performing topic modeling with NMF. Finally, for the sentiment analysis I trained the Gluon NLP model. 


## Running the code

### Preparation

1. Run _pip3 install -r requirements.txt_ to download and install all the dependencies. 

2. Place all the datasets you obtained inside the _src/Datasets/Raw_ folder. 


### Running the Scraper

Scraping is always unpredictable; what ran perfectly yesterday may not work at all today... So, in order to save time and frustration I would advice contacting me first for the datasets. If you want to test the Scraper yourself though, you can run it like any other _Scrapy_ project. 


### Running the model

To run the preprocessing and sentiment analysis model just _cd_ to the _src_ folder and run the following commands: 

1. _python3 clean.py_ to remove missing values and align the different datetime formats. 

2. _python3 preprocess.py_ to align the documents' columns, merge the _tags_, _summary_ and _body_ columns and lowercase, tokenize, remove stopwords and lemmatize all the texts _(it may take some time...)_. 

3. _python3 doc2vec.py_ to create the doc2vec model and vectorize the articles _(it may take some time too...)_. 

4. _python3 relevance\_classifier.py_ to create the Feed Forward Neural Network for the articles' relevance-based classification. 

5. _python3 filter\_irrelevant.py_ to filter out all the irrelevant articles from the corpus. 

6. _python3 get\_agenda.py_ to obtain the mayor's agenda topics, using NMF, and map all the articles of the corpus to their respective agenda topic. 

7. _python3 sentiment\_analysis.py_ to train the Gluon NLP sentiment analysis model and perform predictions on the corpus. 



## That's it! 
Inside the _src/Datasets/Sentiment_ folder you have all the cleaned, filtered and classified files you need. The sentiment is given by the respective column as a raw number, so that you can set your on sentiment sets -e.g. Positive, Negative of Positive, Neutral, Negative- and thresholds. The agenda topic for each article is given from the respective column as an integer number. To map it to the set of descriptive words for its topic you can use the _src/Datasets/agenda.json_ file. 

