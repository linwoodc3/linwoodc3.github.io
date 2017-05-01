---
title: "The Importance of Where: Adding Spatial Context Using Local or Web-based Shapefiles" 
author:
  twitter: linwoodc3
summary: This post introduces a utility function that can automatically read web-based or local shapefiles in zip format into the Python ecosystem.  It takes one line of code!
excerpt: "In the world of data science, we embrace the concept of spatial awareness and knowing where the data are (or datum is). In the same way that geospatial grounding (i.e. georeferenced data) brings clarity to a lost traveler, spatial context can bring clarity to a data set.  Moreover, this “where” does not always have to apply to a location on the earth’s surface . Spatial context (i.e. analytic geometry), or understanding data in the context of geometric space, is just as enlightening."
---

## The Importance of "Where": Adding Spatial Context Using Local or Web-based Shapefile
**Date:** {{ page.date | date_to_rfc822 }}<br><br>

There is nothing worse than being lost.

We have all experienced it.  It’s the panic that overtakes you when you don’t recognize your surroundings.  The buildings and roads are unfamiliar.  You don’t know where you are. You have no spatial context. Naturally, you focus on getting to a familiar landmark or location.  Reaching that landmark brings a sense of relief.   Comfort.  Peace.  Because you know where you are on a map, it’s easier to plot a course to your final destination.

In the world of data science, we embrace the concept of spatial awareness and knowing where the data are (or datum is). In the same way that  familiar surroundings (i. e. [geo-referenced data](https://en.wikipedia.org/wiki/Georeferencing)) brings clarity to a lost traveler, spatial context can bring clarity to a data set.  This “where” does not always have to apply to a location on the earth’s surface. Spatial context (i.e. [analytic geometry](https://en.wikipedia.org/wiki/Analytic_geometry)), or understanding data in geometric space, is just as enlightening.

## Anscombe's Quartet - The Importance of Spatial Context
[Anscombe’s quartet](https://en.wikipedia.org/wiki/Anscombe%27s_quartet) is a great example. Despite having nearly same summary statistics, the plots are nowhere near same.  This is a reminder to plot your data before drawing a conclusion.  It can prevent costly errors. 

Python's [`seaborn` library](https://seaborn.pydata.org/) includes this data set, and we load it and compute the summary statistics. Each column is a different data set, and it's clear that the numbers are nearly identical.<br><br>

```python
import seaborn as sns

# load the seaborn example data
df = sns.load_dataset('anscombe')

# group the data into multiindex df and unstack
ddf = df.groupby('dataset').describe().unstack()

# slice multiindex data
All = slice(None)
test = ddf.T.loc[(All,slice('mean','std')),All]
print(test)
```

statistic | I  | II  | III | IV  
----:|----:|----:|----:|----:
Mean of X | 9.000|9.000|9.000|9.000
StdDev of X | 3.317|3.317|3.317|3.317
Mean of Y | 7.501|7.501|7.500|7.501
StdDev of Y | 2.032|2.032|2.030|2.031

<br><br>The standard deviation and mean have few differences.  Now let's look at the visual of the same data.<br><br>  

<center><img src="{{ site.url }}/assets/img/anscombe.png" alt="Anscombe's Quartet" width="600" height="450"></center><br><br>


The plots are very different.  Again, this is a reminder that you should plot your data and see if you gain any new insights.

## Adding Complementary Data

That small detour was to prove the power of spatial context and set the stage for my Github Gist.  In this day and age of smartphones, geolocation services, and public data streams, geospatial data is easy to find. But getting the data is not the goal. Drawing meaning from the data is our focus.  Lucky for us, the data is referenced to a spot on the earth, but we need a complementary data set with features of the earth or physical locations to really add context.  A dump of tweets with latitude and longitude pairs are just dots plotted on a map.  But, add a basemap or underlying spatial file, and you understand **where** users were when they tweeted.  

I made a Github Gist that helps in this very area.  All you have to do is pass a string as an argument, and regardless of whether the string points to a local or web-based file, you return a spatial object.  The big benefit?  This function is focused on handling zipped shapefiles!  If you work with in the geosptial arena, you are quite accustomed to zipped shapefile data. 

Here is the Gist:<br><br>

{% gist linwoodc3/72b2f24b6d2ff6ffde1597f1ca2dea3f %}
<br><br>

## Demonstrating the Shapefilereader function

We will walk through a quick demo.  Assume we have a `geopandas` data set of tweets passed to us from a colleague, and she only tells us the tweets originated in New York.  She asks for our help in finding the origin zip code for each tweet.  Here are the first 10 rows of the data:<br><br>

```python
import pickle
import geopandas as gpd

# load the pickled data
dg = pickle.load(open('data.pkl','rb'))
print(dg.head(10))
```


lang|               geometry               
----|--------------------------------------
en  |POINT (-73.985131 40.758895)          
en  |POINT (-73.86167 40.7579249)          
en  |POINT (-73.985131 40.758895)          
en  |POINT (-74.10066217000001 40.68497132)
en  |POINT (-71.1956205 42.5047161)        
en  |POINT (-79.98186 40.4285799)          
en  |POINT (-74.018036 40.704395)          
en  |POINT (-71.1097335 42.3736158)        
en  |POINT (-72.8620251 40.8230795)        
en  |POINT (-71.4372796 41.7798226)  

<br><br>Let's get some spatial context from the original data set.  A simple scatter plot is sufficient.<br><br>

```python
import matplotlib.pyplot as plt

# plot the geodataframe
f,ax = plt.subplots(figsize=(15,9))
dg.plot(color='red',ax=ax)
plt.show()
```

<center><img src="{{ site.url }}/assets/img/newyorktweets.png" alt="Non-context NY tweets" width="600" height="450"></center><br><br>

It's hard to tell anything from this plot. An easy fix is to plot this data in the context of something known.  In this case, we find a [publiclly available shapefile that represents New York's zip codes](https://data.cityofnewyork.us/Business/Zip-Code-Boundaries/i8iw-xf4u/data).  Our new function loads the data seamlessly.  

```python
from shapefilereader import shapefilereader

# reading data from NY open data website
ny = shapefilereader('https://data.cityofnewyork.us/download/i8iw-xf4u/application%2Fzip')
ny= ny.to_crs({'init':"epsg:4326"}) # reproject coordinates

# ploting the data
f,ax = plt.subplots(figsize=(15,9))
ax.set_facecolor('lightblue') # setting ocean color
ny.plot(color='tan',ax=ax)
plt.show()
```

<center><img src="{{ site.url }}/assets/img/newyorkzips.png" alt="NY zipcodes" width="600" height="450"></center><br><br>

Based on the shape of the new file, we are starting to understand the context of the data.  The higher concentration areas of our first plot correspond to the New York zip code shapes in our second plot.  We can do better. Next, we combine the two files using a [spatial join](http://geopandas.org/mergingdata.html?highlight=sjoin#spatial-joins) and find the origin zip code for each tweet. <br><br>

```python
import geopandas as gpd

# geopandas spatial join on tweets and zipcode shapefile
nytweets = gpd.sjoin(dg.reset_index(),ny[['ZIPCODE','geometry']],op='intersects',how='inner')
```

<br><br>We can do a lot with this joined table, which was enabled by our shapefilereader function.  Notably, we can answer our colleague's question.  Here is a graphical answer using a [choropleth visualization](https://en.wikipedia.org/wiki/Choropleth_map):<br><br>  

```python
# group the data by zipcode
countedTweets = nytweets.groupby('ZIPCODE')['ZIPCODE']\
.size().sort_values(ascending=False)\
.reset_index().rename(columns={0:'tweetcount'})

# attribute merge with zipcode data
final = ny[['ZIPCODE','geometry']].merge(countedTweets,on='ZIPCODE')

# plot the choropleth
f,ax = plt.subplots(figsize=(15,9))
final.plot(column='tweetcount', scheme='Fisher_Jenks', k=5, cmap='OrRd', linewidth=0.1, ax=ax,legend=True)
ax.set_axis_off()
plt.show()
```

<center><img src="{{ site.url }}/assets/img/newyorkchoropleth.png" alt="NYchoropleth" width="600" height="450"></center><br><br>
And here are the first 10 rows of our tabular answer to the question.<br>

ZIPCODE|tweet count
------:|----------:
  10007|        684
  10036|        303
  10001|        257
  10013|        199
     83|        132
  10003|        131
  10019|        130
  11201|        122
  10014|        120
  10011|         99
  
## Conclusion
<br><br>As shown above, spatial clarity can improve your understanding of data.  Feel free to use the shapefilereader function to add complementary data sets to your geospatial analysis tasks. We combined our source data with a publicly available shapefile.  And in the end, we were able to answer our target questions in visual and tabular format.  Try a similar workflow on one of your datasets! 

