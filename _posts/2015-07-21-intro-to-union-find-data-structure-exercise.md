---
layout: post
title:  "Intro to Union-Find Data Structure, Exercises"
date:   2015-07-21 
tags: [mooc, algorithm, exercises]
---

Let's use union-find data structure to solve some problems in this post. (To learn what is union-find, please read [previous post](http://vancexu.github.io/2015/07/13/intro-to-union-find-data-structure.html).)

## Question 1
**Social network connectivity.** Given a social network containing N members and a log file containing M timestamps at which times pairs of members formed friendships, design an algorithm to determine the earliest time at which all members are connected (i.e., every member is a friend of a friend of a friend ... of a friend). Assume that the log file is sorted by timestamp and that friendship is an equivalence relation. The running time of your algorithm should be MlogN or better and use extra space proportional to N.

**Solution:** This can be easily done by adding a `count` for number of connected component. Regard N members as N objects, regard M timestamps as M unions. Then *"the earliest time at which all members are connected"* is the time when the number of connected component is equal to 1. 

[Sample Code](https://github.com/vancexu/Algs4/blob/master/JobInterviewQuestions/1.1_union_find/WeightedQuickUnionUF.java)

## Question 2
**Union-find with specific canonical element.** Add a method find() to the union-find data type so that find(i) returns the largest element in the connected component containing i. The operations, union(), connected(), and find() should all take logarithmic time or better.

For example, if one of the connected components is {1,2,6,9}, then the find() method should return 9 for each of the four elements in the connected components.

**Solution:** Add another int array `large[]` where large[i] is the largest element in component contains object i. When union, update large array. 

[Sample Code](https://github.com/vancexu/Algs4/blob/master/JobInterviewQuestions/1.1_union_find/UFWithFindLargest.java)

## Question 3
**Successor with delete.** Given a set of N integers S={0,1,...,N−1} and a sequence of requests of the following form:

* Remove x from S
* Find the successor of x: the smallest y in S such that y≥x.

design a data type so that all operations (except construction) should take logarithmic time or better.

**Solution:** I know it's hard to believe this one can be solved by Union-Find. But take a look at the time constrain, and think about how you can use union-find here, you will soon figure out the `UFWithFindLargest` we created for Question 2 is super helpful. When a number is removed, union the immediate neighbor if it is also removed. Then the largest successor is equal to the largest number in that component plus 1.

[Sample Code](https://github.com/vancexu/Algs4/blob/master/JobInterviewQuestions/1.1_union_find/SuccessorWithDelete.java)


## Question 4
**Percolation.** This final question is a programming assignment with specification described [here](http://coursera.cs.princeton.edu/algs4/assignments/percolation.html).

Basically, the question is: 

Given a N-by-N grid of sites. Each site is either open or blocked. A full site is an open site that can be connected to an open site in the top row via a chain of neighboring (left, right, up, down) open sites. We say the system percolates if there is a full site in the bottom row. In other words, a system percolates if we fill all open sites connected to the top row and that process fills some open site on the bottom row.

**Solution:** We can easily transform the 2D grid to a 1D union-find to solve this problem. But how can we take constant number of calls to union-find methods to support `isFull` and `percolates`?

By adding virtual nodes. At the top of the first row and the bottom of the last row, add two nodes, and union them with those rows. Then to check `isFull(i)`, you only need to check whether i is connected to the top virtual node (rather than each node of the first row). Similar for `percolates`. 

However, you will soon notice that this solution will cause a back wash issue, which means unfull sites being treated as full. Why back wash happens? Becuase the top and bottom virtual nodes are unioned (in same component). So how to solve it? We use two union-find with 1 virtual node each. One is for `isFull`, one is for `percolates`

[Sample Code](https://github.com/vancexu/Algs4/tree/master/1-percolation) (Please only use it for learning purpose, not for cheating)






