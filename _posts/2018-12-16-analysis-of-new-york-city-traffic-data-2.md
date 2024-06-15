---
title: "Analysis of New York City traffic data"
date: "2018-12-16"
categories: 
  - "data-science"
  - "python3"
  - "web-api"
tags: 
  - "pandas"
coverImage: "Image9.jpg"
---

## Introduction

One of my first projects aimed mostly at familiarizing myself with the pandas dataframe was on the NYC traffic data. Here, we are reading in a dataset of traffic violations downloaded from [https://data.ny.gov/Transportation/Traffic-Tickets-Issued-Four-Year-Window/q4hy-kbtf](https://data.ny.gov/Transportation/Traffic-Tickets-Issued-Four-Year-Window/q4hy-kbtf). The intention is to extract useful patterns in traffic violations that will be helpful for the police department in order to better manage traffic violations. Also, this analysis could potentially be useful for the everyday commuter. For this project, I used a public dataset released by the New York State DMV for traffic violations in a four-year window between 2013 and 2016. Data extracted from records of tickets on file with NYS DMV. The tickets were issued to motorists for violations of

We start off by loading the dataset as a csv file. This raw dataset contains 1.5 GB of data with about 3 million rows. Let's read in this data into a dataframe and view the data.

<script src="https://gist.github.com/ajey091/17f652b3df45b53a577ff239b30b88ca.js"></script>

![Image1](/assets/images/Image1.png)

Let's jump into the analysis. For starters, let's look at which months have the highest number of violations. At this point, it would be expected that the summer months have higher number of violations simply because there are more drivers on the road. But we shall see.

<script src="https://gist.github.com/ajey091/519ef4b316d78facd190f46db68cff66.js"></script>

![Image2](/assets/images/Image2.png)

While we are seeing that the highest number of violations are committed in the months of March-May, it is rather surprising that the months of June-September (which would involve large amounts of travel) having a dip in the number of violations.

Next, let's look at the distribution of traffic violations on different days of the week.

<script src="https://gist.github.com/ajey091/1ff32d28671ea8baf5534b8af2cc3cc2.js"></script>

![Image3](/assets/images/Image3.png)

I am suspecting that a large percentage of violations that happen on Fridays are drunk driving violations.

## How does Age play a role?

Let's also look at the ages of violation. We can expect younger people to commit more traffic violations due to lack of experience.

<script src="https://gist.github.com/ajey091/059e17223f72fe7d1b9dec46c309b891.js"></script>

![Image4](/assets/images/Image4.png)

It is interesting to note that there is almost a bimodal distribution of violations, with one peak around the 21 year old mark and another at the 44 year mark.

We can also bin the data into different age groups to help further analysis.

<script src="https://gist.github.com/ajey091/c03af5802134063bb4a7e73efb431f02.js"></script>

![Image5](/assets/images/Image5.png)

## Speeding violations

Next, let's take a closer look at the speeding stats. For this, we will find all violations that have the phrase 'speed' in them.

<script src="https://gist.github.com/ajey091/86482b57ff9cd56d222f0631b78523da.js"></script>

## Speed statistics from traffic cameras

In order to look a closer look at the speeds as observed by traffic cameras, I looked at the public dataset provided by the NYCDOT's Traffic Management Center. This data is downloaded from [https://data.cityofnewyork.us/Transportation/Real-Time-Traffic-Speed-Data/qkm5-nuaq](https://data.cityofnewyork.us/Transportation/Real-Time-Traffic-Speed-Data/qkm5-nuaq). This is a fairly large dataset with millions of data points. They also provide geographical data with which we can get maps of speeding as well. We will read in the data and plot out the observed speed values based on the latitudes and longitudes of the speeds. We consider speeds of over 65 mph for plotting.

<script src="https://gist.github.com/ajey091/032eb3e1ebd356bf31fe3b04c4565888.js"></script>

![Image6](/assets/images/Image6.png)

<script src="https://gist.github.com/ajey091/6a05b9f8028c00f027fce1815adfdcc7.js"></script>

![Image7](/assets/images/Image7.png)

This map gives a distribution of the speeding violations (>65 mph) as measured by the traffic cameras. The sizes of the circles represent the speed.

## Conclusion

So there were some interesting observations made here. But this remains a preliminary analysis. More to come soon!
