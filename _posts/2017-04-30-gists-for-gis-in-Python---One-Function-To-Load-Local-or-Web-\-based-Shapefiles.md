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

We have all experienced it.  It’s the panic that overtakes you when you don’t recognize your surroundings.  The buildings and roads are unfamiliar.  You don’t know where you are.  Naturally, you focus on getting to a familiar landmark or location.  Reaching that landmark brings a sense of relief.   Comfort.  Peace.  Because you know where you are on a map, it’s easier to plot a course to your final destination.

In the world of data science, we embrace the concept of spatial awareness and knowing where the data are (or datum is). In the same way that  familiar surroundings (i. e. [geo-referenced data](https://en.wikipedia.org/wiki/Georeferencing)) brings clarity to a lost traveler, spatial context can bring clarity to a data set.  This “where” does not always have to apply to a location on the earth’s surface. Spatial context (i.e. [analytic geometry](https://en.wikipedia.org/wiki/Analytic_geometry)), or understanding data in geometric space, is just as enlightening.

[Ansecombe’s quartet](https://en.wikipedia.org/wiki/Anscombe%27s_quartet) is a great example. Despite having nearly same summary statistics, the plots are nowhere near same.  This is a reminder to plot your data before drawing a conclusion.  It can prevent costly errors. 

Python's `seaborn` library includes this data set, and we load it and compute the summary statistics.  Each row is a data set, and it's clear that the numbers are nearly identical.


```python
import seaborn as sns
import matplotlib.pyplot as plt

%matplotlib inline

df = sns.load_dataset('anscombe')

ddf = df.groupby('dataset').describe().unstack()
ddf
```




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>x</th>
      <th>y</th>
    </tr>
    <tr>
      <th>dataset</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">I</th>
      <th>count</th>
      <td>11.000000</td>
      <td>11.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>9.000000</td>
      <td>7.500909</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.316625</td>
      <td>2.031568</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.000000</td>
      <td>4.260000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.500000</td>
      <td>6.315000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>9.000000</td>
      <td>7.580000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>11.500000</td>
      <td>8.570000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>14.000000</td>
      <td>10.840000</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">II</th>
      <th>count</th>
      <td>11.000000</td>
      <td>11.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>9.000000</td>
      <td>7.500909</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.316625</td>
      <td>2.031657</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.000000</td>
      <td>3.100000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.500000</td>
      <td>6.695000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>9.000000</td>
      <td>8.140000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>11.500000</td>
      <td>8.950000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>14.000000</td>
      <td>9.260000</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">III</th>
      <th>count</th>
      <td>11.000000</td>
      <td>11.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>9.000000</td>
      <td>7.500000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.316625</td>
      <td>2.030424</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.000000</td>
      <td>5.390000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.500000</td>
      <td>6.250000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>9.000000</td>
      <td>7.110000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>11.500000</td>
      <td>7.980000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>14.000000</td>
      <td>12.740000</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">IV</th>
      <th>count</th>
      <td>11.000000</td>
      <td>11.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>9.000000</td>
      <td>7.500909</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.316625</td>
      <td>2.030579</td>
    </tr>
    <tr>
      <th>min</th>
      <td>8.000000</td>
      <td>5.250000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>8.000000</td>
      <td>6.170000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>8.000000</td>
      <td>7.040000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>8.000000</td>
      <td>8.190000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>19.000000</td>
      <td>12.500000</td>
    </tr>
  </tbody>
</table>



Now here is a plot of the four data sets.

<center><img src="{{ site.url }}/assets/img/anscombe.png" alt="Anscombe's Quartet" width="600" height="450"></center>



```python

```
