---
title: "Word cloud of song lyrics (revisited)"
date: "2020-06-01"
categories: 
  - "python3"
  - "web-api"
tags: 
  - "python"
  - "requests"
  - "text-analysis"
  - "word-cloud"
---

I am surprised to learn that a [quick fun post](https://ajeyvenkataraman.com/2019/09/07/word-cloud-of-song-lyrics/) in the last year has turned out to be the most popular post of my website. It is my attempt here to provide some code to generalize the approach followed in the previous post. Specifically, in the previous post, I only created a word cloud for song lyrics of a particular song. Here, I am extending that to include any song of user's choice. The extension is fairly straightforward. Following are the adopted steps:

- Make a call to a web API to a song lyrics website - here, we choose a free website called [Canarado Lyrics.](https://rapidapi.com/canarado/api/canarado-lyrics)
- We parse the input song and artist names, and obtain the lyrics.
- Further, we parse the lyrics text to make some formatting changes.
- Then we use the robust [Wordcloud](https://github.com/amueller/word_cloud)  package to create a wordcloud.

The code for the above steps is given below:

<script src="https://gist.github.com/ajey091/5a576b351d344dd0ec66e49c16925441.js"></script>

There are two ouputs - raw text of the lyrics (a snippet is shown below) and the wordcloud.

> ".... shamone lay it on me, all right i'm giving you on count of three to show your stuff or let it be i'm telling you just watch your mouth i know your game what you're about well they say the sky's the limit and to me that's really true but my friend you have seen nothing just wait til i get through because i'm bad, i'm ...."

![WordCloud_MJ_bad](/assets/images/wordcloud_mj_bad.png)

The above is just the most basic version of the wordcloud output. There are plenty of possible modifications that can be made to get creative with the output wordcloud - some examples given [here](https://github.com/amueller/word_cloud/tree/master/examples).
