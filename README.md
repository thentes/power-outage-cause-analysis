# Predicting the Causes of Power Outages


Created by Toma Hentes


thentes@umich.edu


## Introduction


Some power outages have obvious culprits - if your house is being pummelled by a massive thunderstorm and your power shuts down, you can infer the cause.
However, this is not the case for every power outage. Through details about a power outage, I aim to answer "what caused this power outage?"



The dataset I used for this analysis is Purdue University's 'Major Power Outage Risks in the U.S.' The data includes geographical, climatic, and economic data about power outages. 
The data encompassess 1,534 power outages that have occurred in the United States from January 2000 to July 2016.




CAUSE.CATEGORY, describing the cause of a given power outage, is the column I aim to predict. The dataset contains a constrained set of 7 broad causes - from severe weather to fuel supply emergencies.




## Data Cleaning and Exploratory Data Analysis


There wasn't a considerable amount of data cleaning required to complete my analysis. ADD MORE INFO


Later on, I'd ensure that categorical columns I used in my model, like CLIMATE.REGION, NERC.REGION, and CLIMATE.CATEGORY, were assigned to type 'category.'




<iframe
  src="assets/climate-region.html"
  width="20000"
  height="500"
  frameborder="0"
></iframe>


While sorting outage causes by U.S. state brings about far greater variation between states, grouping by climate region indicates trends by region. It appears that different climate regions have varying frequencies of power outages.



Severe weather is the most prominent cause in every region except the northwest in southwest, in which intentional attacks take over.



Some rarer causes also see more frequency in specific regions. Public appeal is by far the most frequent in the south, while the west expectedly experiences the most islanding.


This bar chart also provides an understanding of which regions experience the most and fewest outages. The northeast experienced over 100 more outages than any other region in this timespan, while west north central had by far the least.





<iframe
  src="assets/scatter.html"
  width="2000"
  height="1500"
  frameborder="0"
></iframe>




It appears that, not only is severe weather the most common cause of power outages, but that they have far greater numbers of customer affected and outage durations than other causes.


It also seems that, although far less frequent, fuel supply emergencies also cause relatively high outage durations, although there are far fewer customers affected.


To remove those extreme outliers on the x-axis—after identifying that severe weather and fuel supply emergencies have the longest durations—let’s see all other causes in more detail.


<iframe
  src="assets/condensed.html"
  width="2000"
  height="1500"
  frameborder="0"
></iframe>


It appears that system operability disruption, alongside severe weather, affects the most customers on average. While the majority of these instances still affect less than one million customers on average, it is the only cause other than severe weather that has affected over a million customers (and it has done so numerous times). This leaves intentional attacks, equipment failures, public appeals, and islanding as causes that affect the fewest customers affected.




Meanwhile, it seems like public appeals and intentional attacks are the only remaining causes that have cause durations longer than 3300, meaning that system operability disruptions, equipment failure, and islanding cause the shortest outages.




Overall, these two plots exemplify that power outage cause may be correlated to outage duration and customers affected.




With a better idea of which columns to use as parameters in my models, I imputed missing values. I'll only go over the columns that I used in my base and final model:


For the number of customers affected, I filled in missing values with the median. As shown by the charts above, there is extreme variance and some significant outliers in the number of customers affected. Since the mean would be affected by this variance, I decided to utilize the median instead. However, since there are so many factors at play when predicting the number of customers affected, I felt it didn't make sense to group by another column and then find the median.







## Framing a Prediction Problem


My prediction problem is to predict the cause of a given power outage. This is a classification problem, as power outage causes are categorical data. Since there are various power outage causes classified in the dataset, this is a multiclass classification. The response variable of this dataset is CAUSE.CATEGORY. This variable indicates a broad categorization of power outage categories. As such, predicting this variable is a dataset-specific equivalent to predicting the cause of any given power outage.






The dataset includes disproportional classes through much of its data, but especially in terms of power outage caues; a significant number of power outages in the dataset are caused by severe weather. For this reason, accuracy may not be the most adequate metric for this analysis. Furthermore, I feel that precision and recall are both important in this instance. Every power outage will be assigned a single cause. For these reasons, I have chosen the F1-score metric to assess my model.






My models are meant to be implemented before a power outage's cause would be known - presumably early after the outage begins. Demand loss would likely be calculated after a cause was determined, meaning I will not include it as a parameter in my models. The number of affected customers, however, is a more subjective case.






While there are many cases in which a cause would be known before how many customers are affected by it - especially in the case of severe weather. However, since power companies often release estimates for the number of affected customers within hours of an outage starting, it's reasonable to assume less obvious power outage causes may not be fully discovered by that point. Therefore, I will be including the number of customers affected as a parameter.




## Baseline Model




For a simple baseline model, I utilized the year and month of a given power outage as parameters.


The model returns a mean cross-variance of approximately 0.516. Essentially, by only using the month and year of the outage, the type of outage can be predicted a little over half of the time.

DOUBLE CHECK

This isn't terrible. It makes sense that the month of the outage could help identify the cause; in a month with a flurry of hurricanes, severe weather would be a reasonable prediction.



Clearly, this model has much room for improvement. There are many far more direct indicators of power outage causes, like the impact of the outage, the location of the outage, and the weather.


Since this model is so rudamentary, it chooses the most common cause - severe outages - most of the time. Since this cause is so frequent, the model likely does not perform as well as it seems.



## Final Model


I was initially inclined to utilize U.S. states themselves as a location parameter, as its far more specific. Howeve, some states - like Alaska or North Dakota - have very limited data. It would be less accurate to assume that 100% of Alaska's power outages are caused by ___ instead of ___ like in its climate region.



Combining those more "direct" indicators with the time of year of the outage 



Year really wasn't useful - both analyzed through df research as well as model implications, also conceptually



I initially considered climate category - either normal, cold, or warm - as a strong contender for a parameter. However, after analyzing the data, it seems that all of them have relatively similar likelihoods of climate causes.

COULD INCLUDE THE GRAPH HERE?




