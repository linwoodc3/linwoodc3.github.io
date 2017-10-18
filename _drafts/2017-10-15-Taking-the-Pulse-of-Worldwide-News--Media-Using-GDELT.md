---
layout: post
draft: true
title: "Terror on the Strip: Building Event Timelines with Python and GDELT" 
comments: true
author:
  twitter: linwoodc3
  email: valinvescap@gmail.com
  facebook: 
  flickr:
  github: linwoodc3
  instagram: linwoodc3
  linkedin: https://www.linkedin.com/in/linwood-creekmore-iii-a2174538
  pinterest:
  rss: datajourney
  stackoverflow: users/4205207/linwoodc3
  youtube: # channel/<your_long_string> or user/<user-name>
  googleplus: u/0/+LinwoodCreekmore 
summary: This post uses news metadata from GDELT to create a substantive event timeline of the recent crisis in Marawi.  I also introduce my Python client to access and process GDELT data in the Python ecosystem.  This is especially useful if you have business interests in areas with stability issues. If you like time series analysis (you'll see potential), geospatial analysis, data analytics, and data engineering, you will enjoy this post! 
excerpt: It all started a few minutes after 10 pm on October 1st.<br> he gunshots sounded like firecrackers at first.  People in the crowd didn't understand what was happening when the band stopped playing and Jason Aldean hustled off stage.<br>"That's gunshots," a man said on a cellphone video in the nearly half-minute of silence and confusion that followed. Then the pop-pop-pop noise resumed. And pure terror set in.

---


<div class="image">
<center><img src="{{ site.url }}/assets/img/concertOverview.jpg" alt="City entranc" ></center>
<div><center><font size=".5"><b>Image: The grounds at the Route 91 Harvest festival on Las Vegas Boulevard South in Las Vegas on Saturday, Sept. 30, 2017. <a href="https://en.wikipedia.org/wiki/Mandalay_Bay" target="_blank"> Mandalay Bay Hotel and Casino</a> can be seen in the background behind the stage. <br><i>Source: http://news3lv.com/, file</i></b> </font></center></div>
<br>
</div>
## Terror on the Strip
<body style="background-color:powderblue;">
<p style="font-family:courier;"><i>It all started a few minutes after 10 pm on October 1st.<br><br>

The gunshots sounded like firecrackers at first.  People in the crowd didn't understand what was happening when the band stopped playing and <a href="https://www.google.com.kh/search?q=Jason+Aldean&rlz=1C5CHFA_enUS751US751&source=lnms&sa=X&ved=0ahUKEwjj-aDZsfHWAhVDjLwKHTRjC_UQ_AUICSgA&biw=1280&bih=682&dpr=1" target="_blank">Jason Aldean</a> hustled off stage.<br><br>  

"That's gunshots," a man said on a cellphone video in the nearly half-minute of silence and confusion that followed. Then the pop-pop-pop noise resumed. And pure terror set in.<br><br>

For reasons that remain unknown, <a href="https://en.wikipedia.org/wiki/Stephen_Paddock" target="_blank">Stephen Craig Paddock</a> fired on a crowd of 22,000 for 10 minutes unhindered in 40- to 50-round bursts from his 32nd floor room of the <a href="https://en.wikipedia.org/wiki/Mandalay_Bay" target="_blank"> Mandalay Bay Hotel and Casino</a>. Paddock had at least 20 guns and hundreds of rounds of ammunition — some with scopes — in his hotel room, and busted out windows with a hammer-like object to create his sniper's perch roughly hundreds of yards from the <a href="https://en.wikipedia.org/wiki/Route_91_Harvest" target="_blank">Route 91 Harvest Festival of country music</a>. Analysis of the shooting video showed Paddock fired a staggering 280 rounds in one 31-second span.<br><br>


<br>
<div class="image">
<center><img src="{{ site.url }}/assets/img/runningcrowd.jpg" alt="Chaos in the crowd" ></center>
<div><center><font size=".5"><b>Image: Chaos as shots rang out at the Route 91 Harvest Country Music Festival in Las Vegas. <br><i>Source: David Becker/Getty Images</i></b> </font></center></div>
<br><br>
</div>
</i></p>     
</body>
<body style="background-color:powderblue;">
<p style="font-family:courier;"><i>
While some concertgoers hit the ground, others forced their way to the crowded exits, shoving through narrow gates, trampling one another, and climbing over fences. They had little cover and no easy way to escape. Those who were not hurt hid behind concession stands or crawled under parked cars. The scene was pure chaos. Bodies were lying on the artificial turf installed in front of the stage, and people were screaming and crying. The sound of people running on the bleachers added to the confusion, leading some of the people still present to suspect the concert was being invaded with multiple shooters. 
<br><br>


At 10:14 p.m., an officer said on his radio that he was pinned down against a wall on Las Vegas Boulevard with 40 to 50 people."We can't worry about the victims," an officer said at 10:15 p.m. "We need to stop the shooter before we have more victims. Anybody have eyes on him ... stop the shooter."

 <br><br>
 
Police frantically tried to locate the shooter and determine whether the gunfire was coming from Mandalay Bay or the neighboring Luxor hotel. Every second was precious.  Any time wasted looking in the wrong hotel resulted in more time to reload and unleash a volley of bullets on the terrified crowd below.
<br>
<div class="image">
<center><img src="{{ site.url }}/assets/img/runningCops.jpg" alt="Police taking cover" ></center>
<div><center><font size=".5"><b>Image: Las Vegas police running along the streets outside the festival grounds of the Route 91 Harvest festival. <br><i>Source: John Locher/AP Photo</i></b> </font></center></div>
<br><br>
</div>
</i></p>     
</body>

<hr>
<br>
        
# Code/Tutorial Introduction
This narrative story/data science tutorial provides a short introduction to a python client I built to access and wrangle georeferenced news information using <a href ="http://www.gdeltproject.org/about.html" target="_blank">Global Database of Events, Language, and Tone (GDELT)</a>.  By the end, you will have the tools needed to build a timeline of events using Python and `gdeltPyR`.  For others considering writing a tutorial, try writing a narrative format as well. Data scientists and data engineers need to be well versed in the art of writing and narratives provide great practice!  You can <a href="https://github.com/linwoodc3/linwoodc3.github.io/blob/master/notebooks/gdeltPyR%20Tutorial%20Notebook.ipynb" target="_blank">download the notebook for this tutorial here</a>. 

### Post Format
Each narrative section is followed by a coding/description section.  I use a page splitter and different font to mark the switch from a narrative to a coding section.  

Every fact or detail in the narratives came from news stories accessed via `gdeltPyR`. Using data wrangling and time series analysis techniques, we can order the stories chronologically to see how this active shooter event evolves in time.  Around one hour after the first gunshots sprayed the concert, GDELT was able to automatically geolocate this event to Las Vegas and catalogue it as a crisis involving firearms. The first GDELT report came at 11:15 PDT (06:15 in UTC time); the shots started at 10:08 (05:08 UTC)!  Using geolocated news data and CAMEO codes, we can identify statistically significant changes in volume using an exponentially weighted moving average.  First, let's take a minute to understand what GDELT is.  

<br>
<div class="image">
<center><img src="{{ site.url }}/assets/img/spinningglobe.gif" alt="GDELT" style="width: 55%" ></center>
<div><center><font size=".5"><b>Image: GDELT monitors world wide news and is a lens into human society.</b> </font></center></div>
</div>
<br>
### What is GDELT?
GDELT is a service that monitors print, broadcast, and web news media in over 100 languages from nearly all countries in the world. Enabled by this constant stream of news data,  GDELT can monitor breaking news events anywhere on the planet.  GDELT data can identify news providers who have a history of generating original content earliest for breaking issues in certain parts of the world.  Conversely, GDELT data can also find news providers who specialize in redisseminating another provider's content with a focus on exposing more substantive news to wider audiences at the cost of speed.  And finally, GDELT makes building news timelines a simple job as we will see in this post. All information about an event is presented chronologically.  

### GDELT's Coding System: CAMEO Codes
The CAMEO code is the center of GDELT data analysis.  CAMEO, which stands for <a href="https://en.wikipedia.org/wiki/Conflict_and_Mediation_Event_Observations" target="_blank">Conflict and Mediation Event Observations</a>, is a framework for coding event data to support the study of political and violent events.  Each GDELT record has a CAMEO code that is a pivot point to filter and categorize news content.  Combining CAMEO code filtering with GDELT's geo-inferencing service, we can build pipelines that monitor news at the city level  (or state or country or continent) on topics across the globe.  The [coding system is pretty extensive](http://data.gdeltproject.org/documentation/CAMEO.Manual.1.1b3.pdf) with codes for diplomatic, military, societal, criminal, and economic events.  For example, to track all news on mass killings in Kigali, Rwanda, we only need to filter on CAMEO code '202' and the [geonames feature identifier for Kigali,  '-2181358' ](http://www.geonames.org/) .  

For all of GDELT's strengths, it would be intellectually dishonest for me to ignore the reported weaknesses.  To see what others have identified as strengths and weaknesses, see [M.D. Ward et al's **Comparing GDELT and ICEWS Event Data**](https://www.researchgate.net/publication/303211430_Comparing_GDELT_and_ICEWS_event_data). One oft cited weakness is duplicates; we'll introduce a quick fix to reduce duplicates when analyzing a specific CAMEO event code. 

<hr>
### A Killer Neutralized... 
<p style="font-family:courier;"><i>At least six officers searched Mandalay Bay hotel floor by floor before they found Paddock's room within hours of the shooting.  Paddock, a 64-year old resident of a Mesquite, Nevada retirement community, had apparently rented two rooms in the hotel four days before the massacre on September 28. He reportedly fired at the officers through the door before Las Vegas Metropolitan Police Department (LVMPD) SWAT used explosives to breach room 32135.  Inside, they found Paddock dead from a self-inflicted gunshot.  <br><br>

The barrage from the 32nd floor lasted several minutes but the damage was extensive.  Initially, the number of fatalities had climbed to 20. Two hours later, the number had pushed past 50, making it the deadliest active shooter event in recent history. At least two off-duty police officers were shot and killed. Two other police officers were injured, one of them critically. Over 500 people were wounded.</i></p>

<br>
<div class="image">
<center><img src="{{ site.url }}/assets/img/girlnearambulance.jpg" alt="Girl in cowboy boots near ambulance" ></center>
<div><center><font size=".5"><b>Image: A woman sits on the curb at the scene of the Las Vegas shooting. <br><i>Source: John Locher/AP Photo</i></b> </font></center></div>
<br>
</div>
 

<p style="font-family:courier;"><i>Tales of heroism and compassion emerged quickly: Couples held hands as they ran through the dirt lot. Some of the bleeding were carried out by fellow concertgoers. While dozens of ambulances took away the wounded, some people loaded victims into their cars and drove them to the hospital. At least 104 patients were treated at the University Medical Center.  Some of the youngest patients treated at the hospital were 16 and 17 years old. </i></p>

<br><br>
<div class="image">
<center><img src="{{ site.url }}/assets/img/carryWounded.jpg" alt="Carrying wounded girl`" ></center>
<div><center><font size=".5"><b>Image: People assist a wounded woman at the scene of the Las Vegas shooting <br><i>Source: Chase Stevens/Las Vegas Review - Journal via AP</i></b> </font></center></div>
<br><br>
</div>

<p style="font-family:courier;"><i>Those who survived physically unscathed did what they could to escape.  People fleeing the concert grounds hitched rides with strangers, piling into cars and trucks. <br><br>

With the shooter neutralized, responders tended to victims and the world searched for an answer to the most difficult question.  Why?  Why did he do it? A part of that answer would likely come from an answer to another question. Who was Stephen Paddock? </i></p><br><br>

<hr>
<br><br>
## Pythonic Access to Worldwide GeoReferenced News

[`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR) is a minimalist Python API for GDELT. For more information, <a href="https://github.com/linwoodc3/gdeltPyR/blob/master/examples/gdeltPyR_basic_use.md#installation" target= "_blank">visit the github project page</a>.  To install:

```bash
pip install gdelt
```
`gdeltPyR` is an ideal tool to explore news events with information that evolves over time.  Because of its global focus, analysis would show how a news story spreads across global providers. Resources like the <a href="https://en.wikipedia.org/wiki/Portal:Current_events" target="_blank">Wikipedia Current Events page</a> has good examples of the type of stories that work well with `gdeltPyR`.  Examples include:
* <a href="https://en.wikipedia.org/wiki/2017_Manchester_Arena_bombing" target="_blank">Manchester Arena bombing</a>
* <a href="https://en.wikipedia.org/wiki/Proclamation_No._216" target="_blank">The Marawi crisis in the Philippines</a>

`gdeltPyR` only requires a date; if news providers are reporting on the topic it will almost certainly end up in the GDELT feed, making it accessible in our Python API.  In the future, `gdeltPyR` will leverage Google's BigQuery to query georeferenced news event data for specific actors. Additionally, I will be adding a feature to query by specific Local Time or UTC time.  

The Las Vegas shooting occurred on October 1, 2017 at 20:08 PDT.  GDELT uses UTC datetimes, so this event has a 7 hour difference in GDELT, putting our target timeframe in the early hours of October 2. 

Let's set up the module and libraries:

```python
##############################
# Standard Library
##############################

import datetime
import re

#############################
# Third-party libraries
#############################

from tzwhere import tzwhere 
import pandas as pd
import numpy as np
import pytz

#############################
# Local modules
#############################

import gdelt
```

The `tzwhere` library can identify the timezone offset using a latitude and longitude pair, so we import this tool for time series functionality later on.  

```python
# tzwhere variable for time normalization
tz1 = tzwhere.tzwhere(forceTZ=True)

# instantiate the gdeltPyR object for searches
gd = gdelt.gdelt()
```
<br><br>
<hr>
<br><br>
### Who was Stephen Paddock?<br>
<p style="font-family:courier;"><i>The search to understand Paddock started in the room where he died.  Police recovered 23 guns (some with scopes) from his room where hotel workers, who were in and out of the room over several days, said they “saw nothing at all” hinting at the forthcoming rampage. At least two of the guns were modified with <a href="https://en.wikipedia.org/wiki/Bump_fire" target = "_blank">bump-stock devices</a> which can be attached to the stocks of semiautomatic guns to allow fully automatic gunfire. The arsenal suggested Paddock was intent on killing as many people as possible but provided little insight  as  to "why" he did it.  His death meant investigators would be on a scavenger hunt to discover a motive.</i></p><br><br>

<div class="image">
<center><img src="{{ site.url }}/assets/img/paddockFace.jpg" alt="Stephen Paddock" ></center>
<div><center><font size=".5"><b>Image: Stephen Paddock, the gunmen in the Las Vegas massacre</b> </font></center></div>
<br>
</div>


<p style="font-family:courier;"><i>Within hours of the shooting, officers executed a search warrant at Paddock's three-year-old, 396,000 US dollar two-bedroom home in the tiny desert community of Mesquite, 80 miles north-east of Las Vegas.  They found 19 additional guns, thousands of rounds of ammunition, and explosives. Law enforcement also discovered several pounds of ammonium nitrate in his car, a fertilizer that can be turned into explosives. </i></p><br>

<div class="image">
<center><img src="{{ site.url }}/assets/img/paddockHome.jpg" alt="Stephen Paddock home" ></center>
<div><center><font size=".5"><b>Image: Stephen Paddock's home in Mesquite, NV. </b> </font></center></div>
<br>
</div>
<div><p style="font-family:courier;"><i>
He had a live-in girlfriend, 62-year old Marilou Danley, who was traveling in the Philippines when the massacre took place.  Although Paddock used some of her identification, investigators clarified that they believed she was not involved with the shooting. He was divorced 27 years ago and his ex-wife, now living in Los Angeles County, California, had no contact with him for years.  There was no record of children. <br><br>

Police said they had no information about Paddock’s motive, that he had no criminal record and was not believed to be connected to any militant group. “We have no idea what his belief system was,” Lombardo said. “I can’t get into the mind of a psychopath.”<br><br>

All firearms may have been purchased legally. A Mesquite store, Guns & Guitars, said it sold a gun to Paddock and that “he never gave any indication or reason to believe he was unstable or unfit at any time.”  He had purchased multiple firearms in the past, several of them purchased in California, according to law enforcement officials. But those didn't appear to be among the 10 or more guns found in the Mandalay Bay hotel room.<br><br>

He had a pilots license, but the medical certification required to fly legally had lapsed.  Nothing about Paddock seemed out of place or out of the ordinary. <br><br> 

Police said they had no information about Paddock’s motive, that he had no criminal record and was not believed to be connected to any militant group. “We have no idea what his belief system was,” Lombardo said. “I can’t get into the mind of a psychopath.” <br><br>

Perhaps a look into his family history or discussions with other family members would provide clues.
 </i></p>
</div>

<hr>
<br><br>
## Using [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR)
`gdeltPyR` is simple to use. As stated earlier, we only need a date and information about the location to find the target data. After we filter, it's just a "point, click, read" job because the news stories will be categorized and organized by time.  

The code to pull data for October 1 through October 2:

```python
# code to use gdeltPyR; pulling all of 1-2 Oct data (coverage = True) 
# and normalizing column names to SQL friendly format (normcols=True)

vegas = gd.Search(
                  date=['2017 Oct 1','2017 Oct 2'],
                  coverage=True,
                  normcols=True
                  )
```

Depending on your internet connection, this could take several to tens of seconds to download.  It takes seconds to pull down a full day depending on your machine (my stats: 2 days full coverage, 29 seconds, 263,707 row by 62 column dataframe that is 569.5 MB). The time to download data will be drastically reduced <a href="https://github.com/linwoodc3/gdeltPyR/issues/24" target="_blank">when `gdeltPyR` includes a direct connection to Google BigQuery.</a>  GDELT also ships data out in 15 minute intervals; if you set the `coverage` parameter to `False`, it takes 1-2 seconds to return a 2000-3000 row by 62 column dataframe. 

The dataframe has a row for each record and each record corresponds to a news article.  Because the GDELT `events` table revolves around the CAMEO code, one article can have multiple entries with a different CAMEO code.  To see the full details on the columns see the <a href="https://github.com/linwoodc3/gdelt2HeaderRows/blob/master/schema_csvs/GDELT_2.0_Events_Column_Labels_Header_Row_Sep2016.csv" target="_blank">schema descriptions here.</a> The most relevant columns for this post are described in the table below:

| Column Name  |  Description |
|---|---|
| **ActionGeo_Lat**  | field providing the centroid latitude of the landmark for mapping.  |
| **ActionGeo_Long**  | field providing the centroid longitude of the landmark for mapping.  |
| **ActionGeo_FeatureID**  | field specifies the GNS or GNIS FeatureID for this location.  |
|  **ActionGeo_Type** |  field specifies the geographic resolution of the match type and holds one of the following values: 1=COUNTRY (match was at the country level), 2=USSTATE (match was to a US state), 3=USCITY (match was to a US city or landmark), 4=WORLDCITY (match was to a city or landmark outside the US), 5=WORLDSTATE (match was to an Administrative Division 1 outside the US – roughly equivalent to a US state). This can be used to filter events by geographic specificity, for example, extracting only those events with a landmark-level geographic resolution for mapping. |
| **EventCode**   | This is the raw CAMEO action code describing the action that Actor1 performed upon Actor2.  |
| **EventRootCode**  |  This defines the root-level category the CAMEO event code falls under. For example, code “0251” (“Appeal for easing of administrative sanctions”) has a root code of “02” (“Appeal”). This makes it possible to aggregate events at various resolutions of specificity. For events at levels two or one, this field will be set to EventCode. |
| **DATEADDED**  | field provides the date the event was added to the master database in YYYYMMDDHHMMSS format in the UTC timezone. For those needing to access events at 15 minute resolution, this is the field that should be used in queries.  |
|  **SOURCEURL** | This field records the URL or citation of the first news report it found this event in. In most cases this is the first report it saw the article in, but due to the timing and flow of news reports through the processing pipeline, this may not always be the very first report, but is at least in the first few reports.

>**Note:**`gdeltPyR` can normalize columns names into <a href="https://www.loc.gov/preservation/digital/formats/fdd/fdd000280.shtml" target="_blank">ESRI shapefile friendly strings</a> when the `normcol` parameter is set to `True`.  So, `ActionGeo_Lat` would become `actiongeolat` 


Each record in the <a href="https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe" target="_blank">dataframe</a> is a news report in time so we can treat this as a time series.  Moreover, GDELT returns data in equally spaced intervals of time which works well for <a href="https://en.wikipedia.org/wiki/Time_series" target="_blank">time series analysis</a>.<br><br>

Next we use create and use custom functions to make timezone aware datetime columns that can be used to index our data in time (e.g. transform UTC to local Pacific Daylight Time using the lat/lon).  The new functions and code follow.

```python
def striptimen(x):
    """Strip time from numpy array or list of dates that are integers
    
    Parameters
    ----------
    x : float or int
        GDELT date in YYYYMMDDHHmmSS format; sometimes it's a
        float others it's an int
    
    Returns
    ------
    
    datetime obj : obj
        Returns a naive python datetime object.
    """
    date = str(int(x))
    n = np.datetime64("{}-{}-{}T{}:{}:{}".format(
    date[:4],date[4:6],date[6:8],date[8:10],date[10:12],date[12:])
    )
    return n

def timeget(x):
    '''convert to datetime object with UTC time tag
    
    Parameters
    ----------
    x : tuple
        Tuple containing ordered value of latitude, longitude, 
        and a datetime object
    
    Returns
    ------
    
    datetime obj : obj
        Returns a time aware python datetime object.
    '''
    
    try:
        now_aware = pytz.utc.localize(x[2].to_pydatetime())
    except:
        pass
    
    # get the timezone string representation using lat/lon pair
    try:
        timezone_str=tz1.tzNameAt(x[0],x[1],forceTZ=True)
        
            # get the time offset
        timezone = pytz.timezone(timezone_str)

        # convert UTC to calculated local time
        aware = now_aware.astimezone(timezone)
        return aware
    
    except Exception as e:
        pass

# vectorize our function
vect = np.vectorize(striptimen)


# use custom functions to build time enabled columns of dates and zone
vegastimed = (vegas.assign(
                dates=vect(vegas.dateadded.values)).assign(
                zone=list(timeget(k) for k in vegas.assign(
                dates=vect(vegas.dateadded.values))\
                 [['actiongeolat','actiongeolong','dates']].values)))
```

The code above created two time-enabled columns; `dates` and `zone` using a chained <a href="https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.assign.html" target="_blank">`pandas.DataFrame.assign` operation</a>.  Both columns are `datetime64[ns]` data types, which means they can be used for <a href="https://pandas.pydata.org/pandas-docs/stable/timeseries.html" target="_blank">time series functionality in pandas</a>. The `zone` column is a timezone aware data type, which adds the timezone offset to `UTC` time. <br><br>

Next, we filter the data to records about the Las Vegas shooting using a combination of:
*  <a href ="http://data.gdeltproject.org/documentation/CAMEO.Manual.1.1b3.pdf" target="_blank">CAMEO event root codes</a> of 18, 19, and 20 which stand for **assault**, **fight**, and **engage in unconventional mass violence** respectively.  See the <a href ="http://data.gdeltproject.org/documentation/CAMEO.Manual.1.1b3.pdf" target="_blank">CAMEO code reference for details on CAMEO event codes.</a>  For a higher level of aggregation, consider using the `QuadClass` field as a filter for the GDELT results. 
*  Search for GNIS feature ID representing Las Vegas,**847388**, in the `actiongeofeatureid` field <br><br>
>**Note** To get more accurate results, use the <a href="https://geonames.usgs.gov/apex/f?p=138:1:0::NO:::" target="_blank">GNIS Feature ID</a> for your location filter as opposed to the string representing the location name because some news reports can spell place names differently. A trick to find the feature ID without searching the GeoNames website is to run a `gdeltPyR` query, find a relevant entry, copy the feature ID value, and filter the data using your new value.  The feature ID for Las Vegas is **847388**. When the `ActionGeo_Type` field is 3 or 4, understand the feature ID could also be specific and reference a landmark inside a city (stadium, park, building, etc.)

To get help on the fields, refer to reference the <a href="https://github.com/linwoodc3/gdelt2HeaderRows/blob/master/schema_csvs/GDELT_2.0_Events_Column_Labels_Header_Row_Sep2016.csv" target="_blank">headers information file.</a> Finally, we use a <a href="https://pandas.pydata.org/pandas-docs/stable/indexing.html" target="_blank">chained pandas indexing functionality</a> to filter our data in the code block below.

```python
# filter to data in Las Vegas and about violence/fighting/mass murder only
vegastimedfil=(vegastimed[
                        ((vegas.eventrootcode=='19') | 
                        (vegas.eventrootcode=='20') | 
                        (vegas.eventrootcode=='18')) & 
                         (vegas.actiongeofeatureid=='847388')])\
                                    .drop_duplicates('sourceurl') 
print(vegastimedfil.shape)
---------------------
Out: (689, 64)

```

We drastically reduced our data set (from 200,000+ to ~700).  The next step is building the urls to chronologically ordered news stories. For this post, I manually read stories to extract facts.  However, you could leverage information extraction tools combined with entitiy extractors to build a knowledge base for events of interest.  That would be a higher level of analysis.  To build the list of articles, see the code below.    

```python
# build the chronological news stories and show the first few rows
print(vegastimedfil.set_index('zone')[['dates','sourceurl']].head())
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>dates</th>
      <th>sourceurl</th>
    </tr>
    <tr>
      <th>zone</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-10-01 19:00:00-07:00</th>
      <td>2017-10-02 02:00:00</td>
      <td>http://www.lasvegasnow.com/news/update-child-f...</td>
    </tr>
    <tr>
      <th>2017-10-01 20:00:00-07:00</th>
      <td>2017-10-02 03:00:00</td>
      <td>https://www.reviewjournal.com/traffic/las-vega...</td>
    </tr>
    <tr>
      <th>2017-10-01 23:15:00-07:00</th>
      <td>2017-10-02 06:15:00</td>
      <td>http://www.dw.com/en/las-vegas-police-active-s...</td>
    </tr>
    <tr>
      <th>2017-10-01 23:30:00-07:00</th>
      <td>2017-10-02 06:30:00</td>
      <td>http://www.goldcoastbulletin.com.au/news/world...</td>
    </tr>
    <tr>
      <th>2017-10-01 23:30:00-07:00</th>
      <td>2017-10-02 06:30:00</td>
      <td>http://www.sanluisobispo.com/news/nation-world...</td>
    </tr>
  </tbody>
</table>
<br><br>

To build a narrative, I simply read articles chronologically to see how the story unfolded in time. You can look at the url string to skip irrelevant articles (first 6) or use time series analysis to trigger relevant time frames (disucssed later).  Once you have the list of the urls, stay alert. News providers will update information but use the same url but you still get an idea for the news providers who get stories out fast.  GDELT preserves this aspect.  However it's important to be aware of <a href="https://en.wikipedia.org/wiki/Participation_bias" target="_blank">participation or non-response bias</a>.  There may be a news provider who did not have its data processed by GDELT, leading to  faulty conclusion that one particular news provider is faster than another.  Be wary of data limitations.<br><br>

If you wanted to time enable the entire 200,000+ row data set for time series analysis, it's relatively simple because `gdeltPyR` returns the data in a <a href="https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe" target="_blank">pandas dataframe.</a>  First you localize the entire dataset to UTC time and then convert it to any timezone using the <a href="http://pytz.sourceforge.net/" target="_blank">Python timezone string of your choice</a>. 

```python
# example of converting to Los Angeles time. 
vegastimed.set_index(
    vegastimed.dates.astype('datetime64[ns]')
                    ).tz_localize(
                                'UTC'
                                ).tz_convert(
                                            'America/Los_Angeles'
                                            )
                                            
# get timezone string using pytz 
```
<br><br>
Alternatively, you could use the the <a href="https://gist.github.com/linwoodc3/5c915fb6d9097e7e27d5b0bc1f047ba2" target = "_blank">`tzwhere` library with latitude and longitude</a> to find the timezone string for each GDELT record and append the time zone this way.  Warning! It is computationally expensive to run this timezone analysis over the entire dataset.
<hr>
<br><br>
### President Duterte Declares Martial Law
<div><p style="font-family:courier;"><i>
By 1045 pm PHT, President Rodrigo Duterte <a href ="https://en.wikipedia.org/wiki/Proclamation_No._216">declared 60 days of martial law in Marawi</a>.  He made the announcement while on official visit to Russia, and even shifted meetings with Russian officials to make an early return to the Philippines to deal with the rising crisis. <br><br>Just ten hours after the start of clashes, the operation was far from complete. Two soldiers from the 103rd Brigade and one policeman had been killed and at least 12 other government personnel were injured during the battle. There were no reports of casualties on the other side.  And if that wasn't enough, the entire city was locked down.  Duterte's martial law applied to the whole island of Mindanao. </i></p> 

<div class="image">
<center><img src="{{ site.url }}/assets/img/Duterte.jpeg" alt="Duterte" ></center>
<div><center><font size=".5"><b>Image: Duterte declares martial law while on official travel in Russia.</b> </font></center></div>
<br>
</div>


<div><p style="font-family:courier;"><i>The city had suffered its share of damage as well.  The Maute Group had burned a church, the Marawi City Jail, the Ninoy Aquino School and the Dansalan Junior College. Moreover,  Maute fighters had occupied the main street of Marawi city, Amai Pakpak Medical Center, City Hall, the city jail, and two bridges.</i></p>  
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">PHILIPPINES: Some houses being set on fire by <a href="https://twitter.com/hashtag/ISIS?src=hash">#ISIS</a> . People don&#39;t know where to go. They are stuck in <a href="https://twitter.com/hashtag/Marawi?src=hash">#Marawi</a>. <a href="https://t.co/5ZuOs8Gpec">pic.twitter.com/5ZuOs8Gpec</a></p>&mdash; Wcn Conflict News (@NewsWcn) <a href="https://twitter.com/NewsWcn/status/867012164275638276">May 23, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
<div><p style="font-family:courier;"><i><br><br>Somehow, a raid on 15 gunmen turned into a city-wide conflict with an estimated 100 gunmen divided into groups of 10 in different locations.  This was the start of a long running conflict.<br><br>This was only the first 10-12 hours.</i></p>

</div>
</div>
</div>

<hr>
<br><br>
## Mission Accomplished: Use [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR) and GDELT

That closes out our brief introduction to [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR) and our story. To summarize, we pulled a chronologically ordered list of URLs to news stories on the Marawi crisis.  After we pulled the data from GDELT, we used the geonames featureid and the CAMEO code to filter down to the relevant data; the filter got us from 200,000+ total GDELT reports to 206 reports dealing with Marawi and violence.  Of those 206 urls, 79 were unique and pointed to different news stories, ordered by time (**change the CAMEO code and feature id to explore issues in other parts of the world**).  To build the final timeline, you only needed to read the stories and write coherently.  I want to point out, the CAMEO system extacts a lot more information that is coded into GDELT. There are over 60 columns of data in GDELT, and each column provides unique value.  We only used four (4) columns in this post (Date Added, Event Root Code, Action Geo FeatureID and Source Url).     


In building [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR) (which I hope you will use or help me develop!), I focused on abstracting the details of the API calls away from the user. And, I added a little multiprocessing juice in there as well to make full use of all available cores! For those who run into feature ID problems, there's an easy way to build your own lookup table of feature ids.  Just pull a few days of GDELT data using [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR), isolate unique feature ids, and create a second column that holds the different names tied to the same feature id.  Pretty soon, you'll have the id and name for most cities, provinces/states, and countries.

Now, go forth and use [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR) or, learn more about [GDELT](http://www.gdeltproject.org/) in general. 

I need to give you a warning on data consumption; GDELT is MASSIVE.  I will eventually write a function in `gdeltPyR` to query GDELT data using Google BigQuery ([already wrote the prototype](https://github.com/linwoodc3/gdeltPyR/issues/24)), but I need to warn you of something first. If you do a query with [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR) covering a few weeks, you may run out of memory.  By default, [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR) stores the data in RAM (because [it's a `pandas` dataframe](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)).  If one full day of reporting is nearly 500 MBs in size, you can see how memory becomes a real problem as you cover more time.  For memory constrained workflows, create a pipeline that reads the data in, writes to disc, and flushes RAM before going to the next day.  

Now, the fun part for you.  We could have done MUCH MORE with this data.  Some ideas include:
- Implement web scraping on each data source to extract the content; then compute element wise Levenshtein distance (LD) or semantic similarity; result - determine which documents have most original content
- Extend analytic above by adding news provider and time component to find news providers who provide most original content faster
- Do everything above, but try to use the resulting corpus for text summarization
- New organizations could use this data to ensure they are adding original content when they publish!
- Can you think of more?!?!? 

### The Obigatory Graphic:  See the Time Series Potential of GDELT
The Walkoff:  Every post needs a graphic.  Below, you'll see a simple time series graphic that charts the magnitude of our target CAMEO code and feature id (normalized by total hour count) through time. We see an obvious uptick in activity later in the day, led by a complete lack of activity. 0900 UTC is about 1700 PHT; we were getting automatic extractions within a few hours of an event happening in a remote village in the Phillipines! We don't cover it, but GDELT extactions assign responsibility to groups (**ABU SAYYAF** automatically extracted), organizations (**GOVERNMENT TROOPS AND POLICE** automatically extracted) and places (**HOSPITAL** automatically extracted in addition to city/state names).

I welcome your thoughts/comments/corrections. My basicaly thought is, since we have a geoname entry for nearly every city on the planet, we can run this analytic ad finitum on each CAMEO code and each feature id; the only limitations are compute power and storage. Now, the graphic (using my Economist matplotlib style):

```python
import matplotlib.pyplot as plt
import matplotlib as mpl

# set style
mpl.style.use('economist')

# resample to hourly interval for all events and marawi events
timeseries= pd.concat([marawi.resample('H')['sourceurl'].count(),muate2.resample('H')['sourceurl'].count()]
         ,axis=1)

# file empty event counts with zero
timeseries.fillna(0,inplace=True)

# rename columns
timeseries.columns = ['Total Events','Marawi Violent Events Only']

# combine
timeseries = timeseries.assign(Normalized=(timeseries['Marawi Violent Events Only']/timeseries['Total Events'])*100)

# make the plot
f,ax = plt.subplots(figsize=(13,7))
ax = timeseries.Normalized.ewm(adjust=True,ignore_na=True,min_periods=5,span=12).mean().plot(color="#C10534",label='Exponentially Weighted Count')
ax.set_title('Hourly Count of Violent Events in Marawi',fontsize=28)
for label in ax.get_xticklabels():
      label.set_fontsize(16)
ax.set_xlabel('Hour of the Day', fontsize=20)
ax.set_ylabel('Percentage of Hourly Total',fontsize='15')
ax.legend()
plt.tight_layout()
plt.show()

```

<div class="image">
<center><img src="{{ site.url }}/assets/img/countGraphic.png" alt="Count" ></center>
<div><center><font size=".5"><b>Image: Simple analytic of normalizing count of event type in geographic regioin</b> </font></center></div>
<br>
</div>



[^1]:  ["MAPPING THE FUTURE OF MANKIND USING HISTORICAL DATASETS"](http://dataconomy.com/2014/09/mapping-the-future-of-mankind-using-historical-datasets/)

[^2]: [Global Database of Events, Language, and Tone (GDELT)](http://www.gdeltproject.org/)
<hr>
<br>
# The Data Science Detour

This section is for you.  Yes. You, the person still reading through the end to the code.  I have a challenge for you, if you are interested.

First, let's cover some basic analysis of the data we already have.  Assume we want to answer this question:

*  Which news source provided the most original content on this topic?


It may seem simple but this can be tricky to deal with as you understand the strengths and weaknesses of [GDELT](http://www.gdeltproject.org/).  [GDELT](http://www.gdeltproject.org/), in my opinion, values sensitivity over specificity.  As a result, you will rarely miss an event but you will almost certainly deal with a good number of false positives.  In this specific case, URLS to news sources repeat in our down sampled data set.  Moreover, we need to strip the unique news provider from the URL and not just use URLs themselves.  I wrote some regex to accomplish both.

```python
######################
# Third party libraries
######################

from bs4 import BeautifulSoup
```

### Who Produced the Most?

With the analytic power of Python `pandas` and regex, we can identify the news source with the highest original production (unique urls).  Let's strip out the providers first:

```python
# regex to strip a url from a string; should work on any url (let me know if it doesn't)
s = re.compile('(http://|https://)([A-Za-z0-9_\.-]+)')

# use dataframe from earlier
frame = maute2

# remove duplicate urls; only keep unique urls
frame = frame.drop_duplicates(['sourceurl'])

# apply regex to each url; strip provider; assign as new column
frame=frame.assign(provider=frame.sourceurl.\
      apply(lambda x: s.search(x).group() if s.search(x) else np.nan))

# group by provider and return a count
groups = frame.groupby(['provider']).size().sort_values(ascending=False).reset_index()

# print the results
print(groups)
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>provider</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>http://www.philstar.com</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>http://news.abs-cbn.com</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>http://cnnphilippines.com</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>http://www.interaksyon.com</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>http://www.gmanetwork.com</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

Easy.  We know `http://www.philstar.com` and `http://news.abs-cbn.com` produced the most stories on the topic in the first few hours. To see how many unique websites wrote news stories on the Marawi crisis, according to [GDELT](http://www.gdeltproject.org/), just run `groups['provider'].unique().shape`; the answer is `55`.  

### Who Produced the Fastest?

What if we wanted to answer, **"Which website produced news stories "faster" on average?"** The first task is transforming our time into something that can be averaged.  If you're thinking [`epoch` time](https://en.wikipedia.org/wiki/Unix_time), that's where I decided to go as well. After the conversion, Python `pandas` functionality gets us to the result we need.

We copy our data again and convert each date to an epoch timestamp.

```python
# subset the data again to include only unique urls
frame2 = frame.copy()[frame.provider.notnull()==True]\
.drop_duplicates('sourceurl')[['provider','sourceurl','dates']]

# convert each date to epoch timestamp
frame2 = frame2.assign(dates=frame2['dates']\
.apply(lambda x: (x.to_pydatetime().timestamp())))

```


Awesome!  Next up, we're going to [use `pandas` to perform some advanced transformations on our data](https://pandas.pydata.org/pandas-docs/stable/groupby.html).  To `pandas` users, this is routine  work but if you are new this library, it can seem like a foreign language.  But, I advise you to learn `pandas`. What other library has this type of functionality?  To ground your understanding for this next block of code, keep `SQL` logic and syntax in mind. We will implement the following logic:

*  Group data by news source
*  Filter data and only keep sources that provided 3 or more original news stories
*  Compute summary statistics (mean, max, min) over our epoch timestamps for each provider
*  Convert epoch time to human readable datetime
*  Sort the final results; provider with earliest average listed first
*  Localize the time to UTC
*  Convert the time from UTC to Philippines time
*  Rename columns
*  Rename index

The end result is, we should see which news source, on average, produced faster on this topic. `pandas` compacts all this logic into a few lines of code:

```python
# group data by news source and keep sources with 3 or more stories
grp = frame2.groupby('provider')\
.filter(lambda x: len(x)>=3).groupby('provider')

# compute summary stats on epoch timestamp; sort by mean
final = grp.agg([np.mean,np.max,np.min]).sortlevel('mean',ascending=False)

# convert epoch to datetime in multiindex dataframe; set index to UTC
newfinal = pd.DataFrame(final['dates']['mean']\
.apply(lambda x:datetime.datetime.fromtimestamp(int(x)))\
.sort_values(ascending=True)).reset_index().set_index('mean',drop=False)

# make datetime timezone aware
newfinal = newfinal.tz_localize('UTC')

# convert timezone to Philippines
newfinal = newfinal.tz_convert('Asia/Manila')

# Rename columns
newfinal.columns = ['provider','UTC Time']

# rename index
newfinal.index.name='Philippines Time'

# print results
print(newfinal)
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>provider</th>
      <th>UTC Time</th>
    </tr>
    <tr>
      <th>Philippines Time</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-05-23 22:45:00+08:00</th>
      <td>http://www.philstar.com</td>
      <td>2017-05-23 14:45:00</td>
    </tr>
    <tr>
      <th>2017-05-23 23:45:00+08:00</th>
      <td>http://cnnphilippines.com</td>
      <td>2017-05-23 15:45:00</td>
    </tr>
    <tr>
      <th>2017-05-24 01:10:00+08:00</th>
      <td>http://www.gmanetwork.com</td>
      <td>2017-05-23 17:10:00</td>
    </tr>
    <tr>
      <th>2017-05-24 01:39:00+08:00</th>
      <td>http://news.abs-cbn.com</td>
      <td>2017-05-23 17:39:00</td>
    </tr>
    <tr>
      <th>2017-05-24 03:20:00+08:00</th>
      <td>http://www.interaksyon.com</td>
      <td>2017-05-23 19:20:00</td>
    </tr>
  </tbody>
</table>
<br>It looks like `http://www.philstar.com` produced the "fastest" overall!

# The Challenge
### Who Produces the Most Semantically Dissimilar Content?

Now here is the challenge.  Don't worry; I will provide a little help to get you started (or maybe you don't need it). This question is a little difficult:
* Which provider produces more semantically dissimilar content? 

In other words, who avoids repeating the same information in different articles (with unique URLs)? Consider calculating a measure for each provider and a measure across the different providers.  We expect to see SOME similarity because the news stories are talking about the same event. While reading these articles, I saw a lot of flat out "copies" or redisseminated news (this is legal, and was often an Associated Press article). With that said, we can use this *dissimilar* calculation to find out which providers are "copiers" and which providers do more "original" reporting.  You could also add a time component into this. **If you don't need any help, stop reading here and try your solution.**

>  **Pity Party Pitstop:** One complaint I've seen about [GDELT](http://www.gdeltproject.org/) is, "Kalev H. Leetaru ([GDELT](http://www.gdeltproject.org/)'s creator) doesn't provide the content!"  To those folks, I say, **"Get it yourself; it's not that hard.**  I wrote this code below in 20 minutes and tested on [GDELT](http://www.gdeltproject.org/) urls.  Some content comes back; some doesn't. And another complaint involves duplicates.  Well, in this post, I gave you code to remove duplicates and isolate unique data providers and unique URLs.  If you know how to work with data, GDELT is a valuable tool.  If you are looking for the perfect data stream with zero interaction required on your part, I'll just say, "Me too!"  

The code below works surprisingly well to pull content from A LOT of news websites.  It will work on news provider websites outside our Maute dataset, so feel free to reuse for other experiments. **Warning**.  Some websites have removed the content so you'll return an empty string.  Other websites may be blocked (every country's internet doesn't play well with others).  And, some websites use different tags for their HTML ([help me add try/except clauses using this Github Gist; let's work together!](https://gist.github.com/linwoodc3/e12a7fbebfa755e897697165875f8fdb)).  I did my best to return a message with a hint on why a URL doesn't return content. Here is the code: 


{% gist linwoodc3/e12a7fbebfa755e897697165875f8fdb %} 

Just to be sure, I'll also provide an example on how to run the function. [I (and people smarter than me) advise moving outside of the dataframe and parallelizing this function call](https://tomaugspurger.github.io/modern-4-performance.html).  I use [`concurrent futures` for this task in favor of the library's simplicity](https://github.com/pydata/parallel-tutorial/blob/master/notebooks/01-map.ipynb).

```python
from concurrent.futures import ProcessPoolExecutor

# set up the multiprocessing mapper
e = ProcessPoolExecutor()

# get unique urls
urls = frame2['sourceurl'].unique()

# run the parallel job; 
#  takes 26 seconds on my 4 core machine; 78 news articles; 
# more cores and better network speed this up
done={}
results = np.array(list(e.map(textgetter,urls)))
```

The next step is merging the content back into our `maute2` dataframe.  Then, we will have all the [GDELT](http://www.gdeltproject.org/) data needed for the challenge.  For those folks who want to perform `third-party` verification of [GDELT](http://www.gdeltproject.org/) modeling, this code gets everything you need to perform it (run this on an entire day; but you ip will probably get blocked by news providers).  You can apply different named entity extractor, sentiment, geo-inferencing,open information, and/or knowledge base models to the content.  Then, compare your results to the output of [GDELT](http://www.gdeltproject.org/).  Here is the code to merge data:

```python
# just a holder
sers = []

# loop over results and build row for each record
for l in results:
    ul = list(l.keys())[0]
    content = l[ul]
    sers.append(pd.Series({'url':ul,'content':content}))
# create new dataframe with url and content
connie = pd.concat(sers,axis=1).T


# merge all data back together
maute2.merge(connie,left_on='sourceurl',right_on='url')
```

You have all the data to complete the challenge! Thanks for reading! I'm curious to see how you tackle this problem.  Please share!
