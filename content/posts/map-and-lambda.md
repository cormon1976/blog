---
title: "Python Map and Lambda"
date: 2018-06-28T21:42:45+01:00
draft: false
tags: [ "python", "development"]
---

## Introduction to Lambdas


One of the guys in my team in work loves Lambda functions. I often have to do a double take on the code logic relating to these 
little beauties so here is a quick post on lambdas and maps.

lambda is just a shorthand to create an anonymous function. It's often used to create a one-off function (usually for scenarios when you need to pass a function as a parameter into another function). It can take a parameter or multiple parameters and it returns the value of an expression.

Python's lambda keyword in my opinions is occasionally useful. If you find yourself doing anything remotely complex with it, put it away and define a real function.

It's construction looks like this.

`lambda arguments: expression`

The one thing that always gets me is that the lambda statement does not have a return statement, it is implied. 

As a comparision, this lambda is the same as the function definition below it.

```python
In [1]: doubleaslambda = lambda x: x * 2

In [2]: print(double(5))
10
```
```python
In [14]: def doubleinafunction(x):
 return x * 2

In [15]: doubleinafunction(5)
Out[15]: 10
```

The type of the return object from a lambda is a function. 

```python
[21]: type(doubleaslambda)
Out[21]: function
```

This reiterates the point that lambda functions are passed as parameters to functions which expects a function object as a parameter like _map_, _reduce_, _filter_ functions among one you can define yourself.

# map 

__map__ functions expect a function object and any number of iterables like list, dictionary, etc. It executes the function_object for each element in the sequence and returns a list of the elements modified by the function object.

Here is an example using a regular function:

```python

In [56]: cities = ['Paris', 'Madrid', 'Dublin']

In [57]: def printcities(city):
 ...: return "I am in " + str(city)

In [58]: map(printcities, cities)
Out[58]: ['I am in Paris ', 'I am in Madrid', 'I am in Dublin']
```

Here are some examples using a lambda function this is essentially the objective of this post using lambdas and map together as a paradigm.

### Pass in a list 

```python
In [63]: cities = ['Paris ','Madrid','Dublin']
In [63]: map(lambda x : "I am in city " + str(x), cities)
Out[63]: ['I am in city Paris ', 'I am in city Madrid', 'I am in city Dublin']
```
```python
capital_cities = {'England': 'London','France': 'Paris', 'Ireland': 'Dublin','Spain': 'Madrid'}
```

### Pass in a dictionary 

```
In [99]: capital_cities = {'England': 'London','France': 'Paris', 'Ireland': 'Dublin','Spain': 'Madrid'}

In [100]: map(lambda x: x, capital_cities.keys())
Out[100]: ['England', 'Spain', 'Ireland', 'France']

In [101]: map(lambda x: x, capital_cities.values())
Out[101]: ['London', 'Madrid', 'Dublin', 'Paris']

```