---
title: "A quick guide to fetching data from a web API (Restaurant data)"
date: "2018-12-19"
categories: 
  - "data-science"
  - "python3"
  - "text-analysis"
  - "web-api"
tags: 
  - "json"
  - "requests"
  - "urllib"
coverImage: "restaurant-food-salat-2.jpg"
---

A common hiccup that we are faced with regularly is being unable to find the menu of a restaurant that we are interested in. How cool would it be to have a spreadsheet/database of all the items on the menu in all the restaurants near you? There are several popular web APIs for restaurant data such as [Zomato API](https://developers.zomato.com/api), [Yelp API](https://www.yelp.com/developers), [Eatstreet API](https://developers.eatstreet.com/). In this post, we will be using Eatstreet API to get the menu of all restaurants in an area.

Note that each API request will need a key for which you need to sign up on the Eatstreet webpage. We will start off by loading the required libraries. We will use the standard library in Python 3 `urllib.request` to [read the URL](https://docs.python.org/3/library/urllib.request.html#urllib.request.urlopen). Also, we will use the `json`  library to read the data in the URL. Then, we will define a function to read in the address and city. First in this function, we will obtain all the restaurants in the given address (which is stored in `data`). Then, we need to loop through all the restaurants and read the items on the menu in each restaurant.

```
import urllib.request
import json
def locu_search(address,city):
    api_key = 'MY_API_KEY'
    url = 'https://api.eatstreet.com/publicapi/v1/restaurant/search?method=both&access-token=' + api_key
    address_mod = address.replace(' ', '+')
    city_mod = city.replace(' ','+')
    final_url = url + "&street-address=" + address_mod + "," + city_mod
    with urllib.request.urlopen(final_url) as url1:
        json_obj = url1.read()
    data = json.loads(json_obj)

# Looping through all the restaurants in data
    for item in data['restaurants']:
    print ('\t\t' + item['name'] + '\n')
    restaurantkey = item['apiKey']
    menuurl = 'https://api.eatstreet.com/publicapi/v1/restaurant/' + restaurantkey + '/menu?includeCustomizations=false&access-token=' + api_key
    with urllib.request.urlopen(menuurl) as url2:
        json_obj = url2.read()
    # json_obj = urllib3.urlopen(menuurl)
    menudata = json.loads(json_obj)
    for item in menudata:
        print(item['name'].upper())
        for item2 in item['items']:
            print(item2['name'])
```

Now, we just need to call the defined function with an address and city. I will just use my university address for this.

```
locu_search('701 W Stadium Ave','West Lafayette')
```

The output of this gives a long list of items on the menu in each restaurant. A small snippet of the output is shown below:

> Sushi Don
> 
> SUSHI DON ROLL - VEGETARIAN SUSHI ROLL Avocado Asparagus Tempura Kampyo Kappa Oshinko Shiitake A & C Roll Sweet Potato Well-being Seaweed Salad Roll SUSHI DON ROLL - COOKED SUSHI ROLL California Ebi Tempura Eel love avocado Philadelphia Salmon Skin Spicy California Spicy Squid Tamago Eel love cucumber Kani Tempura

Note that this also gives us the individual components in each menu item, which I think is fantastic for someone who is picky about food (like I am).
