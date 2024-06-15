---
title: "Word Cloud of song lyrics"
date: "2019-09-07"
categories: 
  - "data-science"
  - "python3"
  - "web-api"
tags: 
  - "text-analysis"
  - "word-cloud"
coverImage: "aboveandbeyond_16.01.13_nyc_f1-3m-e1567869347881.jpg"
---

_Update: I recently made a [post](https://ajeyvenkataraman.com/2020/06/01/word-cloud-of-song-lyrics-revisited/) with a more generic version of the code in this post with the intention of more robustness and flexibility._ 

Something that really gets me going is music, and more recently electronic music. One of my favorite artists of all time is Above & Beyond. Their music moves me deep down inside. They always seem to have the right lyrics for any and every occasion. There's something profoundly fitting about their music and words.

So, I decided to write a quick program to get all their song lyrics from a generic lyrics website and then make a word cloud out of it. Just to clarify, a word cloud (also called a tag cloud) is a technique of visualizing text data in free form such that the size of each word is proportional to the frequency of its occurrence. With music and data analysis coming together, if there was a project that was tailor-made for me, this would be it! I used   `requests`, `lxml` and `BeautifulSoup` libraries to accomplish this. I scraped the data from a popular lyrics website [azlyrics](http://www.azlyrics.com) (thanks guys!). And then used a popular wordcloud python module to prepare a wordcloud.

We will now get down to the coding aspects. Firstly, we will import the relevant modules.

```
import requests
```

The basic idea now is the following

1. Get to the page with the list of Above & Beyond song names
2. Get the URLs for the lyrics
3. Open the URL for each song
4. Get the text corresponding to lyrics on each page (ignore everything else)
5. Copy all the lyrics to a final single string
6. Use this said string to create the word cloud.

Code for some of these steps below:

<script src="https://gist.github.com/ajey091/d164c50b864a300799c6b82b44107e45.js"></script>

Some important points to note about the above snippet of code (which is rather dense):

- Line 1: this link gives the list of all the songs of A & B that the website provides the lyrics to.
- On line 4, we are asking BeautifulSoup to get all the links on the page which has 'abovebeyond' in the link. This is to ignore all other links on the page that do not correspond to song lyrics.
- We are doing some manipulation of the obtained link on line 6 to get the absolute URL for the lyrics page.
- The rest of the code is all about getting the lyrics in a formatted string, which will then be fed to the wordcloud module.

Now, we have all the lyrics in the `all_lyrics` string. We can now just feed in this string to the `wordcloud` [module](https://github.com/amueller/word_cloud) and witness the magic!

```
wordcloud = WordCloud(max_font_size=50, max_words=300, background_color="white").generate(all_lyrics)
```

I had to try a few variants to get it looking the way I wanted it to. But I show below a couple of good ones I could achieve.

![ABwordcloud2](/assets/images/abwordcloud2-e1567873332668.png)

![ABwordcloud](/assets/images/abwordcloud.jpg)

I have to admit that I am quite thrilled with the result. I know for a fact that my fellow Above & Beyond fans will absolutely love looking at this. This was a lot of fun to make as well!

**References**

- https://github.com/elmoiv/AZLyricsAPI
- https://www.wordclouds.com/
