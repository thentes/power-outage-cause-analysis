# Predicting the Causes of Power Outages


Created by Toma Hentes


thentes@umich.edu


## Introduction


The dataset I used for this analysis is Purdue University's 'Major Power Outage Risks in the U.S.' The data includes geographical, climatic, and economic data about power outages. The data encompassess 1,534 power outages that have occurred in the United States from January 2000 to July 2016.




Given details about a power outage, I am to answer the question "what caused this power outage"?


DESCRIBE RELEVANT COLUMNS




## Data Cleaning and Exploratory Data Analysis


There wasn't a considerable amount of data cleaning required to complete my analysis. ADD MORE INFO




<iframe
  src="assets/file-name.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>




It appears that, not only is severe weather the most common cause of power outages, but that they have far greater numbers of customer affected and outage durations than other causes.


It also seems that, although far less frequent, fuel supply emergencies also cause relatively high outage durations, although there are far fewer customers affected.


To remove those extreme outliers on the x-axis—after identifying that severe weather and fuel supply emergencies have the longest durations—let’s see all other causes in more detail.


It appears that system operability disruption, alongside severe weather, affects the most customers on average. While the majority of these instances still affect less than one million customers on average, it is the only cause other than severe weather that has affected over a million customers (and it has done so numerous times). This leaves intentional attacks, equipment failures, public appeals, and islanding as causes that affect the fewest customers affected.




Meanwhile, it seems like public appeals and intentional attacks are the only remaining causes that have cause durations longer than 3300, meaning that system operability disruptions, equipment failure, and islanding cause the shortest outages.




Overall, these two plots exemplify that power outage cause may be correlated to outage duration and customers affected.




INTERESTING AGGREGATES




There were a few values I needed to imputate.




## Framing a Prediction Problem


My prediction problem is to predict the cause of a given power outage. This is a classification problem, as power outage causes are categorical data. Since there are various power outage causes classified in the dataset, this is a multiclass classification. The response variable of this dataset is CAUSE.CATEGORY. This variable indicates a broad categorization of power outage categories. As such, predicting this variable is a dataset-specific equivalent to predicting the cause of any given power outage.


The dataset includes disproportional classes through much of its data, but especially in terms of power outage causes; a significant number of power outages in the dataset are caused by severe weather. For this reason, accuracy may not be the most adequate metric for this analysis. Furthermore, I feel that precision and recall are both important in this instance. Every power outage will be assigned a single cause. For these reasons, I have chosen the F1-score metric to assess my model, as it should act as a balanced metric that adjusts for uneven classes.




## Baseline Model




The two features implemented into my model - outage duration (OUTAGE.DURATION) and the number of customers affected (CUSTOMERS.AFFECTED) - are both quantitative.




The model returns a ______ .




While I think this model is a solid baseline, it can certainly be improved. HOW CAN IT BE IMPROVED.




## Final Model




