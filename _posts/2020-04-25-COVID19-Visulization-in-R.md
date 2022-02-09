---
layout: post2
title: "Covid19 Visulization in R"
subtitle: "Create interactive Geo-spatial maps with the leaflet and highchart package"
background: '/img/posts/covid19/coivd_bkg.jpg'
# image: "/img/posts/covid19/coivd_bkg.jpg"
---

### Introduction
In December 2019, COVID-19 coronavirus was first identified. By March 11, 2020, the World Health Organization (WHO) categorized the COVID-19 outbreak as a pandemic. Currently, on date 4 May 2020, 3.53 million people are infected. Pandemic is spreading all over the world, it becomes literately important to understand about this spread. 

Fortunately, organizations around the world have been collecting data so that CDCs can monitor and learn from this pandemic. Notably, the Johns Hopkins University Center for Systems Science and Engineering created a publicly available data for us to make out how did the virus spread across the globe. 

To answer the question of "Given the history data of confirmed, recovered, and death number, how COVID-19 spread worldwide so far?"
I discuss from three perspectives: 
1. Geographical distribution across the world
2. COVID-19 situation Changes with Time
3. Whether lock-down policy is effective 

### How COVID-19 spread across the world
We are now going to create an interactive map with leaflet to see how COVID19 start sprouting across the world.
<iframe src="/img/posts/covid19/covid_map.html" height = "13%" width = "100%"></iframe>
From this dynamic map, we can find that this disease first outbreaked in China in early February; thousands of people infected in Italy, Iran, and South Korea in early March, and Italy had a outbreak in mid March; meanwhile, the infected number of Asia countries almost stoped; in early April, outbreak occured in America countries and European countries, and infected number keeps increasing. 

### How COVID-19 situation Changes with Time
We are now going to create an dynamic plot with highchart to visulize stastics information about COVID19, including confirmed case number, death number ,and recovered number.
<iframe src="/img/posts/covid19/covid_timeseries.html" height = "10%" width = "100%"></iframe>
From 2020-1-26 to 2020-4-16, the confirmed cases grows very rapidly, from 555 cases to 2.12 Million. The average growth rate is about 11%, which means every 7 days, the number of infected will double on average. 
The mortality rate is around 5.5%, which is significantly higher than Seasonal flu, Swine flu or Measles, but lower than SARS(10%) and MERS.
The recovered rate has a large decrease from mid March, but here we would expect a significant delay in reporting of recovered cases. 
Here the suggestion is that people should take full attention to this high infection rate disease. Neither easily treat it as a common cold or flu, or be nervous as SARS. 

### Spreading pattern in early Sprouting countries
Studying the previous case is a good way to better understand the development pattern.
First, I filter out countries with large samples.
<img src = "/img/posts/covid19/top10.png" width = "100%">
Then, I picked out China and Italy from the top 10 country list of confirmed cases, to discuss their growth rate with the lock-down control.
<img src = "/img/posts/covid19/lock.png" width = "100%">
By comparing red line shaded in red, and blue line shaded in blue, we can see that the growth pattern is quite similar, and a obvious decrease trend after around 11 days lockdown.   
Thus, strict lockdown policy is an effective policy. We can conclude that pandemic is dangerous but still controllable if everyone can strictly keep social distance. 
Any other solution may be possible? 
My suggestions here are based on the idea of lowering two main metrics, which are confirmed case and death rate.
To lower the confirmed case: 1. keep social distance to lower affected rate; 2. control population mobility by providing shelters or tents to homeless people; 3. wash hands once arrive home
To lower the death rate: we can give supports like providing pharmacy and grocery delivery service to vulnerable people, including the elders, pregnant people and people with asthma or chronic lung disease; 
Last, keep the public informed of the lastest COVID situation and be optimistic!

All the data used in this report can be [downloaded from github](https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data/csse_covid_19_time_series), provided by JHU CSSE.  





   