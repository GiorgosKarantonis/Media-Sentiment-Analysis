# CS-506-Mainstream-Media-Sentiment-Analysis

This repo is part of the Media Sentiment Analysis Project for BU's CS506 class. The code provided here refers addresses the collection and manipulation of data from various mainstream journals. 


## A couple of disclaimers...

1. This file simply provides the steps required to run the mainstream media model and it's not the documentation of our project. If you want to find out more about our approach, our experiments and our results please check our _\_Report.pdf_ file. 

2. No datasets are have been uploaded to this repo, but if you would like to test our model, without having to run our Scraper first, feel free to contact me. 


## Running the code

### Preparation

1. Clone or download the repo and _cd_ to its local directory. 

2. Run _pip3 install -r requirements.txt_ to download all the dependancies. 

3. In the _src_ folder create a folder named _Datasets_. 

4. Inside the _Datasets_ folder create another one named _Raw_. 

5. Place all the datasets you obtained, either by running the Scraper yourself or by contacting me, inside the _Raw_ folder. 


### Scraper

Scraping is always unpredictable; what ran perfectly yesterday may not work at all today... So, in order to save time and frustration, I would advice contacting me for the datasets. If on the other hand you want to test the Scraper yourself, you can execute it like any other _Scrapy_ project. 


### Running the model

To run the preprocessing and sentiment analysis model just _cd_ to the _src_ folder and run the following commands: 

1. _python3 clean.py_ to remove missing values and align the different datetime formats. 

2. _python3 preprocess.py_ to align the documents' columns, merge the _tags_, _summary_ and _body_ columns and lowercase, tokenize, remove stopwords and lemmatize all the texts _(it may take some time...)_. 

3. _python3 doc2vec.py_ to create the doc2vec model and vectorize the articles _(it may take some time too...)_. 

4. _python3 relevance\_classifier.py_ to create the Feed Forward Neural Network for the articles' relevance-based classification. 

5. _python3 filter\_irrelevant.py_ to filter out all the irrelevant articles from the corpus. 

6. _python3 get\_agenda.py_ to obtain the mayor's agenda topics, using NMF, and map all the articles of the corpus to their respective agenda topic. 

7. _python3 sentiment\_analysis.py_ to train the Gluon NLP sentiment analysis model and perform sentiment predictions on the corpus. 



## That's it! 
Inside the _src/Datasets/Sentiment_ folder you have all the cleaned, filtered and classified files you need. The sentiment is given by the respective column as a raw number, so that you can set your on sentiment sets -e.g. Positive, Negative of Positive, Neutral, Negative- and thresholds. The agenda topic for each article is given from the respective column as an integer number. To map it to the set of descriptive words for its topic you can use the _src/Datasets/agenda.json_ file. 

