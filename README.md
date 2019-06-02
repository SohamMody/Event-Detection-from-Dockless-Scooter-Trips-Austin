# Event Detection based on Dockless Scooter Trips in Austin, Texas

Dockless scooters are a recent occurrence in cities and towns across the United States. There is still relatively little understanding in how they fit into the cities and towns they operate in. There are various benefits with this technology -- scooters are readily available, cheap, and fun to ride. They are also touted as a solution for the first-mile/last-mile problem, which is something even the most developed transit systems still struggle with. 

Nevertheless, scooters have seen a fair share of opposition and problems. One of the biggest concerns is that these scooters affect city operations. Scooters impair the orderliness and safety of streets and sidewalk. In Washington, DC, San Francisco, and Austin, local residents have been forced to accept the new way of transit. People say they often feel unsafe around people riding scooters and many report that they have multiple almost collisions with riders.  

The issue gets even more out-of-control when masses gather for an event. This had happened in Austin in 2018 during the SXSW festival when scooters became a fun and cheap way to travel to conference events. Thousands of scooters could be found in downtown Austin, many of them obstructed the sidewalks, roads, public and private spaces. Riders were mostly not wearing helmets, cruising at high speeds. Although the city did not announce that they had any issues with it, many residents complained. An issue of forecasting such events (and smaller ones) and tying scooter ridership arises.  

We try to answer the following questions in our research:
 ### Can significant social events in Austin be detected using dockless electric scooter data in a predictive manner? Can the demand for scooters be predicted during events like holiday, sporting events, and concerts? Can we come up with a model that incorporates exogenous variables such as location of trip’s origin and trip duration to make predictions? 
 
This is a project done by Soham Mody and Timur Mukhtarov for the course Machine Learning for Cities as a part of our master's in urban data science at New York University.

The main code has been divided into 3 parts for ease of understanding. 
1.) In Preprocessing.ipynb, we download the dockless scooter trip data along with the council district and census tract shapefiles and apply the basic preprocessing steps that we think are needed just doing an initial analysis of the dataset. 

2.) Then, we use this processed data in EDA.ipynb where we do an exploratory data analysis of the trips dataset. Here, we further do some processing that is needed before feeding the data to the models and also, do some analysis of ridership counts from a time of the day and geospatial point of view. We also aggregate the data by census tract so that, it is easier to do the modelling and anomaly detection.

3.) Finally, we apply 3 models to the prepared data from EDA.ipynb to detect anomalies(events) in Modelling.ipynb. We choose a time-series forecasting model SARIMA as our baseline model and then, apply more sophisticated methods like Isolation Forest and Local Outlier Factor. We also PCA during the latter 2 models to get the 2 most prominent features as visualing the results in 2-D helps us to choose a better contamination value(percentage of total observations which are outliers) for these models.

From the results in Modelling.ipynb, we can see that our models predicted many dates as event. We validated the results by doing a Google search of the predicted dates and found that the models was able to successfully detect events like the Austin City Limits Festival and New Year’s Eve as well as bad weather days.

Also, we can see that, both the Isolation Forest and the Local Outlier Factor models detect more events compared to the baseline model. This is due to the contamination value being more flexible. Thus, we are able to detect more events even though this may increase the number of normal events being detected as anomalies in some cases. Additionally, we can see how Isolation Forest just sees things on a global scale and classifies events just on that basis which might result in it missing many local outliers and even more normal events being classified as anomalies. But, density-based methods like LOF solve this problem by looking at the observation from a local perspective and are able to detect these local outliers. 

Of course in the case of a huge city like Austin, none of these results can conclusively predict that an event did occur as there could be many external factors for the abnormal shift in the values of these features. Additionally, the results would always need to be validated against real world information to see if they are correct.


