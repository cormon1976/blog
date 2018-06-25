---
title: "Advanced Python Dictionaries"
date: 2018-01-03T18:33:53Z
draft: false
tags: [ "python", "development"]
---
## Introduction.

In my previous post I talked about the constructs and various methods and data retrival mechanisms that are available when using a python dictionary.

This post is going to cover some more advanced dictionary topics.

## A list of dicts.

If we had a list of two  dicts like this

```python
In [6]: capital_cities = [{"Ireland": "Dublin", "England": "London", "Spain": "Madrid"},{"Iran": "Tehran", "Turkey":"Ankara"}]

In [7]: capital_cities                                                                               
Out[7]:[{'England': 'London', 'Ireland': 'Dublin', 'Spain': 'Madrid'}, {'Iran': 'Tehran', 'Turkey': 'Ankara'}]
```

I always find the best way to approach a data structure that is more complex is to study it closely and dissect it piece by piece until you are clear on what type of data structure you are dealing with.

In out capital_cities examples starting from the outside confirm the data structures
with the ```type``` command

 ```python
 In [8]: type(capital_cities)
 Out[8]: list

 ```
so we have a list how we find out what data structures are inside the list we can loop over the elements and pass the elements to ```dir```

```python
In [13]: for elements in capital_cities:
            print type(elements)
   ....:
<type 'dict'>
<type 'dict'>

```

Cool so we have a list contains dicts , we can now go ahead and apply iteration on these structures like so. First a for loop over the list and then a for loop over the dicts.

```python
In [17]: for elements in capital_cities:
            for key , value in elements.items():
               print 'nested keys are {} , nested values are {} '.format(key, value)
   ....:
nested keys are England , nested values are London
nested keys are Spain , nested values are Madrid
nested keys are Ireland , nested values are Dublin
nested keys are Turkey , nested values are Ankara
nested keys are Iran , nested values are Tehran
```

## Dictionary Comprehensions

On top of list comprehensions, Python now supports dict comprehensions, which allows you to express the creation of dictionaries at runtime using a concise syntax.

You should ensure that you never makes them too complex and as a rule of thumb create a new dict from the output of the logic within the dictionary comprehension.

A dictionary comprehension takes the form `{key: value for (key, value) in iterable}` This syntax was introduced in Python 3 and backported as far as Python 2.7.

In the below example we are constructing a dictionary based on two lists , this is just in keeping with our theme of capital cities. We then use a dict conprehension (and `zip`)to construct the dict using form  `{key: value for (key, value) in iterable}`. This is cretainly a more concise way of writing control logic statements.

```python

In [12]: capitals = ["Dublin", "London", "Tehran"]

In [13]: countries = ["Ireland", "England", "Iran"]

In [10]: {k: v for (k, v) in zip(countries, capitals)}

In [14]: combinations = {k: v for (k, v) in zip(countries, capitals)}

In [14]: combinations

Out[14]: {'England': 'London', 'Iran': 'Tehran', 'Ireland': 'Dublin'}

```

A future example is below. Here we are just setting all the values in an existing dictionary with a comprehension and assigning the output
to a new dictionary called `sunny`.

```python

In [28]: capital_cities = {"Ireland": "Dublin", "England": "London", "Spain": "Madrid"}

In [26]: sunny = {key: 'Sunny Weather Forecasted' for key, values in capital_cities.items()}

In [27]: sunny
Out[27]:
{'England': 'Sunny Weather Forecasted',
 'Ireland': 'Sunny Weather Forecasted',
 'Spain': 'Sunny Weather Forecasted'}

```
