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
excerpt: It all started a few minutes after 10 pm on October 1st.<br><br> The gunshots sounded like firecrackers at first.  People in the crowd didn't understand what was happening when the band stopped playing and Jason Aldean hustled off stage.<br><br>"That's gunshots," a man said on a cellphone video in the nearly half-minute of silence and confusion that followed. Then the pop-pop-pop noise resumed. And pure terror set in.

---


<div class="image">
<center><img src="{{ site.url }}/assets/img/concertOverview.jpg" alt="City entranc" ></center>
<div><center><font size=".5"><b>Image: The grounds at the Route 91 Harvest festival on Las Vegas Boulevard South in Las Vegas on Saturday, Sept. 30, 2017. <a href="https://en.wikipedia.org/wiki/Mandalay_Bay" target="_blank"> Mandalay Bay Hotel and Casino</a> can be seen in the background behind the stage. <br><i>Source: http://news3lv.com/, file</i></b> </font></center></div>
<br>
</div>
<body>
<p style="font-family:courier;"><i>It all started a few minutes after 10 pm on October 1st.<br><br>

The gunshots sounded like firecrackers at first.  People in the crowd didn't understand what was happening when the band stopped playing and <a href="https://www.google.com.kh/search?q=Jason+Aldean&rlz=1C5CHFA_enUS751US751&source=lnms&sa=X&ved=0ahUKEwjj-aDZsfHWAhVDjLwKHTRjC_UQ_AUICSgA&biw=1280&bih=682&dpr=1" target="_blank">Jason Aldean</a> hustled off stage.<br><br>  

"That's gunshots," a man said on a cellphone video in the nearly half-minute of silence and confusion that followed. Then the pop-pop-pop noise resumed. And pure terror set in.<br><br>


For reasons that remain unknown,  <a href="https://en.wikipedia.org/wiki/Stephen_Paddock" target="_blank">Stephen Paddock, a 64-year old white male, </a>fired on a crowd of 22,000 for 10 minutes unhindered in 40- to 50-round bursts from his 32nd floor room of the <a href="https://en.wikipedia.org/wiki/Mandalay_Bay" target="_blank"> Mandalay Bay Hotel and Casino</a>. Paddock had at least 20 guns and hundreds of rounds of ammunition — some with scopes — in his hotel room, and busted out windows with a hammer-like object to create his sniper's perch roughly hundreds of yards from the <a href="https://en.wikipedia.org/wiki/Route_91_Harvest" target="_blank">Route 91 Harvest Festival of country music</a>. Analysis of the shooting video showed Paddock fired a staggering 280 rounds in one 31-second span.<br><br>

<div class="image">
<center><img src="{{ site.url }}/assets/img/runningcrowd.jpg" alt="Crowd runs while being shot at" ></center>
<div><center><font size=".5"><b>Image: Chaos as shots rang out at the Route 91 Harvest Country Music Festival in Las Vegas. <br><i>Source: David Becker/Getty Images</i></b> </font></center></div>

</div>
</i></p>     
</body>
<body style="background-color:powderblue;">
<p style="font-family:courier;"><i>
While some concertgoers hit the ground, others forced their way to the crowded exits, shoving through narrow gates, trampling one another, and climbing over fences. They had little cover and no easy way to escape. Those who were not hurt hid behind concession stands or crawled under parked cars. The scene was pure chaos. Bodies were lying on the artificial turf installed in front of the stage, and people were screaming and crying. The sound of people running on the bleachers added to the confusion, leading some of the people still present to suspect the concert was being invaded with multiple shooters. <br><br>

At 10:14 p.m., an officer said on his radio that he was pinned down against a wall on Las Vegas Boulevard with 40 to 50 people."We can't worry about the victims," an officer said at 10:15 p.m. "We need to stop the shooter before we have more victims. Anybody have eyes on him ... stop the shooter." <br><br>

 
Police frantically tried to locate the shooter and determine whether the gunfire was coming from <a href="https://s.yimg.com/ny/api/res/1.2/NK2pyf1FpkmaJzgSyiYOlQ--/YXBwaWQ9aGlnaGxhbmRlcjtzbT0xO3c9NjUwO2g9NDg4/http://globalfinance.zenfs.com/en_us/Finance/US_AFTP_SILICONALLEY_H_LIVE/Heres_what_we_know_about-a9d6cb39d84dcf2be0adc2c66844faa3" target="_blank">Mandalay Bay or the neighboring Luxor hotel</a>. Every second was precious.  Any time wasted looking in the wrong hotel resulted in more time to reload and unleash a volley of bullets on the terrified crowd below.
<br>
<div class="image">
<center><img src="{{ site.url }}/assets/img/runningCops.jpg" alt="Police taking cover" ></center>
<div><center><font size=".5"><b>Image: Heavily armed officers frantically search for the shooter. <br><i>Source: John Locher/AP Photo</i></b> </font></center></div>

</div>
</i></p>     
</body>

<hr>
        
# Code/Tutorial Introduction
Horrible flash-in-the-pan events, such as the Las Vegas active shooter crisis, happen infrequently in specific cities.  However, when looking at destabilizing events on a national or global scale, we learn that these types of events are a regular occurrence.  In the past, getting information on these events depended on the location of the event, your proximity to the event, and the likelihood of a news provider in your region (and language) covering the event. But the arrival of the information age has made it possible to learn about these events in real time regardless of location.  Services such as <a href="https://www.gdeltproject.org/" target="_blank"> Global Database of Events, Language, and Tone (GDELT)</a> track these events in remote locations across the globe.<br><br>  


This tutorial shows how the mining of auto-parsed news stories can keep you (or your client) informed of the evolving security situation in a place of interest. Included is a short introduction to a python client I built to access and wrangle parsed news stories using <a href ="http://www.gdeltproject.org/about.html" target="_blank">GDELT</a>. By the end of this tutorial, you will have the tools needed to build a timeline of events using Python and `gdeltPyR`. **More importantly, these techniques will help you create narratives from news stories written in over 100 languages using GDELT's translated events table.** For others considering writing a tutorial, try the narrative format we will use for this post. Data scientists and data engineers need to be well-versed in the art of writing and narratives provide great practice! You can <a href="https://github.com/linwoodc3/linwoodc3.github.io/blob/master/notebooks/gdeltPyR%20Tutorial%20Notebook.ipynb" target="_blank">download the notebook for this tutorial here</a>.

### Understanding the Narrative Tutorial Format

This tutorial is split into sections. We switch from a **narrative story section**, told using the data returned from `gdeltPyR` and a **tutorial section** that gives instruction on how to use `gdeltPyR` and analyze the returned data.  I use a page splitter and different font to signal the switch between a narrative and coding section.
 
Every fact and image in the narrative came from news stories accessed via gdeltPyR. Using data wrangling and time series analysis techniques, we will order the stories chronologically to see how this active shooter event evolved in time. Moreover, we understand just how responsive the GDELT service is.  Nearly one hour after the first gunshots were fired, GDELT had automatically geolocated this event to Las Vegas and catalogued it as a crisis involving firearms. The first GDELT report came at 23:15 PDT (06:15 in UTC time).   News reports suggest the shooting started at 22:08 PDT (05:08 UTC)!  We can even use time series analysis to build an alert for a city and specific type of event using GDELT data.  

It cannot go unnoticed that the example I present in this tutorial is trivial and simple.  GDELT offers more data sets and supports higher order analysis.  Data sets that are (or will be) availble via `gdeltPyR` include:
*  **Coming Soon** GDELT <a href="https://blog.gdeltproject.org/gdelt-visual-knowledge-graph-vgkg-v1-0-available/" target="_blank">Visual Global Knowledge Graph (VGKG)</a> - Access millions of images tied to news stories; includes metadata tags and other fields for higher order analysis of images, topics, and global news media
*  **Coming Soon** <a href="https://blog.gdeltproject.org/announcing-the-american-television-global-knowledge-graph-tv-gkg/" target="_blank">American Television Global Knowledge Graph (TV-GKG)</a> - programmatic access to metadata of parsed closed captioning covering more than 150 English language  American television stations in 20 markets, some dating as far back as June 2009.  Metadata and tags support higher order analysis
* **Available** <a href="https://blog.gdeltproject.org/gdelt-global-knowledge-graph/" target="_blank">Global Knowledge Graph (GKG)</a> - parsed feed that links every person, organization, location, count, theme, news source, and event mentioned in news articles published worldwide into a single network 
*  **Coming Soon** <a href="https://blog.gdeltproject.org/gdelt-geo-2-0-api-debuts/" target="_blank">GDELT GEO 2.0 API</a>- map the geography of keyword based worldwide news using a keyword filter; updates every 15 minutes.
*  **Available** <a href="https://blog.gdeltproject.org/gdelt-2-0-our-global-world-in-realtime/" target="_blank">Event mentions</a> - table that records every mention of an event over time, along with the timestamp the article was published

As you can see, GDELT is a powerful data set.  But, what exactly is GDELT? Let's run through an introduction.
 

<br>
<div class="image">
<center><img src="{{ site.url }}/assets/img/spinningglobe.gif" alt="GDELT" style="width: 55%" ></center>
<div><center><font size=".5"><b>Image: GDELT monitors world wide news and is a lens into human society.</b> </font></center></div>
</div>
<br>

### What is GDELT?

GDELT is a service that monitors print, broadcast, and web news media in over 100 languages from nearly all countries in the world. Enabled by this constant stream of news data, GDELT can monitor breaking news events anywhere on the planet. Data scientists and developers can use this data to identify news providers who have a history of generating original content earliest for breaking issues in certain parts of the world, showing you where to look for news when something is happening in your market. Conversely, analysis of GDELT data can show which news providers specialize in redisseminating another provider’s content.  In this case, a provider would value pushing out more substantive news to wider audiences at the cost of speed. Finally, as we will demonstrate in this tutorial, GDELT can be used to build event timelines.<br><br>

### GDELT’s Coding System: CAMEO Codes


The CAMEO code is the center of GDELT data analysis. CAMEO, which stands for <a href="https://en.wikipedia.org/wiki/Conflict_and_Mediation_Event_Observations" target="_blank">Conflict and Mediation Event Observations</a>, is a coding framework used to support the study of political and violent events. After passing through a series of extractors and machine learning algorithms, each news story is assigned a CAMEO code, geoinferenced location, and a series of other metadata tags for analysis.  As it's quite possible for a single news story to cover multiple topics (e.g. US President speech on multiple issues), it's possible for a single news story to have multiple CAMEO codes and GDELT entries. CAMEO codes, along with other parsed values in the GDELT record, can be used to filter and categorize news content. We can subsequently use this filtering pipeline to automatically monitor news at the city, state, or country level on multiple topics across the globe. The coding system is pretty extensive with codes for diplomatic, military, societal, criminal, and economic events or actors. For example, to track all news on mass killings in Kigali, Rwanda, we only need to filter on CAMEO code ‘202’ and the geonames feature identifier (feature ID) for Kigali, ‘-2181358’ .<br><br>

For all of GDELT’s strengths, it would be intellectually dishonest for me to ignore the reported weaknesses. To see what others have identified as strengths and weaknesses, see <a href="https://www.researchgate.net/publication/303211430_Comparing_GDELT_and_ICEWS_event_data" target="_blank">M.D. Ward et al’s Comparing GDELT and ICEWS Event Data</a>. One oft cited weakness is duplicates; we’ll introduce a quick fix to reduce duplicates when analyzing a specific CAMEO event code.<br><br>

Now that we understand GDELT, let's jump back into the story.

<hr>
## A Killer Neutralized... 


<p style="font-family:courier;"><i>

Las Vegas responders continued their search for the shooter as the terrifying sound of quick-succesion gunshots engulfed the festival grounds. At least six officers searched Mandalay Bay hotel floor by floor before they found Paddock's room minutes after the shooting started. Paddock, a 64-year old resident of a Mesquite, Nevada retirement community, had apparently rented a two-room suite in the hotel four days before the massacre. As police closed in on his position, Paddock shot and wounded a hotel security officer through the door before <a href="https://www.lvmpd.com/en-us/Pages/default.aspx" target="_blank">Las Vegas Metropolitan Police Department (LVMPD) SWAT</a> used explosives to breach room 32135. Inside, they found Paddock dead. He had killed himself. After 10 minutes of terror that seemed like an eternity, it was finally over.<br><br>

The barrage from the 32nd floor lasted several minutes but the damage was extensive.  Initially, the number of fatalities had climbed to 20. Two hours later, the number had pushed past 50, making it the deadliest active shooter event in recent history. At least two off-duty police officers were shot and killed. Two other police officers were injured, one of them critically. Over 500 people were wounded.</i></p>


<div class="image">
<center><img src="{{ site.url }}/assets/img/girlnearambulance.jpg" alt="Girl in cowboy boots near ambulance" ></center>
<div><center><font size=".5"><b>Image: A woman sits on the curb at the scene of the Las Vegas shooting. <br><i>Source: John Locher/AP Photo</i></b> </font></center></div>
<br>
</div>
 

<p style="font-family:courier;"><i>Tales of heroism and compassion emerged quickly: Couples held hands as they ran through the dirt lot. Some of the bleeding were carried out by fellow concertgoers. While dozens of ambulances took away the wounded, some people loaded victims into their cars and drove them to the hospital. At least 104 patients were treated at the University Medical Center.  Some of the youngest patients treated at the hospital were 16 and 17 years old. </i></p>


<div class="image">
<center><img src="{{ site.url }}/assets/img/carryWounded.jpg" alt="Carrying wounded girl`" ></center>
<div><center><font size=".5"><b>Image: People assist a wounded woman at the scene of the Las Vegas shooting <br><i>Source: Chase Stevens/Las Vegas Review - Journal via AP</i></b> </font></center></div>
<br><br>
</div>

<p style="font-family:courier;"><i>Those who survived physically unscathed did what they could to escape.  People fleeing the concert grounds hitched rides with strangers, piling into cars and trucks. <br><br>

With the shooter neutralized, responders tended to victims and the world searched for an answer to the most difficult question.  Why?  Why did he do it? A part of that answer would likely come from an answer to another question. Who was Stephen Paddock? </i></p>

<hr>

### Pythonic Access to Worldwide GeoReferenced News
In the same way that officers relied on training and teamwork to locate the shooter, we need a reliable tool to access GDELT data.  That's where <a href="https://github.com/linwoodc3/gdeltPyR" target="_blank">`gdeltPyR`</a> comes in .  <a href="https://github.com/linwoodc3/gdeltPyR" target="_blank">`gdeltPyR`</a> is a minimalist Python API for GDELT and an ideal tool to explore news events that evolve over time. Because of <a href="https://github.com/linwoodc3/gdeltPyR" target="_blank">`gdeltPyR`</a>'s global and multilingual focus, analysis can show how news events spread across the world. For detailed information on the project, visit the <a href="https://github.com/linwoodc3/gdeltPyR" target="_blank">`gdeltPyR` project page on GitHub</a>. 

### Set up Environment for Code in Tutorial

You can set up the environment to follow this tutorial with a few lines of code.  First, <a href="https://conda.io/docs/user-guide/install/index.html" target="_blank">make sure you have Anaconda installed</a>. Then, download my <a href="https://github.com/linwoodc3/linwoodc3.github.io/blob/master/notebooks/environment.yml" target="_blank">environment.yml</a> file, start a terminal session from the directory where the file is downloaded, and type:
```bash
conda env create; source activate gdeltblog

```
That should install all the dependencies. 

If you only want to install `gdeltPyR`, in a terminal session run:

```bash
pip install gdelt
```

Not all current events can be analyzed using <a href="https://github.com/linwoodc3/gdeltPyR" target="_blank">`gdeltPyR`</a> because GDELT is focused on news events that impact security and stability.  For examples of the types of events to test, visit the <a href="https://en.wikipedia.org/wiki/Portal:Current_events" target="_blank">Wikipedia Current Events page</a> and look at the `Armed conflicts and attacks` or `Politics and elections` entries.  Some examples I've tested include:

* <a href="https://en.wikipedia.org/wiki/2017_Manchester_Arena_bombing" target="_blank">Manchester Arena bombing</a>
* <a href="https://en.wikipedia.org/wiki/Proclamation_No._216" target="_blank">The Marawi crisis in the Philippines</a>

Outside of making sure your topic is covered in GDELT, <a href="https://github.com/linwoodc3/gdeltPyR" target="_blank">`gdeltPyR`</a> is easy to use and only requires a date when your event of interest occurs.  In the future, <a href="https://github.com/linwoodc3/gdeltPyR" target="_blank">`gdeltPyR`</a> will leverage <a href="https://cloud.google.com/bigquery/" target="_blank">Google’s BigQuery</a>, providing a way to query a specific city, landmark, actor, or CAMEO event code over any amount of time. Additionally, I will be adding a feature to query by specific Local Time or UTC time.

The Las Vegas shooting occurred on October 1, 2017 at 22:08 PDT. GDELT uses UTC datetimes, so this event has a +7 hour difference in GDELT, putting our target timeframe in the early hours of October 2.
 

Let’s set up the module and libraries:


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

The `tzwhere` library can identify the time zone offset using a latitude and longitude pair, so we import this tool for time series functionality later on. 

```python
# tzwhere variable for time normalization
tz1 = tzwhere.tzwhere(forceTZ=True)

# instantiate the gdeltPyR object for searches
gd = gdelt.gdelt()
```

With our libraries set up, let's get back into the story.
<br><br>
<hr>

### Who was Stephen Paddock?<br>
<p style="font-family:courier;"><i>
The search to understand Stephen Paddock started in the room where he died. Police recovered 23 guns (some with scopes) from his room where hotel workers, who were in and out of the room over several days, said they “saw nothing at all” hinting at the forthcoming rampage. At least two of the guns were modified with <a href="https://en.wikipedia.org/wiki/Bump_fire" target = "_blank">bump-stock devices</a> which can be attached to the stocks of semiautomatic guns to allow fully automatic gunfire. Investigators could tell from the arsenal, Paddock was intent on killing as many people as possible and the number killed on Oct 1 could have been higher if not for the quick response of the officers.  Despite the large arsenal in the room, authorities still had little insight into "why" he did it. Paddock's death meant investigators would be on a scavenger hunt to discover a motive.
</i></p>

<div class="image">
<center><img src="{{ site.url }}/assets/img/paddockFace.jpg" alt="Stephen Paddock" ></center>
<div><center><font size=".5"><b>Image: Stephen Paddock, the gunmen in the Las Vegas massacre</b> </font></center></div>
<br>
</div>


<p style="font-family:courier;"><i>
In the midst of the hotel room search, officers executed a search warrant at Paddock's three-year-old, 396,000 US dollar two-bedroom home in the tiny desert community of <a href="https://en.wikipedia.org/wiki/Mesquite,_Nevada" target="_blank">Mesquite</a>, 80 miles north-east of Las Vegas. The discovery included more of the same.  They found 19 additional guns, thousands of rounds of ammunition, and explosives. Investigators said they discovered several pounds of <a href="https://en.wikipedia.org/wiki/Ammonium_nitrate" taret="_blank">ammonium nitrate</a> in his car, a fertilizer that can be used to create explosives.
</i></p><br>

<div class="image">
<center><img src="{{ site.url }}/assets/img/paddockHome.jpg" alt="Stephen Paddock home" ></center>
<div><center><font size=".5"><b>Image: Stephen Paddock's home in Mesquite, NV. </b> </font></center></div>
<br>
</div>
<div><p style="font-family:courier;"><i>


With the physical search ongoing, officers turned to Paddock's close relationships and life.  He had a live-in girlfriend, 62-year-old Marilou Danley, who was traveling in the Philippines when the massacre took place. Although Paddock used some of her identification to check into the hotel, investigators clarified that they believed she was not involved with the shooting. He married Peggy Okamoto in 1985 but the couple divorced in 1990, nearly three decades ago.   Peggy, now living in Los Angeles County, California, said she had no contact with him for years.<br><br>

Financially, Paddock was a wealthy man.  He was worth more than $2 million, having made a good chunk of money from buying and selling real estate in several states, including California, Nevada, Florida and Texas. As a retiree, he had no children and plenty of money to play with. So, he took up gambling.
Paddock told neighbors he was a professional gambler and a prospector, and liked to bet big, wagering tens of thousands of dollars in a sitting. 
<br><br>

Perhaps Paddock had a checkered past or multiple run-ins with police?  Investigators quickly learned this was not the case.  A criminal check provided little insight into Paddock’s motive or temperament because he had no criminal record and was not believed to be connected to any militant group. “We have no idea what his belief system was,” Lombardo said. “I can’t get into the mind of a psychopath.”<br><br>

Next, officers looked into Paddock's arsenal.  The paper trail could possibly reveal something.  Initial research suggested Paddock had purchased  his firearms legally. A Mesquite store, Guns & Guitars, said it sold a gun to Paddock and that “he never gave any indication or reason to believe he was unstable or unfit at any time.” Additional research showed he had purchased multiple firearms in the past, with several of them purchased in California, according to law enforcement officials. Interestingly, those guns didn't appear to be among the 10 or more guns found in the Mandalay Bay hotel room.  Nothing materialized from the gun angle.<br><br>
</i></p><br>

<div class="image">
<center><img src="{{ site.url }}/assets/img/gunsNguitars.jpeg" alt="Girl in cowboy boots near ambulance" ></center>
<div><center><font size=".5"><b>Image: Gun store where Paddock purchased some guns. <br><i>Source: Getty</i></b> </font></center></div>
<br>
</div>

<p style="font-family:courier;"><i>
Then, the search moved to Paddock's hobbies.  He had two planes and held a private pilot's license but had not updated the medical certification required to fly since 2008 or 2010. According to relatives,  Paddock liked country music and went to concerts like the Route 91 Harvest festival he attacked on Sunday night.<br><br>

The look into Paddock's past was proving fruitless.  Nothing about Paddock, <a href="https://www.theguardian.com/us-news/2016/sep/20/gun-ownership-america-firearms-super-owners" target="_blank">including his ownership of over 40 guns</a>, seemed out of place or out of the ordinary. Officers decided to move to his family history next.  Perhaps his siblings or parents would provide clues.

 </i></p>
</div>

<hr>

## Using [`gdeltPyR`](https://github.com/linwoodc3/gdeltPyR)
Unlike the difficulties investigators experienced in trying to find Paddock's motive, `gdeltPyR` is easy to understand and use. As stated earlier, we only need a date and information about the location to find the target data. After we filter the data to the relevant GDELT records, it’s just a “point, click, and read” job because the news stories will be categorized and organized by time.

The code to pull data for October 1 through October 3:

```python
# code to use gdeltPyR; pulling all of 1-3 Oct data (coverage = True) 
# and normalizing column names to SQL friendly format (normcols=True)

vegas = gd.Search(
                  date=['2017 Oct 1','2017 Oct 3'],
                  coverage=True,
                  normcols=True
                  )
```

Depending on your internet connection, this could take several to tens of seconds to download. My query took 40 seconds to return 461,243 a row by 62 column dataframe that is 996.1 MB. The time to download data will be drastically reduced <a href="https://github.com/linwoodc3/gdeltPyR/issues/24" target="_blank">when `gdeltPyR` includes a direct connection to Google BigQuery.</a>  GDELT also ships data out in 15 minute intervals; if you set the `coverage` parameter to `False`, it takes 1-2 seconds to return a 2000-3000 row by 62 column dataframe. As GDELT is updated every 15 minutes, a near realtime feed would be easy to manage.

As disscussed earlier, one article can have multiple entries with different CAMEO codes.  Our goal is to use the returned metadata to filter down to the relevant records.  To see the full details on the columns/metadata, see the <a href="https://github.com/linwoodc3/gdelt2HeaderRows/blob/master/schema_csvs/GDELT_2.0_Events_Column_Labels_Header_Row_Sep2016.csv" target="_blank">schema descriptions here.</a> The most relevant columns for this post are described in the table below:

| Column Name  |  Description |
|---|---|
| **ActionGeo_Lat**  | field providing the centroid latitude of the landmark for mapping.  |
| **ActionGeo_Long**  | field providing the centroid longitude of the landmark for mapping.  |
| **ActionGeo_FeatureID**  | field specifies the GNS or GNIS FeatureID for this location.  |
|  **ActionGeo_Type** |  field specifies the geographic resolution of the match type and holds one of the following values: 1=COUNTRY (match was at the country level), 2=USSTATE (match was to a US state), 3=USCITY (match was to a US city or landmark), 4=WORLDCITY (match was to a city or landmark outside the US), 5=WORLDSTATE (match was to an Administrative Division 1 outside the US – roughly equivalent to a US state). This can be used to filter events by geographic specificity, for example, extracting only those events with a landmark-level geographic resolution for mapping. |
| **EventCode**   | This is the raw CAMEO action code describing the action that Actor1 performed upon Actor2.  |
| **EventRootCode**  |  This defines the root-level category the CAMEO event code falls under. For example, code “0251” (“Appeal for easing of administrative sanctions”) has a root code of “02” (“Appeal”). This makes it possible to aggregate events at various resolutions of specificity. For events at levels two or one, this field will be set to EventCode. |
| **DATEADDED**  | field provides the date the event was added to the master database in YYYYMMDDHHMMSS format in the UTC time zone. For those needing to access events at 15 minute resolution, this is the field that should be used in queries.  |
|  **SOURCEURL** | This field records the URL or citation of the first news report it found this event in. In most cases this is the first report it saw the article in, but due to the timing and flow of news reports through the processing pipeline, this may not always be the very first report, but is at least in the first few reports.

>**Note:**`gdeltPyR` can normalize columns names into <a href="https://www.loc.gov/preservation/digital/formats/fdd/fdd000280.shtml" target="_blank">ESRI shapefile friendly strings</a> when the `normcol` parameter is set to `True`.  So, `ActionGeo_Lat` would become `actiongeolat` 


Each record in the <a href="https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe" target="_blank">dataframe</a> is a news report in time so we can treat this as a time series.  Moreover, GDELT returns data in equally spaced intervals of time which works well for <a href="https://en.wikipedia.org/wiki/Time_series" target="_blank">time series analysis</a>.<br><br>

To condition our data for time series analysis, we will create and use custom functions to make time aware columns that can be used to index our data (e.g. transform UTC to local Pacific Daylight Time using the lat/lon).  The code block that follows creates the function and applies it via <a href="https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.vectorize.html" target="_blank">numpy vectorization</a>.  We will also use a chained <a href="https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.assign.html" target="_blank">`pandas.DataFrame.assign` operation</a> to create our new columns.

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
    
    # get the time zone string representation using lat/lon pair
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


The code above created two time-enabled columns; `dates` and `zone`. Both columns are <a href="https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.datetime.html#datetimes-and-timedeltas" target="_blank">`datetime64[ns]` data types</a>, which means they can be used for <a href="https://pandas.pydata.org/pandas-docs/stable/timeseries.html" target="_blank">time series functionality in pandas</a>. The `zone` column is a time zone aware data type (Los Angeles time), which adds the time zone offset to `UTC` time. The `dates` column is UTC time. <br><br>

We can filter out any records not related to the Las Vegas shooting using a combination of:
*  <a href ="http://data.gdeltproject.org/documentation/CAMEO.Manual.1.1b3.pdf" target="_blank">CAMEO event root codes</a> of 18, 19, and 20 which stand for **assault**, **fight**, and **engage in unconventional mass violence** respectively.  See the <a href ="http://data.gdeltproject.org/documentation/CAMEO.Manual.1.1b3.pdf" target="_blank">CAMEO code reference for details on CAMEO event codes.</a>  For a higher level of aggregation, consider using the `QuadClass` field as a filter for the GDELT results. 
*  Search for GNIS feature ID representing Las Vegas,**847388**, in the `actiongeofeatureid` field <br><br>
>**Note** To get more accurate results, use the <a href="https://geonames.usgs.gov/apex/f?p=138:1:0::NO:::" target="_blank">GNIS Feature ID</a> for your location filter as opposed to the string representing the location name because some news reports can spell place names differently. A trick to find the feature ID without searching the <a href="https://geonames.usgs.gov/apex/f?p=138:1:0::NO:::" target="_blank">GeoNames website</a> is to run a `gdeltPyR` query, find a relevant entry, copy the feature ID value, and filter the data using your new value.  The feature ID for Las Vegas is **847388**. When the `ActionGeo_Type` field is 3 or 4, understand the feature ID could also be specific and reference a landmark inside a city (stadium, park, building, etc.)

To get help on the fields, reference this <a href="https://github.com/linwoodc3/gdelt2HeaderRows/blob/master/schema_csvs/GDELT_2.0_Events_Column_Labels_Header_Row_Sep2016.csv" target="_blank">headers information file.</a> Finally, we use <a href="https://pandas.pydata.org/pandas-docs/stable/indexing.html" target="_blank">chained pandas indexing functionality</a> to filter our data in the code block below.

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

This operation drastically reduced the size of our data set (from 400,000+ to ~1200).  The next step is building the list of chronological news stories. For this post, I manually read stories to extract facts.  However, you could leverage <a href="https://en.wikipedia.org/wiki/Open_information_extraction" target="_blank">information extraction tools combined with entity extractors</a> to build a knowledge base for events of interest.  That would be a higher level of analysis and is outside the scope of this post.  To build the list of articles, see the code below.    

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

Finally, to build a narrative, I read articles chronologically to see how the story unfolded in time. You can look at the url strings to skip irrelevant articles (first 6) or we could use time series analysis to identify a timeframe when the number of news articles with our CAMEO code and in our location of interest increases to an abnormal rate (higher than normal using a running average count).  <br><br>

While reviewing the articles, stay alert.  News providers will update information but use the same url.  Therefore, some stories will have more information than they had when originally published. GDELT preserves the original time of the article but not the content; you should see clues in the text to let you know the article was updated.  Additonally, it's important to be aware of <a href="https://en.wikipedia.org/wiki/Participation_bias" target="_blank">participation or non-response bias</a>.  There may be a news provider who did not have its data processed by GDELT, leading to a faulty conclusion that one particular news provider is faster than another.  As always, be wary of data limitations.<br><br>

If you wanted to index the entire data set for time series analysis, it's relatively simple because `gdeltPyR` returns the data in a <a href="https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe" target="_blank">pandas dataframe.</a>  First you would localize the entire dataset to UTC time and then convert it to any time zone offset using the <a href="http://pytz.sourceforge.net/" target="_blank">Python time zone string of your choice</a>. 

```python
# example of converting to Los Angeles time. 
vegastimed.set_index(
    vegastimed.dates.astype('datetime64[ns]')
                    ).tz_localize(
                                'UTC'
                                ).tz_convert(
                                            'America/Los_Angeles'
                                            )
                                            
# get time zone string using pytz 
```
<br><br>
Alternatively, you could use the <a href="https://gist.github.com/linwoodc3/5c915fb6d9097e7e27d5b0bc1f047ba2" target = "_blank">`tzwhere` library with latitude and longitude</a> to find the time zone string for each GDELT record and normalize time this way.  Warning! It is computationally expensive to run this time zone analysis over the entire dataset.

Our data is ready for time series analysis, but first, let's jump back into the story to see what the police learned about the suspect from family and friends.  
<hr>
### Still Seeking a Motive, Investigators Turn to Family and Friends
<div><p style="font-family:courier;"><i>
With little to show from all other leads, investigators hoped family members could provide some answers. At first glance, Stephen Paddock's parental history seemed to provide some clues.  <br><br>

Decades before that fateful Sunday when Stephen perpetrated the worst active shooting event in recent US history, his father was on the FBI’s most-wanted list.  Benjamin Hoskins Paddock had been sentenced to 20 years in prison after being convicted of bank robbery and automobile theft.   In 1969, when Stephen was 15 years old, Benjamin escaped from prison in El Paso, Texas. He remained on the Most Wanted List from June 10, 1969 until May 5, 1977.  He was finally captured in 1978 while running a bingo parlor in Oregon. <br><br>
</i></p><br>

<div class="image">
<center><img src="{{ site.url }}/assets/img/paddockDad.jpg" alt="father" ></center>
<div><center><font size=".5"><b>Image: Mugshot of shooter's father, Benjamin Hoskins Paddock.</b> </font></center></div>
<br>
</div>

<p style="font-family:courier;"><i>
While the paternal history seemed promising, comments by Eric Paddock, Stephen Paddock's brother, suggested the father had little influence in his upbringing. <br><br> 

“I didn’t know him. We didn’t know him,” Eric Paddock said of his paternal father, Benjamin Paddock. “He was never with my mom. I was born on the run and that’s the last time he was ever associated with by our family.”<br><br>

Another dead end.<br><br>

As the only family member speaking publicly, Eric answered questions on his brother's frame of mind, which only raised **more** questions as to why Stephen picked up the gun that Sunday night.  His answers didn't get us any closer to a motive. 

</i></p>

<div class="image">
<center><img src="{{ site.url }}/assets/img/brotherpaddock.jpeg" alt="brother" ></center>
<div><center><font size=".5"><b>Image: The shooter's brother, Eric Paddock, talks with reporters.</b> </font></center></div>
<br>
</div>

<p style="font-family:courier;"><i>

"We have absolutely no idea whatsoever," Eric Paddock said to reporters gathered outside his home Monday morning. "We have no idea why he did this. And that's what you're going to find out. I can't imagine. When you guys found out why this happened, let us know. I have no idea whatsoever."<br><br>

The response seemed totally out of touch with the man who used his modified rifles to kill 50 and wound over 500 innocent people.  Even more troubling, was the brother's comments on his brother's ownership of guns. He said Stephen was, “Not an avid gun guy at all...where the hell did he get automatic weapons? He has no military background."  But, as it turns out, Stephen had a lot of guns.  More importantly, he had guns that suggested an affinity and interest that surpassed those of a "casual" gun owner.    
</i></p>

<div class="image">
<center><img src="{{ site.url }}/assets/img/shooting-brother.jpg" alt="brothers together" ></center>
<div><center><font size=".5"><b>Image: Older picture of Paddock brothers.</b> </font></center></div>
<br>
</div>

<p style="font-family:courier;"><i>
<br><br>Statements from Paddock's live-in girlfriend were contradictory as well when compared to his actions. Everyone painted Paddock as a guy who kept to himself. They all seem genuinely surprised. <br><br>
"I knew Stephen Paddock as a kind, caring, quiet man," Marilou Danley said in a statement read by her attorney. "He never said anything to me or took any action that I was aware of that I understood in any way to be a warning that something horrible like this would happen.”<br><br> 
  
</i></p>

<div class="image">
<center><img src="{{ site.url }}/assets/img/marilou.jpg" alt="girlfriend" ></center>
<div><center><font size=".marilou.jpg"><b>Image: Stephen Paddock's close female companion,Marilou Danley.</b> </font></center></div>
<br>
</div>
</div>

<p style="font-family:courier;"><i>It seemed that no one truly knew Stephen Paddock. Or perhaps the Paddock who fired the gun on thousands of helpless people was the imposter; perhaps he snapped that day.  Either way, there was no conclusive evidence.
</i></p>

### Investigation Continues but Questions Remain

<p style="font-family:courier;"><i>
Family and friend interviews answered questions about Stephen Paddock the person. But they did not answer questions about Paddock the gunman.  Overall, investigators did an admirable job piecing together the timeline of events and gathering background on the shooter.  They had information on the shooter's life, friends, financial situation, family history, and insight into where he purchased the guns. <br><br> 

As the aftermath of the Las Vegas event settles, the world struggles to come to terms with what happened.  Each person or group affected has something to cope with: families mourn those who perished,  the injured begin the healing process, people close to Stephen question if they ever really knew him, survivors confront the reality of their escape from death or maiming, and everyone struggles to make sense of the whole ordeal.  The timeline of events is somewhat clear, but one glaring question remains.  <br><br> Why? <br><br>  Why did Stephen Paddock bring all those guns to his room?  Why did he snap that day? Why did he go on to commit the worst active shooter crisis in modern US history? <br><br> 

Only time will tell.<br><br> 

Or worse. Perhaps we will never know. 

</i></p>

<hr>


## The Data Science Detour: Analyzing GDELT data

Our narrative ended with a lot of unanswered questions about Paddock, but our code tutorial answered several questions regarding `gdeltPyR` and GDELT.  We learned GDELT is a service that monitors print, broadcast, and web news media all over the world in over 100 languages.  We also learned the `gdeltPyR` library provides a Pythonic pathway to query GDELT's parsed news data. Then, we used `gdeltPyR` to get a tidy, time-enabled data news data set about the Las Vegas event, which ultimately provided all the data to see how the event evolved. As stated, my example is trivial and focused on a U.S. problem; we could have easily picked a similar event in some remote part of the world and had similar results. 

Up until now, our coding was utilitarian in nature;  it was focused on defining and downloading the GDELT data we wanted.  To cross into the realm of data science, we need to extract knowledge or insights from our GDELT data that could drive a decision.  In data science, the goal is to create a data product. Data products <a href="https://www.goodreads.com/author/quotes/8647128.Benjamin_Bengfort" target="_blank">derive their value from data and generate more data by influencing human behavior or by making inferences or predictions upon new data</a>.  In this section, we use GDELT data to answer questions where the answers could be used to drive human or business decisions.  

While reading, feel free to pause and try your solution before continuing to my solution.  These are simple questions so give it a try.  

### Question 1: Who Produced the Most Articles About the Las Vegas Active Shooter Event? 

With the analytic power of Python `pandas` and <a href="https://en.wikipedia.org/wiki/Regular_expression" target="_blank">regex</a>, we can identify the news source with the highest original production (unique urls).  As stated early on, one problem with GDELT is duplicates.  A parsed news article can have multiple entries that use the exact same url. Moreover, the urls are unique in that they point to specific articles.  We can use regex to strip the root URL from each record and then count occurrences.  To find our providers, we need to strip the base URL and not just use article URLs for analysis.  I wrote some regex to accomplish both. Again, we use chained operations to get our desired output in one line of code.

```python
import re
import pandas as pd

# regex to strip a url from a string; should work on any url (let me know if it doesn't)
s = re.compile('(http://|https://)([A-Za-z0-9_\.-]+)')

# apply regex to each url; strip provider; assign as new column
print(vegastimedfil.assign(provider=vegastimedfil.sourceurl.\
      apply(lambda x: s.search(x).group() if s.search(x) else np.nan))\
.groupby(['provider']).size().sort_values(ascending=False).reset_index().rename(columns={0:"count"}).head())
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
      <td>https://www.yahoo.com</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>https://www.reviewjournal.com</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>https://article.wn.com</td>
      <td>14</td>
    </tr>
    <tr>
      <th>3</th>
      <td>https://patch.com</td>
      <td>11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>http://www.msn.com</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

<br><br>After some research into the top URLs, you'll find <a href="https://www.reviewjournal.com" target="_blank">`https://www.reviewjournal.com`</a> is an interesting as top producer with `15` stories.  The other sites are world wide generic sites that likley have syndicated reporting. But <a href="https://www.reviewjournal.com" target="_blank">`https://www.reviewjournal.com`</a> is different.  A visit to the site and close look at the top left banner provides all the information we need.
<div class="image">
<center><img src="{{ site.url }}/assets/img/reviewjournal.png" alt="Review Journal" ></center>
<div><center><font size=".5"><b>Image: The Review Journal is a local paper in Las Vegas.</b> </font></center></div>
<br>
</div>
After visiting the site, we see the name is the ***Las Vegas*** Review Journal, which explains a lot.  This is a local paper, meaning this provider is more likely to have reporters on the ground to keep its viewership/readership informed of breaking information.   
<br>
How can this information help drive decisions?  While anecdotal, we used analytics to identify a local news provider to keep track of major events in city.  This could be repeated for the same city to get a more statistically relevant conclusion. Moreover, this analytic could be repeated for other cities to find the local papers/providers for each city of interest.  With this information, it's possible to keep a tab on local events and how the local population perceives the events.  Finally, it's pretty interesting to find this Las Vegas paper in the midst of the generic producers.  But that leads to our next question; how many news providers did we have producing on this issue?     


### Question 2: How many unique news providers did we have producing on the  the Las Vegas Active Shooter Event? 

The purpose of answering this question is to see just how wide GDELT's coverage is; does GDELT have a few sources publishing multiple stories or does are multiple sources publshing a few stories? This question is easy to answer because of the work we did in the previous question.  Each base url counts as a unique news provider (e.g. https://www.reviewjournal.com).  GDELT gave us a <a href="https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html" target="_blank">tidy data set</a>, so we just count up the occurrences.  

```python
# chained operation to return shape
vegastimedfil.assign(provider=vegastimedfil.sourceurl.\
      apply(lambda x: s.search(x).group() if \
      s.search(x) else np.nan))['provider']\
.value_counts().shape
---------------------
Out: (797,)
```
GDELT pulled from 797 news sources for this Las Vegas active shooter story alone; that's out of ~1200 stories. Imagine how many providers exist for the entire day?  <br><br>This provides some evidence of GDELT's wide reaching sources. Looking at the distribution plots below, we see that most news providers wrote less than 5 news stories, with most only producing between 1 and 2 stories.  If a news provider produced 4 articles, they were in the 95th percentile.  So, all producers above this number can be considered high producers, and with the Las Vegas Review being a local paper, that's pretty impressive to be in the top 5 with global producers like Yahoo, World News, Patch, and MSN. If we were advising our clients on which news sources to use for the security situation in Las Vegas, we have a data-based reason to recommend the Review Journal over other local providers.  Of course, additional tests would make the recommendation stronger.
> These recommendations are based on GDELT processed news and not raw parsing of all news.  It's always good practice to caveat the limitations of the data and recommendations that come from your analysis of the data.

Here is the distribution plot.

```python
import matplotlib.pyplot as plt
import seaborn as sns

# make plot canvas
f,ax = plt.subplots(figsize=(15,5))

# set title
plt.title('Distributions of Las Vegas Active Shooter News Production')

# ckernel density plot
sns.kdeplot(vegastimedfil.assign(provider=vegastimedfil.sourceurl.\
      apply(lambda x: s.search(x).group() if s.search(x) else np.nan))['provider']\
.value_counts(),bw=0.4,shade=True,label='No. of articles written',ax=ax)

# cumulative distribution plot
sns.kdeplot(vegastimedfil.assign(provider=vegastimedfil.sourceurl.\
      apply(lambda x: s.search(x).group() if s.search(x) else np.nan))['provider']\
.value_counts(),bw=0.4,shade=True,label='Cumulative',cumulative=True,ax=ax)

# show it
plt.show()
```
<div class="image">
<center><img src="{{ site.url }}/assets/img/cumPlot.png" alt="Review Journal" ></center>
<div><center><font size=".5"><b>Graphic: Distribution plot show LV Review Journal is in category of its own.</b> </font></center></div>
<br>
</div>

A good number of new sources only published one or two stories; this could be for a number of reasons.  Those producers who don't have many viewers/readers in Vegas would may provide an initial report from a syndicated partner or a precursory update for a national/global audience.  In another scenario, national/global providers may wait to get resources on site to before starting a heavy reporting line on a remote topic.  The latter suggests we should expect to see a gradual rise in the number of published reports about the event as more reporters get in place. That leads to our next question, which uses time series analysis concepts.

### Question 3: What changes did we see in the volume of news reports about the Las Vegas active shooter event?

Time series is where GDELT data shines.  GDELT processes data in equally spaced intervals (15 minutes), and we can use an exponentially weighted moving average to look at the volumetric change.  To improve the validity of the results, we will normalize the count of Las Vegas active shooter news tories in GDELT to the total count of news stories in GDELT for each 15 minute interval.  As a result, we will see our monitored value as a proporation as opposed to seeing a raw count.  For example:
*  1000 total GDELT events for one 15 minute interval
*  100 total events in our CAMEO code of interest for the same 15 minute interval
*  We would just divide 100/1000 to get our normalized value for the 15 minute interval

Our data is time indexed to Los Angeles time. Again, I'm using chained `pandas` operations to simply the code to fewer lines. Here is the code and plot.
```python
import matplotlib.pyplot as plt
timeseries = pd.concat([vegastimed.set_index(vegastimed.dates.astype('datetime64[ns]')).tz_localize('UTC').tz_convert('America/Los_Angeles').resample('15T')['sourceurl'].count(),vegastimedfil.set_index('zone').resample('15T')['sourceurl'].count()]
         ,axis=1)

# file empty event counts with zero
timeseries.fillna(0,inplace=True)

# rename columns
timeseries.columns = ['Total Events','Las Vegas Events Only']

# combine
timeseries = timeseries.assign(Normalized=(timeseries['Las Vegas Events Only']/timeseries['Total Events'])*100)

# make the plot
f,ax = plt.subplots(figsize=(13,7))
ax = timeseries.Normalized.ewm(adjust=True,ignore_na=True,min_periods=10,span=20).mean().plot(color="#C10534",label='Exponentially Weighted Count')
ax.set_title('Reports of Violent Events Per 15 Minutes in Vegas',fontsize=28)
for label in ax.get_xticklabels():
      label.set_fontsize(16)
ax.set_xlabel('Hour of the Day', fontsize=20)
ax.set_ylabel('Percentage of Hourly Total',fontsize='15')
ax.legend()
plt.tight_layout()
plt.show()
```
<div class="image">
<center><img src="{{ site.url }}/assets/img/countGraphic.png" alt="EWMA of Events" ></center>
<div><center><font size=".5"><b>Graphic: Normalized count of events in Las Vegas. Peak begins after 11pm PDT.</b> </font></center></div>
<br>
</div>

As we noted early on in this post, GDELT automatically geolocated this news event to Las Vegas within 1 hour of the gunshots being fired.  While it's true that breaking news and television stations were reporting the story within minutes, it's important to note that GDELT **automatically inferred the location, CAMEO code, and actors**.  If a system is looking at multiple cities across the globe for specific events, `gdeltPyR` and GDELT can be a force multiplier when human capital and time are constraining factors. If we w 

Speaking of time, we can explore one more time aspect of this data.

### Question 4: Using the GDELT processed news providers as the population, which provider produced the fastest overall?

This question can be tricky, but we have all the data needed to answer the question.  We want to calculate, on average, which news provider gets stories out faster.  In a business case, the answer to this question would support the recommendations we made earlier, giving our client an added dimension to not just track the news provider who produces the most, but also the provider who is fastest on the scene when a breaking event happens.  

To get an average time, we need time as an integer (<a href="https://en.wikipedia.org/wiki/Unix_time" target="_blank">epoch</a>).  The bulk of this computation will focus on converting to epoch. We are getting slightly more advanced in our wrangling/computation.  The steps we will follow are:
*  Group data by news source
*  Filter data and only keep sources that provided 3 or more original news stories
*  Compute summary statistics (mean, max, min) over our epoch timestamps for each provider
*  Convert <a href="https://en.wikipedia.org/wiki/Unix_time" target="_blank">epoch time</a> to human readable datetime
*  Sort the final results; provider with earliest average listed first
*  Localize the time to UTC
*  Convert the time from UTC to Philippines time
*  Rename columns
*  Rename index

Here is the code:

```python

# complex, chained operations to perform all steps listed above

print((((vegastimedfil.reset_index().assign(provider=vegastimedfil.reset_index().sourceurl.\
      apply(lambda x: s.search(x).group() if s.search(x) else np.nan),\
                                      epochzone=vegastimedfil.set_index('dates')\
                                      .reset_index()['dates']\
.apply(lambda x: (x.to_pydatetime().timestamp()))).groupby('provider')\
.filter(lambda x: len(x)>=10).groupby('provider').agg([np.mean,np.max,np.min,np.median])\
.sort_index(level='median',ascending=False)['epochzone']['median'])\
  .apply(lambda x:datetime.datetime.fromtimestamp(int(x)))\
.sort_values(ascending=True)).reset_index()\
 .set_index('median',drop=False)).tz_localize('UTC')\
.tz_convert('America/Los_Angeles'))
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>provider</th>
      <th>median</th>
    </tr>
    <tr>
      <th>median</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-10-02 15:45:00-07:00</th>
      <td>https://www.reviewjournal.com</td>
      <td>2017-10-02 22:45:00</td>
    </tr>
    <tr>
      <th>2017-10-02 18:15:00-07:00</th>
      <td>https://www.yahoo.com</td>
      <td>2017-10-03 01:15:00</td>
    </tr>
    <tr>
      <th>2017-10-02 19:45:00-07:00</th>
      <td>https://article.wn.com</td>
      <td>2017-10-03 02:45:00</td>
    </tr>
    <tr>
      <th>2017-10-03 08:00:00-07:00</th>
      <td>https://patch.com</td>
      <td>2017-10-03 15:00:00</td>
    </tr>
  </tbody>
</table>

It comes as no surprise that the local paper, the <a href="https://www.reviewjournal.com" target="_blank">Las Vegas Review Journal</a>, is the fastest overall producer on this topic when we consider new producers who produced a minimum of 10 articles. Returning to our ficticious business customer, we have more ammunition for our data-based recommendation to follow the Las Vegas Review Journal for violent event coverage in Las Vegas.  We would of course need to test this scenario on other high profile events, but we have some preliminary information to have discussions with our customer.  

We will close this post with a challenge to answer the most difficult question. 

# The Data Scientist Challenge
### Question 5: Who produces the most semantically dissimilar content?  

By answering this question, and combining with all the answers from above, we could more confidently recommend a local new source to our client because we identified:

* who produces the most
* who produces the fastest
* who produces the most unique content

> **Note** Every recommendation/classification above is caveated with "according to GDELT parsed news feeds".  And, we would need more examples to increase the relevance of the recommendation

In totality, these answers identify the producer who is always getting the scoop on a story using a repeatable data-driven approach.  While this challenge posits the most difficult question, the tools/libraries that you can use are well known. Consider using <a href="http://scikit-learn.org/stable/tutorial/text_analytics/working_with_text_data.html" target="_blank">scikit-learn</a>, <a href="https://radimrehurek.com/gensim/tut1.html" target="_blank">gensim (semantic similarity)</a>, and <a href="http://www.nltk.org/howto/metrics.html" target="_blank">nltk (Levenshtein edit distance)</a>, etc. 

The first step to answer **Question 5** is getting the content, and I'll provide the code for you.

The function to scrape content works surprisingly on from *MOST* news websites. For those websites where it doesn't work (blocked, IP issues, etc.), I added exceptions and warnings to give as much information as possible.  Here is the code from my GitHub gist: 

{% gist linwoodc3/e12a7fbebfa755e897697165875f8fdb %} 

I will provide an example of using the code. When building text corpora in Python, remember to `yield` instead of `return` in your function.  `yield` leads to a lazy (on demand) generation of values, which translates to lower memory usage. This code stores the returned data in memory but could easily be modified to write to disk.

```python
# create vectorized function
vect = np.vectorize(textgetter)

#vectorize the operation
cc = vect(vegastimedfil['sourceurl'].values[10:25])

#Vectorized opp
dd = list(next(l) for  l in cc)

# the output
pd.DataFrame(dd).head(5)
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>base</th>
      <th>text</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>http://www.goldcoastbulletin.com.au</td>
      <td>Automatic gunfire at the Mandalay Bay Resort i...</td>
      <td>Las Vegas shooter: Mandalay Bay casino gunman ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>http://www.sanluisobispo.com</td>
      <td>Unable to reach website.</td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>http://www.nydailynews.com</td>
      <td>\r\n\tA lone shooter rained death along the La...</td>
      <td>Mass shooting at Mandalay Bay concert in Las V...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>http://www.hindustantimes.com</td>
      <td>A gunman opened fire at a country music festiv...</td>
      <td>Las Vegas shooting: Over 20 dead, 100 injured;...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>https://www.themorningbulletin.com.au</td>
      <td>\n\tLAS Vegas shooter Stephen Paddock had a st...</td>
      <td>Las Vegas shooting: Gunman Stephen Paddock had...</td>
    </tr>
  </tbody>
</table>


You have all the data to complete the challenge! Thanks for reading! I'm curious to see how you tackle this problem.  Please share!
