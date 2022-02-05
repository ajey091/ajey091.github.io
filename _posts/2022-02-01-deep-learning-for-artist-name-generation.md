---
title: "I built a web app to generate artist/names using Deep Learning"
date: "2022-02-01"
categories:
  - "machine-learning"
  - "python3"
  - "text-analysis"
tags:
  - "deep-learning"
  - "flask"
  - "heroku"
  - "lstm"
  - "text-generation"
---

At the height of a snowy Chicago winter and in the midst of another wave of the pandemic, a recent hobby I have picked up has been mixing songs using a DJ controller. It has been a deeply engaging activity and I have been uploading mixes to [my soundcloud](https://soundcloud.com/ajey-venkataraman) (unabashed self-promotion). However, one challenge I have faced is to come up with an artist/DJ name - there are too many factors to consider and most obviously good ideas are already taken. So I tried to delegate the task to a deep learning algorithm. While generative models are exciting, they typically require large amounts of data to train, and they are time and resource intensive; they are still in their nascent stages at this point.

## The Idea

The basic idea is to train a deep learning model to learn the structure in a provided corpus of words. We will invoke already trained Long Short Term Memory networks ([LSTMs](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)), a special kind of recurrent neural networks that are capable of learning long-term dependencies. LSTMs typically work very well for understanding the structure behind language (words and sentences) and are hence commonly used in machine translation and speech recognition. The following is an itemized list of the steps we will follow:

1. We will find sources of data on the internet about previous artist names
2. Train the LSTM model to learn the structure and patterns behind these artist names
3. Ask the trained model to generate new names
4. Use `Flask` to serve the model
5. Host the model on a `Heroku` web server

## Data collection and cleanup

I used two different data sources as input to the LSTM model, which I combined to train the model - the first dataset is from the [MusicBrainz](https://musicbrainz.org/) database which consists of over 1.4 Million musical artists. The second dataset is from scraping the Wikipedia page for the [list of club DJ names](https://en.wikipedia.org/wiki/List_of_club_DJs) using [BeautifulSoup](https://beautiful-soup-4.readthedocs.io/en/latest/).

<script src="https://gist.github.com/ajey091/20d27a66db56f58979c2d8785772a062.js"></script>

<!-- \[gist https://gist.github.com/ajey091/20d27a66db56f58979c2d8785772a062\] -->

We also clean up the data we obtain from the MusicBrainz website - specifically, we will only choose names from english-speaking countries and keep only alphabets.

<script src="https://gist.github.com/ajey091/8d7a62f59256fd9b678c5cafcec0a397.js"></script>

<!-- \[gist https://gist.github.com/ajey091/8d7a62f59256fd9b678c5cafcec0a397\] -->

We then append the two sources of data and feed into the model.

## Model

There are already excellent trained LSTM models for text generation on the internet - there is no point in reinventing the wheel. We will invoke the [startup-name-generator (sng)](https://github.com/AlexEngelhardt/startup-name-generator) model. We will train this model on the dataset that we generated in the previous step. The training takes a few tens of minutes; the time taken for generation of words is proportional to the number of words we request - on my local machine, the trained model took about 3 seconds for every 10 words. This might be a problem when we deploy it to the web server, we will address this issue in the next section.

<script src="https://gist.github.com/ajey091/6f2d1d203d99ab9dc9d6f259bb9509d7.js"></script>

<!-- \[gist https://gist.github.com/ajey091/6f2d1d203d99ab9dc9d6f259bb9509d7\] -->

## Serving with Flask

We will use the pickled model to make generations for a number requested by the user and host it on a local server. We will create a file `app.py`:

<script src="https://gist.github.com/ajey091/84b7695c33a59fbd2bac1414e18f0026.js"></script>

<!-- \[gist https://gist.github.com/ajey091/84b7695c33a59fbd2bac1414e18f0026\] -->

We will use a simple, standard html template for our endpoint.

<script src="https://gist.github.com/ajey091/cb5794a1458ef48dbf1694ec92acb71d.js"></script>

<!-- \[gist https://gist.github.com/ajey091/cb5794a1458ef48dbf1694ec92acb71d\] -->

When we run `app.py`, we will be able to see our artist name generation file at `http://127.0.0.1:5000/`.

## Web hosting with Heroku

Heroku is a web hosting platform that easily integrates with Flask. The basic idea is to host whatever we have running on our local server to a URL on the web. Firstly, we need to create a virtual environment and install dependencies:

```
python3 -m venv venv
source venv/bin/activate
(venv) > pip install flask gunicorn sng
(venv) > pip freeze > requirements.txt
(venv) > less requirements.txt
click==8.0.3
Flask==2.0.2
gunicorn==20.1.0
itsdangerous==2.0.1
Jinja2==3.0.3
MarkupSafe==2.0.1
numpy==1.22.1
pandas==1.4.0
python-dateutil==2.8.2
pytz==2021.3
six==1.16.0
sng==0.3.2
Werkzeug==2.0.2
```

Next, we get into hosting on Heroku. This process is fairly, simple although getting it to actually work the first time is sometimes challenging. First we need to create a `Procfile` inside the main folder with just one line:

`web: gunicorn app:flask_app`

Then we create a free account on [Heroku](https://dashboard.heroku.com/).

```
(venv) > git init
(venv) > heroku login
(venv) > git add .
(venv) > git commit -m "first commit"
(venv) > git push heroku main
```

The `heroku login` command takes you to the login page, where we have to enter our credentials.

The final command above takes a while to finish, since we are uploading not only our files but also installing the dependencies on the remote server. Once we're done with that step, we should see our application hosted on the web server. My website is hosted at:

[https://generate-djnames.herokuapp.com/](https://generate-djnames.herokuapp.com/)

Note that you will be initially assigned a random URL, which you can easily change in the Heroku dashboard.

An important consideration is that running our app on a web server takes significantly more time than running on our local machine because of all the overhead. When I was testing this app, my generation step would constantly time out. The way I overcame this issue was by requesting a large number (100K) of generations during the training phase and caching the results in a text file. Then, on our web server, we can just randomly sample from the text file, which is much faster.

Here is a snippet of the output:

![](https://ajeyvenkataraman.files.wordpress.com/2022/02/image.png?w=862)
