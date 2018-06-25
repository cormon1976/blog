---
title: "Python Dictionaries"
date: 2018-01-03T18:33:53Z
draft: false
tags: [ "python", "development"]
---

## Introduction.

 Dictionaries in python are of one of the built-in data type and argueable the most useful one.

 You'll hear the name "Hash Map" and "Arrays" also relating to this data structure.

In essence a dictionary or dict is a key, value pairing where each key is unique with the following construction

```python
capital_cities = {"Ireland": "Dublin", "England": "London", "Spain": "Madrid"}
```

Above is a simple dict called ```capital_cities``` that contains three keys(countries) and three values(capital city)

The curly brace is the identifer and also required for the construction of a python dictionary.

This data structure then means you can pull key and values in your code. If you have some logic in your code that reflects
a matching concept then dicts are for you. For example if you webapp had geo location based services and a user on your
site(which ranks capital_cities for social events then the dict above could be used to pull out the capital_city based on
country ip address , a contrived example but you get the idea.

## Basic Operators

To ```add``` a new key, value pair to the dict do the following.

```python
In [14]: capital_cities['France'] = 'Paris'
In [19]: capital_cities
Out[16]: {'England': 'London','France': 'Paris',
          'Ireland': 'Dublin','Spain': 'Madrid'}
```

To ```del``` a  key, value pair from  the dict use the ```del``` operator

```python
In [18]: del capital_cities['France']
In [19]: capital_cities
Out[19]: {'England': 'London', 'Ireland': 'Dublin', 'Spain': 'Madrid'}
```

Check if a key exists in a given dictionary by using the ```in``` operator like
this which returns a boolean True/False ,you should always check the existance
of a key in your dict to ensure you don't get any key exceptions.

```python
In [5]: 'Ireland' in capital_cities
Out[5]: True

In [8]: In [5]: 'Italy' in capital_cities
Out[8]: False

```
Use ```len``` to determine the number of entries in a dictionary

```python
In [9]: len(capital_cities)
Out[9]: 3
```

## Data Retrival  

Pulling data out of dict's is pretty easy and dict comes with a whole set of
 methods attached.

When you ```know the key and want the assiocated value``` simply do the following.
 When/where possible use this instead of for loops.

```python
In [10]: capital_cities['England']
Out[10]: 'London'
```

When you simply want all the ```keys``` in the dict use a simple for loop.
It is so common to iterate over the keys in a dictionary that we can omit the
keys method call in the for loop — iterating over a dictionary implicitly
iterates over its keys, we are not using the keys keyword here we are simply
giving it a more accurate name ```country```.

```python
In [15]: for country in capital_cities:
    print " {} is in the dict ".format(country)
   ....:     
 England is in the dict
 Spain is in the dict
 Ireland is in the dict  
```

When you simply want all the ```values``` in the dict use a simple for loop
calling out the values as the desired return element.

```python
In [14]: for listed_cities in capital_cities.values():
    print " {} is in the dict ".format(listed_cities)
   ....:     
 London is in the dict
 Madrid is in the dict
 Dublin is in the dict

```

When you want all the ```keys and all the values``` you can use  ```.items()```
which will pull all key-value pairs from a dictionary into a list of
tuples.

```python
In [16]: print capital_cities.items()
[('England', 'London'), ('Spain', 'Madrid'), ('Ireland', 'Dublin')]
```
or looping over them like so

```python
In [21]: for country, capital in capital_cities.items():
    print "The capital of {} is {}" .format(country, capital)
   ....:     
The capital of England is London
The capital of Spain is Madrid
The capital of Ireland is Dublin
```

## Merging/Sorting

To ```merge``` two or more dicts together, use the update method like so.


```python
In [18]: european_capital_cities = {"Ireland": "Dublin", "England": "London", "Spain": "Madrid"}

In [19]: middleast_capital_cities = {"Iran": "Tehran", "Turkey":"Ankara"}

In [20]: global_capitals = {}

In [21]: for city in [european_capital_cities, middleast_capital_cities]:
               global_capitals.update(city)
   ....:

In [22]: global_capitals
Out[22]:
{'England': 'London',
 'Iran': 'Tehran',
 'Ireland': 'Dublin',
 'Spain': 'Madrid',
 'Turkey': 'Ankara'}
```

To get you dict in some sort of ```sorted``` state , (they are unsorted by default) use the sorted function on the items like so.

```python

In [35]: for country, capital in sorted(global_capitals.items()):
            print country , capital
   ....:
England London
Iran Tehran
Ireland Dublin
Spain Madrid
Turkey Ankara
```

I am going to write something up on nested dicts and more complex data structures
realting to dict next , till then keep it real homies :).

