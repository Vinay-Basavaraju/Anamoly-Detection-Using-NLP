# Anomaly Detection Using NLP

This project is about detecting anomalies in web and application server logs of an ecommerce application using machine learning model. This is achieved using NLP techniques. 

## How does it benefit

By detecting unusual patterns in the web and application server logs, we can alert the system admin about a problem which is about to happen, in advance. This helps the support team to take corrective action before any major damage is done to the system. 

Issues like system hack, server going down due to full capacity usage etc can be identified and notified in advance to the support team who can further take corrective action. 

After the model is trained initially , the model will continue to learn with new log data always. Hence any change in application log pattern is taken care automatically without requiring the model to be changed and re deployed. 

## Solution Approach

Data objects with behaviors that are very different from expectation are anomalies and the process of finding them is called anomaly Detection. 

Natural language processing (NLP) techniques can be used to detect unusual log data and flag it as an anomaly. 

The Word2Vec model from Google can be used to learn the word embedding from the log data. Once the model is trained , it would have learnt the word embedding of all the log data. Any new log data having unusual pattern can be detected by using one of the distance metrics, the Cosine Similarity, to find the distance between new words encountered, comparing it with the most similarly occurred words in the already learnt log data. 

If the Cosine similarity between the new log data and the most similar log data is below a pre defined value like less than 0.6, then it can be flagged as an anomaly and the support team will be notified. 

This is an unsupervised model. It can be improved further by taking user feedback. When the email is sent to the support team with details on the anomaly detected, the support team can further review and flag it as an anomaly or not an anomaly. This feedback will be used as an label, making the model semi supervised. 


## Pre Processing

Depending on how the data is logged, certain data in the log file can be removed which does not add much value in detecting an anomaly like time stamp in each row of log data.

Each line of log data in the log file will be considered as one sentence and will be tokenised before feeding to the model. 


## How it works

In word embedding model, the words are positioned in the vector space , closer to other words depending on what words surround the word when it is used. So the Cosine similarity of words which occur in normal log data will be higher when compared to the words occurring in the abnormal log data. 

If we consider one line of log data, all the words occurring in this line is learnt with respect to the other words surrounding each word in a line of log data. 

For example, in case of a system hack, let's assume the URL request is received by the web server and the URL received has an unusual URI when compared to the URI served by the application. In this case the cosine similarity of the new log data will be very less compared to all the other log data in the vector space and hence can be flagged as an anomaly. 


## Model Training

Word2Vec model is neural network based model and requires huge amount of data to be trained. This is not a problem for this use case since huge amount of log data is generated every minute. All the log data including the archived log data since years can be used to train the model.


## Statistics Report

Monthly statistics report on new log data found every month, anomalies found, false positives can be sent to the support team. 