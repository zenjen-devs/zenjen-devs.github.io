[Back](https://zenjen-devs.github.io)

## Problem Statement: Classification of Accident Severity Using Historical NYC Crash Data

![NYC_CRASH_DATA_Banner](https://user-images.githubusercontent.com/84609216/188340988-20821f45-23d3-45b9-bdb2-b7f8b9c4a9cd.png)


Based on the historical data available with respect to NYC crash data, I developed a model to classify whether an accident is deemed severe/not severe. The model is a **binary classifier** in which target variable *serious_accident* is either *True/False* dependent on whether at least one (>1) injury was reported. 

The dataset contains approximately 1.2 million records, each representing a motor vehicle accident that occurred within the 5 boroughs of NYC between April 2012 and August 2022. This is the entirety of the crash data available as of August 2022, accessed directly from NYC OpenData and downloaded to a CSV dataset.

## Classification Summary & Model Performance 

Analysis of the model performance revealed that the *contributing factors* and *type of vehicles* invovled in the crash are the most important features with regard to predicting severity classification, respectively. This is consistent with orevious studies that conclude that point of impact and/or vehicle size are highly relevant factors in accident severities. Moreover, model performance results indicated that off-streets and hour of day in which an accident occurred also have relatively higher importance in predicting severity.

# Methodology

To handle imbalances in the dataset (such as overrepresentation of "fender-bender" type accidents), I employed a down-sampling technique which restored balance ahead of data pre-processing for training the model. While the dataset was mostly complete, missing data was handled through extrapolation of mean values. 



## Deep-Dive Data Mining: Analyzing Pre & Post-COVID Car Crash Data

This exploratory analysis further examined data for patterns and  points of interest pertaining to car accidents in the NYC boroughs. Results are useful for development of technology and to inform programs that can mitigate the ecnonic impacts and loss of life due to traffic accidents. This project was completed using mainly Python libraries and Tableau. <a href="pdfs/NYC_CrashData_EDA_2019-2022_JenArriaza.pdf" class="image fit"><b>View the full report here </b> <img style="vertical-align:middle" src="https://cdn-icons-png.flaticon.com/512/376/376007.png" height="12" width="12"/></a>

#### Insights

![image](https://user-images.githubusercontent.com/84609216/178160896-f2e439e0-2677-4d1b-96b6-56f35c1d574a.png)

A times series analysis of data from January 2019 to March 2022 shows that accident numbers fell to about half at the peak of quarantine. But what's more interesting is what numbers <b> did not fall</b>: <br>

![image](https://user-images.githubusercontent.com/84609216/178161094-70986a9c-9036-4115-a868-de93b4fb7321.png)

<i><b>Less accidents, but rising fatalities</b></i>. Although there are significantly less vehicles and overall accidents on NYC roads as expected post-COVID, pedestrian deaths continue on an upward trend as seen in the graph. This phenomena may be due to increased driver anxiety, larger vehicles, and changes in social norms as discussed in this [New York Times article](https://www.nytimes.com/2022/02/14/us/pedestrian-deaths-pandemic.html). <br>
  
Further exploration of the data revelead other interesing factors, i.e.; locations with high fatalities, and sedans vs. SUVs. <a href="pdfs/NYC_CrashData_EDA_2019-2022_JenArriaza.pdf" class="image fit"><b>For the full project report click here.</b></a>
  

  ![image](https://user-images.githubusercontent.com/84609216/178176439-7813c41a-73d6-4e58-87af-a06cea9cf8df.png)
  
<i>Next update</i>: Predictive modeling with real-world data to source serious accidents using automated machine learning (autoML).
