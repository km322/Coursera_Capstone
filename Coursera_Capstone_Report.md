# Coursera Capstone Report: San Francisco Crime 
### By: Ketan M, July 23, 2021

## Part 1 Introduction:

#### 1.1 Background:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;San Francisco is a huge city with a diverse and large population. It is home to many and provides numerous jobs and opportunities. Throughout San Francisco, there are many areas with high crime rates. These high crime rates can influence where people shop to where people live. Each year the crime rates in different areas change, resulting in a different environment. Looking at the rate and type of crime in a multitude of areas is really important in order to ensure your well-being. This information, derived from crime reports by the San Francisco Police Department, can tell you where are the safest places to travel or safest routes in the city. Obviously, this data can be very useful in order to keep the city safe. 

#### 1.2 Problem:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;There are two main problems that the data will solve. First, it will find which areas have the highest crime rate in certain months of a year and plot that on interactive maps. The data will also find the nearest venue, distance, and San Francisco crime to an address that the user chooses. Secondly, the data will also be used to find the top 3 types of crimes in each district and compare and group each district to each other based on the type of crime and frequency. I will use the KMeans model to solve this. Basically, problem one is to find where are most of the crimes in San Francisco located and the second problem is which are the most common types of crime in San Francisco. 

#### 1.3 Interest:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tourists and the police would be interested in the results of this project for many reasons. Firstly, Tourists can figure out where are the safest places to travel and the safest routes in San Francisco. Secondly, the police can figure out where to send their patrolling officers based on the type of crime and frequency of crime. This can make the San Francisco streets safer for everybody. Therefore, this project can contribute much-needed information to the general public.

## Part 2 Data Acquisition and Cleaning:

#### 2.1 Data Sources:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I will use Kaggle datasets and Foursquare location data in order to solve the problems. I will use the "San Francisco Crime Classification" dataset in Kaggle, and here is the link to it https://www.kaggle.com/kaggle/san-francisco-crime-classification. This has data about San Francisco crimes from 2003 to 2015. I will also use a multitude of libraries. The libraries I will use are Folium, Pandas, Numpy, Requests, Sklearn, Matplotlib, Geopy, and some data booting libraries. The data and libraries will help me perform the data analysis and result in some interesting conclusions. 

#### 2.2 Data Cleaning: 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I started off by downloading the test.csv data from the Kaggle data set. Since two questions need to be solved, I copied the data set over to another data set. So, I have two data sets, sf_crime_1, representing the first question, and sf_crime_2, representing the second question.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The first problem I encounter is that the timestamp is in one column. I want the timestamp to be split into years, months, days, hours, and minutes in order to get the data in a specific interval. So, for both data sets, I normalize the timestamps using the pandas to_datetime method and then put each unit of time into columns. So I basically split the timestamps into 5 columns representing units of time. This occurs in both data sets. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To solve the first question, we need to use the frequency of the locations of the crimes. So, if there are crimes with the same location, I will keep them in order to produce an accurate model. Also, there is a bunch of useless information that has nothing to do with this question, so, in the feature selection section, I will discard the useless information. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To solve the second question, we need to use the frequency of the category of crime. So, if there are redundant locations and categories, I will keep them in order to produce an accurate model. Once again, there is a lot of data that has nothing to do with this question, so, in the feature selection section, I will discard the useless information. 

#### 2.3 Feature Selection
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The two data sets have a lot of information that does not help get the answers to the problems. So, in order to lower the size of the data, I remove information that does not relate to the problem. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In the first data set, sf_crime_1, I start off with 878049 samples and 14 features. Now, a lot of this information is useless. So I remove them. I remove the Timestamp, Category, Description, Day of the Week, Resolution, Day, Hour, and Minute. I do not remove the year and the months because I want to create an interval for the data in order to reduce the number of samples. So, I only choose the samples from the first four months of 2014. Now I have 24228 samples and 6 features, the features being the District, Address, Latitude, Longitude, Year, and Month. I also reset the index here. This question has three main parts, so I copy this data into three data sets, sf_crime_cluster, sf_crime_heat, and sf_crime_venue. These data sets are used to create a cluster marker map, a heat map, and a venue finding algorithm. 

<img width="488" alt="Screen Shot 2021-07-20 at 10 52 59 AM" src="https://user-images.githubusercontent.com/76541886/126372340-0b3afe90-8e75-4840-b84b-c8d4ad99010e.png">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In the second data set, sf_crime_2, I once again start off with 878049 samples and 14 features. Now since the frequency of crime in a district is needed, keeping all the samples is important in order to get an accurate model. Also, since we are classifying only 10 districts, the runtime should be relatively quick. In this data set, I also drop some features. I remove the Timestamp, Day of the Week, Resolution, Month, Day, Hour, and Minute. So now I have 878049 samples and 7 features, the features being Category, Description, District, Address, Latitude, Longitude, and Year. Using this data set and other libraries, I can create more data sets that can solve the question. 

<img width="814" alt="Screen Shot 2021-07-20 at 11 05 45 AM" src="https://user-images.githubusercontent.com/76541886/126373550-b715bb16-4bc4-4133-9e2d-f54ecb45aa3b.png">

## Part 3 Data Methodology:

### Problem 1:

#### 3.1 Description of Code:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;After the data cleaning process, I started to code a visualization of the data in order to solve the problem. So first, I created a marker cluster map. It can help find where crimes are located. I imported the Marker Cluster library from Folium.Plugins and then started to create a Folium Cluster map. I started by creating a folium map called marker_cluster_map with the coordinates on San Francisco, a starting zoom of 12, and the ability to display a control scale. From there, I got the Latitude and Longitude values from the sf_crime_cluster data set and put them into a list so I can plot the points on the map. Then I iterated through the data set to get the Districts and Addresses and put them into a list so each point can be labeled. I then defined the marker cluster part of the map through an object called MarkerCluster. The MarkerCluster object has parameters for the locations of the crimes and the labels of the crimes, both of which were defined earlier. I then added this MarkerCluster object to the map and then displayed the map. The results will be shown later in the Results part of this report. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;After creating the Marker Cluster map, I thought it would be more helpful to create a Heat Map as well. Heat Maps are more interpretable than Marker Cluster Maps and they find the density of crimes. So, you can determine where most of the crimes are. So, I start by importing the Heat Map library from Folium.Plugins. I then create a folium map with the same parameters as before. The coordinates are on San Francisco, the start zoom is 12, and the map has a control scale. I then get the locations of each crime using the sf_crime_heat data set. Since heat maps do not have markers, I do not need to get the district name and address as done with the Marker Cluster map. I then create a HeatMap object with the locations as the data and the radius of each crime to be 10 units. I add this object to the map and display the map. The results will be shown later in the Results part of this report. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;After I visualize the data and solve the main problem. I want to create something extra that can find the nearest venue to the location that a user inputs. I want it to also find the distance to the nearest crime in San Francisco and the nearest San Francisco Crime. So first I start off by defining my Foursquare information. This is hidden for privacy. I then define a getNearbyVenues function which takes a set of coordinates and a name and gets the name of the nearest venue. It works by using the Foursquare API and my information in order to get information about a location. I also define a checking function which basically ensures that the following code does not result in an error using python's try and except functions. From there I create a complicated piece of code that accomplished my goal. In this complicated piece of code, I import Nominatim and distance from geopy. I then create an infinite while loop where the user inputs an address. A Nominatim object is then created and it is used to get information about the address. I then check if the user's address is exit, if so, then I break the while loop and the cell is complete. I then check if the address is valid using the checking address defined previously. If the address is valid, I get the locations coordinates and San Francisco's crime coordinates and find the least distance between a crime in San Francisco and the address inputted. I then use the getNearbyVenues function to get the nearest venue to the address. I then print out the nearest venue to the address, the address of the nearest crime to the user's address, and the distance, in miles, to the nearest crime. This entire process is then repeated once again. So, I basically created something that lets users input an address, giving you the nearest venue to the address and the distance to the nearest crime in San Francisco. An example will be shown in the Results section of this report. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So, in this question, I basically visualized the data by creating two separate maps of it. I then created a type of app that finds some information about an address that a user inputs. Keep in mind that this data is from the first 4 months of 2014. In the Results section of this report, I will show examples of what came out of my code. 

### Problem 2:

#### 3.2 Description of Code:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In this problem, I need to find which are the most common crimes in each district and compare them. So first I check if there are any missing values in sf_crime_2 by using the .count() and groupby method. I then create a data set called sf_coords. This is created by getting the mean value of the coordinates of the districts. sf_coords will be used later in order to plot the districts on a map. From here, I use something called One-Hot Encoding in order to create a vector for each crime. One-Hot Encoding is a vectorizer. This data is stored in a data set called sf_crime_onehot. This type of vectorizer is used for comparing, which we are going to do later. Then I used the groupby and mean methods to get a frequency table of each type of crime in each district. I stored this in the sf_crime_grouped data set. Basically, this data set finds the percentage of crime categories in each district. This will be used in order to cluster districts later. The data will be shown in the Results section.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The previous paragraph is the methodology of the setup of the map and clustering. In this paragraph, I will talk about finding the most common types of crimes in a district. So first, I define the function, return_most_common_crime, which, as it states, returns the most common crimes. So, I then indicate that I want the top three crimes to be displayed, and then create a data set called PdDistrict_sorted. It has the 10 districts and the top 3 most frequent crimes in each district. This is highly interpretable and tells you which districts have the most common type of crimes. I will share the data in the Results section of this Notebook. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I then use an unsupervised machine learning model called KMeans. It is a categorical model that is really fast and can draw conclusions based on unsupervised data. It creates clusters based on the data and categorizes information. I want to compare and cluster districts, so KMeans is a great way to do so. In order to use the KMeans model, I define the number of clusters, 3, and then clean the sf_crime_grouped data set by removing non-numeric data. I then run and fit the KMeans model and then get the cluster labels that I then merge with the coordinate data. So, I now have a data set called sf_merged that has the District, Latitude, Longitude, Cluster Label, 1st Most Common Crime, 2nd Most Common Crime, and 3rd Most Common Crime. I will share the results in the Results section of this report.  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Now I want to visualize the cluster on a map. So I create a map centered on San Francisco using Folium. I then plot the districts using the coordinate data created a little bit ago. Each data point has a color representing its cluster label. Each point has a label stating the District Name and the cluster label. So, I basically have compared and clustered each San Francisco District to each other. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I have successfully found the most common types of crime in each San Francisco Districts. I have also compared and clustered each District using an unsupervised machine learning model called KMeans. Keep in mind that the data in this problem is from 2003 to 2015. I have visualized the results in the Results section of this report. 

## Part 4 Results:

### 4.1 Problem 1 Results:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Visualizing the locations of the crimes led to two maps. Each map is interactive and shows where most of the crimes are. They show the crimes in San Francisco in the time interval 2014 January to 2014 April. 

Marker Cluster Map:

<img width="834" alt="Screen Shot 2021-07-23 at 6 47 36 PM" src="https://user-images.githubusercontent.com/76541886/126854117-0af1360e-59ca-4295-9247-1575e6b8ae24.png">

Heat Map:

<img width="840" alt="Screen Shot 2021-07-23 at 6 48 05 PM" src="https://user-images.githubusercontent.com/76541886/126854129-be520908-f1a3-4222-9f97-7d1b760269cd.png">
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As you can see the northwest area of San Francisco has the highest amount of crime and the highest density. The southeast area of San Francisco is the complete opposite. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Here is an example of the venue code specified in the Methodology Section. 

<img width="802" alt="Screen Shot 2021-07-23 at 7 40 33 PM" src="https://user-images.githubusercontent.com/76541886/126855248-26778053-40e2-4c75-9084-9f3a7bbfe237.png">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;You can enter an address and it results in the following information. 

### 4.2 Problem 2 Results:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In this problem, there was a large methodology to get to the result. So, I will display the results of some of the steps. Keep in mind that this data has a 12-year interval from 2003 to 2015. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The first step, checking crime values, is displayed below.

<img width="621" alt="Screen Shot 2021-07-23 at 7 55 52 PM" src="https://user-images.githubusercontent.com/76541886/126855574-da94d12d-5283-4763-985f-69e9bb88328c.png">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The second step, creating the sf_coods data set. The sf_coords data set:

<img width="249" alt="Screen Shot 2021-07-23 at 7 59 07 PM" src="https://user-images.githubusercontent.com/76541886/126855591-a913107d-d941-4aaa-8c0b-7f80a11727d8.png">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Next, using One-Hot Encoding as a vectorizer. Using One-Hot Encoding:

<img width="872" alt="Screen Shot 2021-07-23 at 8 00 17 PM" src="https://user-images.githubusercontent.com/76541886/126855615-7ea69528-19c0-4fe5-ab45-74e4e7b531e7.png">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Creating a frequency table for each district. This is a frequency table for categories of crime. 

<img width="855" alt="Screen Shot 2021-07-23 at 8 01 18 PM" src="https://user-images.githubusercontent.com/76541886/126855644-833a40a7-6d88-4cf1-aff7-2a280d0d8dbf.png">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The most common type of crimes for each category is created, which is shown below.

<img width="566" alt="Screen Shot 2021-07-23 at 8 03 30 PM" src="https://user-images.githubusercontent.com/76541886/126855680-13b438e2-4bd6-4933-ad9b-6664ff1481b5.png">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Creating a map that is based on the comparison of each district. The KMeans algorithm categorized each district and it is displayed in this map. 

<img width="839" alt="Screen Shot 2021-07-23 at 8 04 09 PM" src="https://user-images.githubusercontent.com/76541886/126855710-e6d63b3d-4398-4516-87f9-768a20a77a9b.png">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The images below show the districts in each cluster. It has three clusters and 10 districts. 

<img width="779" alt="Screen Shot 2021-07-23 at 8 05 31 PM" src="https://user-images.githubusercontent.com/76541886/126855727-5f418501-ac34-4ec6-9437-92e725cbcff5.png">

<img width="785" alt="Screen Shot 2021-07-23 at 8 05 35 PM" src="https://user-images.githubusercontent.com/76541886/126855729-a87f14a0-a34e-4035-8b45-caed08c76e1b.png">

<img width="800" alt="Screen Shot 2021-07-23 at 8 05 38 PM" src="https://user-images.githubusercontent.com/76541886/126855732-be4faad6-6a6a-408b-8b96-8fe2219b0a8c.png">

## Part 5 Interpreting Results:

### 5.1 Overview:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Interpreting the results can lead to conclusions, however, the conclusions might be skewed due to factors out of my control. An example of this is that this data is taken from Police reports, meaning that crimes that were not reported nor found out were not accounted for in this analysis. Also, the crime data represent San Francisco crime, so if there was crime taken near the borders of San Francisco, it might now have been accounted for.  

### 5.2 Problem 1:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;We can interpret the interactive maps by saying that crime density was particularly high in northwest San Francisco. We can also say that crime density was the lowest in the southeast area of San Francisco. Also, this is crime density per unit of area. So, the population density might have also affected this. Nevertheless, we can conclude that northeastern San Francisco contains the highest rate of crime based on the maps generated based on the data. I would recommend sending more police forces to the northeastern area of San Francisco. I would also recommend avoiding the northeastern area. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The interactive cell of my code might not have much to interpret, but it's basically an app to users find the safest locations to travel to. It could help users plan out their travel plans and stay safe. 

Keep in mind these results relate to the first 4 months of 2014. 

### 5.3 Problem 2: 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This problem has highly interpretable results that can benefit a lot of people. First, the map demonstrates that the central and southern parts of San Francisco have the same types of crime and are really similar to each other. They are areas that contain minor crimes like theft and non-criminal offenses. The north section of San Francisco contains a lot of crime relating to more scary aspects of life. It has a huge amount of theft, a lot of drug usage, and a lot of other offenses. This means that the northern section required more caution in regards to drugs and property theft. The southern and central areas of San Francisco seem to require less caution in regards to drugs, but other minute crimes like small theft still need to be watched for. I also recommend sending officers specialized in theft and drugs in the northern areas while sending general small crime officers to the southern areas. 

Keep in mind these results relate to a 12-year interval from 2003 to 2015. 

### 5.4 Combined Conclusion:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The combined conclusion from both of the problems is really useful to everybody. First off, the Northern area of San Francisco contains crime relating to drugs and theft. This crime is much more common in this area. The central and southern area has crimes relating to theft and non-criminal offenses. This crime is less common. Basically, we can infer that the southern areas of San Francisco are safer to travel to. If you travel to the northern areas, be wary of theft and drug usage. I would recommend sending more officers to northeastern San Francisco to deal with theft and drugs. I would recommend sending fewer officers to the southern areas and, if needed, specifically keep watch for small crimes. I think that these recommendations will help keep everybody in San Francisco safer. 

## Part 6 Conclusion:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;All in all, this analysis reviewing the crime data in San Francisco was really fun to do. I learned a lot about the crime in San Francisco, and it led to some results that led to some interesting conclusions. These conclusions, stated above, can help people stay safer as they travel to San Francisco. However, there are some shortcomings that can cause some of the conclusions to fail. For example, this data is from a decade ago, so crime might have changed in recent years. Also, the crimes are based off police reports so some of the crimes will not be included because it was not reported. Nevertheless, the analysis provided insights into the locations of the crime and the type of crimes that occurred. It was really fun and I hope to do more in the future. 
