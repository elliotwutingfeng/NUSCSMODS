---
layout: post
published: true
title: 'CS3230 - Lecture 1: Recap of Assymptops'
---
# Time complexity
- worse case and average:
 - Worse: Max time that is required with input size n
 - Avg: Assume that input is distributed somewhere randomly

> Assume the finite set of inputs, we consider only contains two inputs, A1 and A2. The time needed for solving them is T1 and T2.
Avg time is (T1+T2)/2

## Asymptotic time complexity
Look at the term that grows the fastest and ignore the constant

e.g f(n) = 39m^2 +16n +5
- We will only look at n^2

#### Why ignore?
1. Growing factors are more significant
2. The cosntant is usually small for most algo

## Upper and lower bounds
![1-1.PNG]({{site.baseurl}}/img/1-1.PNG)

### Proving asymptotics using limits
![3230-1-1.PNG]({{site.baseurl}}/img/3230-1-1.PNG)

- Compute the ratio as n tends to infinite. 

![3230-1-2.PNG]({{site.baseurl}}/img/3230-1-2.PNG)


