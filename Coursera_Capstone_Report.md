# Coursera Capstone Report

## Part 1 Introduction:

#### 1.1 Background:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;San Francisco is a huge city with a diverse and large population. It is home to many and provides numerous jobs and opportunities. Throughout San Francisco, there are many areas with high crime rates. These high crime rates can influence where people shop to where people live. Each year the crime rates in different areas change, resulting in a different environment. Looking at the rate and type of crime in a multitude of areas is really important in order to ensure your well-being. This information, derived from crime reports by the San Francisco Police Department, can tell you where are the safest places to travel or safest routes in the city. Obviously, this data can be very useful in order to keep safe. 

#### 1.2 Problem:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;There are two main problems that the data will solve. First, it will find which areas have the highest crime rate in certain months of a year and plot that on interactive maps. The data will also find the nearest venue, distance, and San Francisco crime to an address that the user chooses. Secondly, the data will also be used to find the top 3 types of crimes in each district and compare and group each district to each other based on the type of crime and frequency. I will use the KMeans model to solve this. Basically, problem one is to find where are most of the crimes in San Francisco located and the second problem is which are the most common types of crime in San Francisco. 

#### 1.3 Interest:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tourists and the police would be interested in the results of this project for many reasons. Firstly, Tourists can figure out where are the safest places to travel and the safest routes in San Francisco. Secondly, the police can figure out where to send their patrolling officers based on the type of crime and frequency of crime. This can make the San Francisco streets safer for everybody. Therefore, this project can contribute much-needed information to the general public.

## Part 2 Data Acquisition and Cleaning:

#### 2.1 Data Sources:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I will use Kaggle datasets and Foursquare location data in order to solve the problems. I will use the "San Francisco Crime Classification" dataset in Kaggle, and here is the link to it https://www.kaggle.com/kaggle/san-francisco-crime-classification. This has data about San Francisco crimes from 2003 to 2015. I will also use a multitude of libraries. The libraries I will use are Folium, Pandas, Numpy, Requests, Sklearn, Matplotlib, Geopy, and some data booting libraries. The data and libraries will help me perform the data analysis and result in some interesting conclusions. 

#### 2.2 Data Cleaning: 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I started off by downloading the test.csv data from the Kaggle data set. Since there are two questions that need to be solved, I copied the data set over to another data set. So, I have two data sets, sf_crime_1, representing the first question, and sf_crime_2, representing the second question.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The first problem I encounter is that the timestamp is in one column. I want the timestamp to be split into years, months, days, hours, and minutes in order to get the data in a specific interval. So, for both data sets, I normalize the timestamps using the pandas to_datetime method and then put each unit of time into columns. So I basically split the timestamps into 5 columns representing units of time. This occurs in both data sets. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To solve the first question, we need to use the frequency of the locations of the crimes. So, if there are crimes with the same location, I will keep them in order to produce an accurate model. Also, there is a bunch of useless information that has nothing to do with this question so in the feature selection section I will discard the useless information. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To solve the second question, we need to use the frequency of the category of crime. So, if there are redundant locations and category, I will keep them in order to produce an accurate model. Once again, there is a lot of data that has nothing to do with this question so in the feature selection section I will discard the useless information. 
