---
layout: default
title: Home
navigation_weight: 1
---


### Welcome to the Data Journey of a Data Junkie

Motivation is hard to measure.   

It's one of those intangible skills that everyone wants in a friend, coworker, or subordinate. `Data Junkie` is your window into the topics and personal projects that motivate me every single day.  Welcome to my journey to become an expert in data science.   I am fueled by an unending motivation to work in the field I love.

Google and YouTube are my instructors.  Python and R are my preferred tools. Time is my only limitation.


### Blog Posts and Projects

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>


