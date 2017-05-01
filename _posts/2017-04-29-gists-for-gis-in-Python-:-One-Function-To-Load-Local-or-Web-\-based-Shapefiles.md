---
title: "GitHub Gists for GIS in Python: Loading a Zipped Local or Web-based Shapefile with One Function" 
author:
  twitter: linwoodc3
summary: This post introduces a utility function that can automatically read web-based or local shapefiles in zip format into the Python ecosystem.  It takes one line of code!
excerpt: "In the world of data science, we embrace the concept of spatial awareness and knowing where the data are (or datum is). In the same way that geospatial grounding (i.e. georeferenced data) brings clarity to a lost traveler, spatial context can bring clarity to a data set.  Moreover, this “where” does not always have to apply to a location on the earth’s surface . Spatial context (i.e. analytic geometry), or understanding data in the context of geometric space, is just as enlightening."
---

## GitHub Gists for GIS in Python: Loading a Zipped Local or Web-based Shapefile with One Function 
**Date:** {{ page.date | date_to_rfc822 }}<br><br>

There is nothing worse than not knowing where you are.

We have all experienced it.  It’s the panic that overtakes you when you don’t recognize your surroundings.  The buildings and roads are unfamiliar.  You don’t know where you are.  Naturally, you focus on getting to a familiar landmark or location.  Reaching that landmark brings a sense of relief.   Comfort.  Peace.  Because you know where you are on a map, it’s easier to plot a course to your final destination.

In the world of data science, we embrace the concept of spatial awareness and knowing where the data are (or datum is). In the same way that  familiar surroundings (i. e. [geo-referenced data](https://en.wikipedia.org/wiki/Georeferencing)) brings clarity to a lost traveler, spatial context can bring clarity to a data set.  This “where” does not always have to apply to a location on the earth’s surface. Spatial context (i.e. [analytic geometry](https://en.wikipedia.org/wiki/Analytic_geometry)), or understanding data in geometric space, is just as enlightening.

[Ansecombe’s quartet](https://en.wikipedia.org/wiki/Anscombe%27s_quartet) is a great example. Despite having nearly same summary statistics, the plots are nowhere near same.  This is a reminder to plot your data before drawing a conclusion.  It can prevent costly errors. 

Python `seaborn` includes this data set, and we load it and compute the summary statistics.  Each row represents a data set; you can see that numbers are nearly identifical.  

```python
import seaborn as sns

#load the data
df = sns.load_dataset('anscombe')

#perform groupby, compute summary, and unstack
ddf = df.groupby('dataset').describe().unstack()

# print the results
print(ddf)
```

<center><img src="{{ site.url }}/assets/img/anscombe.png" alt="Anscombe's Quartet" width="600" height="450"></center>

![]("{{sit.url }}/assets/img/ansecombe.html")
```python
import pandas as pd
```


```python

```
