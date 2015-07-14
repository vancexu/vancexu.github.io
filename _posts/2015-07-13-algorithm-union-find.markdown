---
layout: post
title:  "[Algs4] Union Find"
date:   2015-07-13 
tags: [mooc, algorithm]
---
This post introduces a simple data structure called **Union Find**. If you wonder how Facebook/LinkedIn know whether people A and B may know each other through some common friends, you can figure it out by reading on :)

## Problem: Dynamic Connectivity
Given a set of N objects, we want to:  
1. **Union command**: connect two objects.  
2. **Find/connected query**: is there a path connecting the two objects?

As shown in the following GIF, there are N=10 objects, we do 5 unions and then check object[0] and object[7] are not connected, object[8] and object[9] are connected. After 4 more unions, object[0] and object[7] are connected.

![Dynamic Connectivity]({{ site.baseurl }}/images/2015-07-13/dynamic-connectivity.gif){: .center-image}

Another example below: it's hard for human to figure out whether point p and q are connected or not, we need computer to do that.

![Connectivity Example]({{ site.baseurl }}/images/2015-07-13/connectivity-example.png){: .center-image}

As you can guess, there are many applications on this:  
* Friends in a social network  
* Pixels in a digital photo  
* Computers in a network  
* Transistors in a computer chip  
* Metallic sites in a coposite system  

When programming, it's convenient to name objects 0 to N-1. Because:
* Use integers as array index
* Suppress details not relevant to union-find. (can use symbol table to translate from site names to integers)

We assume connectivity is an equivalence relation, which is reflexive, symmetric, and transitive.

Then we define **Connected Components**: Maximal set of objects that are mutually connected. Example below.

![Connected Component]({{ site.baseurl }}/images/2015-07-13/connected-component.png){: .center-image}
 
### Union-find data type (API) 
Our goal is: Design efficient data structure for union-find.  
* Number of objects N can be huge
* Number of operations M can be huge
* Find queries and union commands may be intermixed.

![union-find API]({{ site.baseurl }}/images/2015-07-13/uf-api.png){: .center-image}

## Quick Find


