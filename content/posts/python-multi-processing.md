---
title: "Python Multi Processing"
date: 2018-11-08T13:52:40Z
draft: false
tags: [ "python", "development"]
---

## Introduction.

This article is a brief yet concise introduction to multiprocessing in Python.

Alot of my professional work is geared towards I/O and networking operations with individual separate memory space requirements so  multiprocessing is more preferable to multithreading. This avoids the limitations of threading the main one being the global interpreter lock (GIL), which ensures that only one thread runs at a time. 

We prefer in work to take full advantage of  multicore systems, and in the world of Python that means using processes.

The _multiprocessing_ package supports spawning processes using an API similar to the threading module. It also offers both local and remote concurrency. This post will discuss multiprocessing in Python and how to use multiprocessing to communicate between processes and perform synchronization between processes.

## Basic Example

{{< gist cormon1976 1d1086c9165630d3ba85962c299f6945 >}}


In the example code above, we first import the Process class and then instantiate the process object passing in the hello_world function which we want to run in the process.

We then tell the process to begin using the start() method, and we finally complete the process with the join() method

It usually more useful to be able to spawn a process with arguments to tell it what work to do. Unlike with threading, to pass arguments to a multiprocessing Process the argument must be able to be serialized using pickle. This example passes each process  a famous person so the output is a little more interesting.


{{< gist cormon1976 8278c618d98d8bf03b90bc304a5d674c >}} 


## The Pool Class

The Pool class is used to represent a pool of worker processes. It has methods which can allow you to offload tasks to the worker processes. Let’s look at a really simple example:

{{< gist cormon1976 0c60a9fa7d623bdef579c8175530ab43 >}} 

Basically what’s happening here is that we create an instance of Pool and tell it to create three worker processes. Then we use the map method to map a function and an iterable to each process. Finally we print the result, which in this case is actually a list:

`['Hello Bob', 'Hello Alice', 'Hello Eve']`

I find the pool class easier to grasp :)

## Processes Communication

Multiprocessing supports two types of communication channels between processes **Queues** and **Pipes8**.

Which one to chose ?

To quote [this](https://stackoverflow.com/questions/8463008/python-multiprocessing-pipe-vs-queue) SO article 


`If you need more than two points to communicate, use a Queue().`

`If you need absolute performance, a Pipe() is much faster because Queue() is built on top of Pipe().`


#### Queues

Queue objects are used to pass data between processes. They can store any pickle-able Python object. The multiprocessing queue lives shared memory.

{{< gist cormon1976 e1667dfa58444fc52fd8afcbe36de5dc >}} 

In the above example, we first create a generic function simply adding in passed objects to the queue. We then instantiate a queue object and a process object and begin the process.

Finally, we check if the queue is not empty and if so we get the values from the front of the queue and print them to the console.

The queue is a First-In-First-Out data structure. 

Queues are specially useful when passed as a parameter to a Process target function to enable the Process to consume data. By using put() function we can insert data to then queue and using get() we can get items from queues. 

#### Pipes

Pipes in multiprocessing are primarily used for communication between processes. It is more of a two communication data flow. When you create a pipe it create the two ends of that pipe allowing you to send data in and receive it on the other end.

{{< gist cormon1976 f9724892abf8d67da9f0856dff50cb14 >}} 

which will produce 

`['Sending something into the pipe !!!!!!!!']`

We first create a Pipe object and name either side of the pipe return objects.

Then like in the case of of a queue I create a Process passed in a generic function but also what end of the pipe I want to send data into. 

And finally we pull out the data on the opposing end of the pipe with the `.recv()` method.