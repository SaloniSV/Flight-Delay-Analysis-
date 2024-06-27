# Flight-Delay-Analysis

Introduction

Flight delays have become a very important subject for air transportation all over the
world because of the associated financial losses that the aviation industry is continuously
going through.
These delays not only cause inconvenience to the airlines, but also to passengers.
With the increased travel time comes and increase in expenses associated to food and
lodging, this results in added stress among passengers, but this doesn't account for the
growing distrust towards the airlines, who also suffer from extra costs such as those
associated to their crews, aircraft repositioning, increased fuel consumption while trying to
reduce their elapse time, and many others that tarnish the airlines reputation and often result
in the loss of demand by passengers.
The reasons for these delays vary a lot going from air congestion to weather
conditions, mechanical problems, difficulties while boarding passengers, and simply the
airline's inability to handle the demand given its capacity.
So what can be done as a passenger to avoid delayed flights? Is it possible to know if
your flight will be delayed before it comes up on the departure boards?
In this project, I have used PySpark to explore data and visualize insights to answer
some questions related to these flight delays. As a customer, we can stay informed about the
airline we choose, and its delay expectancy.

**Introduction**
Flight delays have become a very important subject for air transportation all over the
world because of the associated financial losses that the aviation industry is continuously
going through.
These delays not only cause inconvenience to the airlines, but also to passengers.
With the increased travel time comes and increase in expenses associated to food and
lodging, this results in added stress among passengers, but this doesn't account for the
growing distrust towards the airlines, who also suffer from extra costs such as those
associated to their crews, aircraft repositioning, increased fuel consumption while trying to
reduce their elapse time, and many others that tarnish the airlines reputation and often result
in the loss of demand by passengers.
The reasons for these delays vary a lot going from air congestion to weather
conditions, mechanical problems, difficulties while boarding passengers, and simply the
airline's inability to handle the demand given its capacity.
So what can be done as a passenger to avoid delayed flights? Is it possible to know if
your flight will be delayed before it comes up on the departure boards?
In this project, I have used PySpark to explore data and visualize insights to answer
some questions related to these flight delays. As a customer, we can stay informed about the
airline we choose, and its delay expectancy.


**Dataset Description:**
The dataset was located from Kaggle [1], this dataset was collected from U.S
department of transportation. The dataset tracks the performance of domestic flights within
the United States. This dataset has information about flights from 2018 to 2022, and it
contains information about the flight's Year, Month, Day, Day Of Week, Airline, Flight
Number , Tail Number, Origin Airport, Destination Airport, Scheduled Departure, Departure
Time, Departure Delay, Taxi Out, Wheels Off, Scheduled Time, Elapsed Time, Air Time,
Distance,Wheels On, Taxi In, Scheduled Arrival, Arrival Time, Arrival Delay, Diverted,
Cancelled, Cancellation Reason, Air System Delay, Security Delay, Airline Delay, Late
Aircraft Delay, Weather Delay.


**Data Collection:**
To start the project, I obtained accurate data from Kaggle. I used Parquet files which
facilitate faster retrieval of data. Here, we have accessed a total of 29,193,782 number of
rows for the years 2018 to 2022 to complete this project. These parquet files were uploaded
to an AWS S3 Bucket that was made publicly accessible. Next, I used the AWS S3 URL link
in Databricks to extract the data and perform analysis and transformation. This made it
possible for me to perform subsequent transformation and analysis on the data.


**Data Preparation:**
1. Dropping Duplicate Rows: The code starts by removing any duplicate rows from
the flights DataFrame to ensure that each observation is unique.
2. Removing Rows with Null Departure or Arrival Time: It filters out rows where
either the departure time (DepTime) or the arrival time (ArrTime) is null. This ensures that
only records with valid departure and arrival times are retained.
3. Cleaning Departure Delay Data: It removes rows where the departure time is
'2400', likely indicating a midnight departure time, which is treated as a null value. It converts
the DepTime and CRSDepTime columns to StringType since they were cast to String. It
creates new columns DepTimeDateTime and CRSDepTimeDateTime, parsing the time
5
strings into actual timestamps using the to_timestamp function. It calculates the departure
delay (DepDelay) in minutes by subtracting the scheduled departure time from the actual
departure time and converting the result from seconds to minutes. It creates a new column
DepDelayMinutes, which captures the positive departure delay values, setting negative delays
to zero. It drops the temporary timestamp columns DepTimeDateTime and
CRSDepTimeDateTime as they are no longer needed.
4. Cleaning Arrival Delay Data: Similar to the departure delay data cleaning
process, it removes rows with arrival time '2400', converts relevant columns to StringType,
creates timestamp columns for arrival time and scheduled arrival time, calculates arrival
delays, creates a new column capturing positive arrival delays, and drops the temporary
timestamp columns.
5. Removing Null Values from Taxi In/Taxi Out Columns: It filters out rows
where either the TaxiIn or TaxiOut columns are null, ensuring that only records with valid
taxi in and taxi out times are retained.
6. Showing DataFrame Schema: Finally, it prints the schema of the flights
DataFrame to provide an overview of its structure after the data cleaning operations.
These steps collectively ensure that the flights DataFrame is cleaned and prepared for
further analysis, with invalid or missing data removed and relevant columns properly
formatted. Once the data was collected, the next step was to prepare it for analysis.


**Data Analysis:**
 I used Pyspark to analyze all our data frames. The data analysis involved using
various statistical techniques to gain insights. The analysis was carried out using Python
6
libraries such as Pandas, NumPy, Seaborn and Matplotlib. The analysis included calculating
descriptive statistics, identifying trends, and determining correlations between variables.
Some steps taken to analyze the data:
• I grouped the data year, and calculated the total flights operated by year from 2018-
2022.
• I grouped the data by Airline and ranked the top 20 by delayed flights and visualized
it using Seaborn.
• Since we have established that Southwest airlines has the maximum delayed flights
in our dataset, we calculated the chance of having a flight delay if a passenger is
choosing to travel by Southwest airlines.
• I grouped the data to show the delay by each month and count the number of flight
delays by the month.
• I aggregated and filtered the data to get a distribution of delay times upto 3 hours.
• I grouped the delay times into 6 categories depending on the delay time experienced
On Time Early – Departure Delay of 0 mins
Small Delay – Departure delay of 15 mins or less
Medium Delay – Departure delay of 15 mins – 45 mins
Large Delay – Departure delay of 45 mins and more
Cancelled – If the flight gets cancelled
Diverted – If the flight status is diverted
• I calculated the percentage of flights which get delayed in our entire dataset.
7
• I aggregate the delay groups by year and check the delay groups by year to
understand how the delay time has fared over the years.
• I also aggregated the delay time by months and check which month has the highest
delay times.
After completing the data analysis, the next step was to visualize the data. I created
several visualizations using the Matplotlib libraries and Seaborn libraries.
One challenge I encountered during this phase was deciding which visualizations to
create. With so much data, it was difficult to know which visualizations would be most
informative. I overcame this challenge by reviewing the data analysis results and selecting the
visualizations that best represented the insights gained.


**Visualization:**
The different visualizations are provided below with an explanation for each of them –
1. Total Delayed flights by Year
This analysis provides valuable insights into the total flights that were delayed and
operated by year. I have analyzed our data for the year’s 2018-2022. Here, we have used
Matplotlib libraries to plot the graph and label each year by the total number of delayed
flights. As seen in the visualization, 2019 is the highest number of delayed flights while 2020
has a sharp decline which could be because of the COVID-19 pandemic.
8
2. Distribution of Delayed flights by Airline
This visualization provides a comparison of delays by Airlines. Since we have ample
number of airlines in our dataset, we have limited the visualization to just the top 20 for a
clean approach. The airline with the most delays is Southwest Airlines are seen in the graph,
followed by Delta Airlines, SkyWest Airlines, American Airlines and United Airlines.
9
3. Distribution of Delayed Flights upto 3H
This visualization provides insights about the delay times of upto 3 hours with a bin
size of 9 minutes. As seen in the viz. the most delayed are reported to be 27 minutes or less
and there is a gradual decline. It is a right-skewed data and an unimodal graph with a
prominent peak at 9 minutes.
4. Flights delayed by Month
 This visualization provides a comparison of the total flights delayed grouped by each
month over the past couple of years. As seen in the viz. it can be iterated that July month has
the highest number of delays and this can be attributed to weather-related delays caused
during the summer months.
10
5. Delay Group Clustering
This visualization shows the clustering of flights by Delay Groups- OnTime_Early if
the flights have not experienced any delay. Small Delay, if there was a 15-minute or lesser
delay, Medium Delay, if the flights were delayed over 15mins and under 45mins. For any
delays, over 45mins, it is classified as a Large Delay. We have attempted to plot any diverted
planes, however, there isn’t any significant information on diverted planes in our dataset.
11
6. Heatmap by Year
This visualization is a heatmap of the percentage of delayed flights by year.
7. Heatmap by Month
This visualization is a heatmap of the percentage of delayed flights by month.


**Conclusion:**
 The following are the conclusions derived -
• The year 2020 had the least flight delays and this is most likely due to the global
pandemic that started during that year and influenced the traveling.
• Southwest Airlines faced most delays out of the top companies while Republic
Airlines faced the least.
12
• There is a 38% chance that the flight will be delayed if traveling on a Southwest
flight.
• 25% of flights from 2018-2022 have been delayed according to our dataset.
• 65% of delays are between 0-30mins.
• It is more likely to have a delay during the summer months(June, and July). July
also has the most total flights so there probably is a correlation.
• It is less likely to have a delay during September
• Starting from March 2020 the number of daily delays considerably dropped and kept
a low trend until Apr-May 2021. This period coincides with the lock down and travel
restrictions period. Fewer flights probably were correlated to higher capability of
handling flights on time.
Reflections:
 This project was a great learning experience. I was able to learn how to store, collect,
clean and visualize millions of rows of data. This project have a valuable experience working
with PySpark and leveraging technologies such as AWS S3, Spark, Databricks. Since, I had
taken up the challenge to complete this project solo, there were multiple challenges including
difficulty in getting the code right, mining useful data from the dataset, and performing
visualizations. However, this did not stop me from completing this project.
13
Future Scope:
 The future scope of this project is to use machine learning models like Logistic
Regression, Decision Tree Classifier, Random Forest Regression and Linear Regression and
its variant Boosted Linear Regression to predict the departure delay of flights. If given the
right set of input parameters, even simple algorithms can predict the delays with high
accuracy. Although good results were obtained, there is a huge scope for future work. If
weather and air traffic control information is made available we can then go on to predict
arrival delay even without the inclusion of departure delay as an attribute. Also, we can
progress into predicting if a flight will be delayed or cancelled based on weather factors like
snow, rain, storms and so on.
References
1. https://www.kaggle.com/datasets/robikscube/flight-delay-dataset-20182022
2. https://docs.databricks.com/
3. https://docs.aws.amazon.com/index.html
4. https://community.cloud.databricks.com/?o=1327577811019730#notebook/39365843
76938536/command/2004104969533133

The dataset was located from Kaggle [1], this dataset was collected from U.S
department of transportation. The dataset tracks the performance of domestic flights within
the United States. This dataset has information about flights from 2018 to 2022, and it
contains information about the flight's Year, Month, Day, Day Of Week, Airline, Flight
Number , Tail Number, Origin Airport, Destination Airport, Scheduled Departure, Departure
Time, Departure Delay, Taxi Out, Wheels Off, Scheduled Time, Elapsed Time, Air Time,
Distance,Wheels On, Taxi In, Scheduled Arrival, Arrival Time, Arrival Delay, Diverted,
Cancelled, Cancellation Reason, Air System Delay, Security Delay, Airline Delay, Late
Aircraft Delay, Weather Delay.


**Data Collection:**

To start the project, I obtained accurate data from Kaggle. I used Parquet files which
facilitate faster retrieval of data. Here, we have accessed a total of 29,193,782 number of
rows for the years 2018 to 2022 to complete this project. These parquet files were uploaded
to an AWS S3 Bucket that was made publicly accessible. Next, I used the AWS S3 URL link
in Databricks to extract the data and perform analysis and transformation. This made it
possible for me to perform subsequent transformation and analysis on the data.

**Future Scope:**
 The future scope of this project is to use machine learning models like Logistic
Regression, Decision Tree Classifier, Random Forest Regression and Linear Regression and
its variant Boosted Linear Regression to predict the departure delay of flights. If given the
right set of input parameters, even simple algorithms can predict the delays with high
accuracy. Although good results were obtained, there is a huge scope for future work. If
weather and air traffic control information is made available we can then go on to predict
arrival delay even without the inclusion of departure delay as an attribute. Also, we can
progress into predicting if a flight will be delayed or cancelled based on weather factors like
snow, rain, storms and so on.
References
1. https://www.kaggle.com/datasets/robikscube/flight-delay-dataset-20182022
2. https://docs.databricks.com/
3. https://docs.aws.amazon.com/index.html
4. https://community.cloud.databricks.com/?o=1327577811019730#notebook/39365843
76938536/command/2004104969533133
