---
author:
  twitter: linwoodc3
summary: This post introduces a utility function that can automatically read web-based or local shapefiles in zip format into the Python ecosystem.  It takes one line of code!
---

# Spatial Context in Python: Reading Web-based or Local Shapefiles

There's nothing more disconcerting than not knowing your location.

Knowing your location brings comfort. 

We have all experienced it.  It's the panic that overtakes you when you don't recognize your surroundings.  The buildings and roads are unfamiliar.  You don't know where you are.  Naturally, you focus on getting to a familiar landmark or location.  Reaching that landmark brings a sense of relief.   Comfort.  Peace.  Because you know where you are on a map, it's easier to plot a course to your final destination.  

In the world of data science, we embrace the concept of spatial awareness and knowing where the data are (or datum is).  In the same way that geospatial grounding (i.e. [georeferenced data](https://en.wikipedia.org/wiki/Georeferencing)) brings clarity to a lost traveler, spatial context can bring clarity to a data set.  Moreover, this "where" does not always have to apply to a location on the earth's surface . Spatial context (i.e. [analytic geometry](https://en.wikipedia.org/wiki/Analytic_geometry)), or understanding data in the context of  geometric space, is just as enlightening.  

The Ansecombe's quartet is our model case. As the famous figure below shows, spatial awareness adds a new dimension of understanding of the data. Despite having nearly identical descriptive statistics, the four data sets are quite different spatially. 
<center><img src="{{ site.url }}/assets/img/anscombe.png" alt="Anscombe's Quartet" width="600" height="450"></center>



```python
import pandas as pd
```


```python

```
