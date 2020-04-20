---
layout: post
published: true
title: ST2334 - Estimation based on normal Distribution
---

# Point estimation

## Mean and variance

- Assume that some characteristics of elements can be represented by random variable X whose pdf is fx(x,titer)

> Choose the varables for our parameters, this will give us different normal distribution


The form of pdf is assumed know except that it contains unknown parameter titer

> Parameter is just some constant for our PDF

1. Estimator: Based as a fomula on the random sample -> Can use to estimate the unknown parameter

## Estimation
1. Point estimation

> This will be always wrong, but it is good for a large sample size (Law of large number)

![2334_6_1.PNG]({{site.baseurl}}/img/2334_6_1.PNG)

2. Interval estimation

Choose an interval where the unknown can land in.

e.g Avg temperature in singapore: 28 - 30 degrees





# Parameter and statistic

A statistic is a function of the random sample which does not depend on any unknown parameters

![2334_6_2.PNG]({{site.baseurl}}/img/2334_6_2.PNG)

We can only vary the random set but we cannot involve anything that is not known to us, it cannot be use as an estimator

## Point estimate of mean

Suppose u is the population mean
- The stats that one uses to obtain a pount estimate is called estimator

e.g *X*spa is an estimator of u

The value of X, denoted by *x*spa is an estimate of u


#### E.g 1 
- Sample mean of random sample taken from population with mean u is 5
- Point estimate for the population mean u is 5

- lowercase: estimate
- Uppercase: Estimator

> Different random sample give different point estimates of u

## Interval estimation
- Define two stats like:
![2334_6_3.PNG]({{site.baseurl}}/img/2334_6_3.PNG)


This is a random interval per 2 end points where each end point is a random variable.

#### E.g 2 

Suppose a^2 is known

Let

![2334_6_4.PNG]({{site.baseurl}}/img/2334_6_4.PNG)

> Random variable has more than one variable with a probability associated with it.

> Unknown parameters are unknown constant that will not change

![2334_6_5.PNG]({{site.baseurl}}/img/2334_6_5.PNG)

Here we use xspa to determine the estimate.
If we want to find the chance where 

*p(titleL < u < titleU)* ?


# Unbiased estimator

- A statistic is said to be an unbaised of the parameter titer if

![2334_6_6.PNG]({{site.baseurl}}/img/2334_6_6.PNG)

> E(x) = u and E(xspa) = u

![2334_6_7.PNG]({{site.baseurl}}/img/2334_6_7.PNG)

![2334_6_8.PNG]({{site.baseurl}}/img/2334_6_8.PNG)
> This is a consistent estimator where n is very huge

To compare two different estimator for same parameter, we look at the unbiasness.


Estimator is good if:

- Biase is small (Not too far from para)
- Variation is not very big

> This is called mean square error



# Interval estimation
- An interval estimate of population parameter is an interval of the form

![2334_6_9.PNG]({{site.baseurl}}/img/2334_6_9.PNG)

We try to get the width of confidence interval small.


- Since different sample will yeild different titer hat

- Therefore, these end points of the interval are values of corresponding random variables 

> I take a sample and calculate many intervals. Titerlhat can be consider as a random variable.


![2334_6_10.PNG]({{site.baseurl}}/img/2334_6_10.PNG)


![2334_6_11.PNG]({{site.baseurl}}/img/2334_6_11.PNG)


> If we repeat it many times, about 95 percent of the time, it will cover



# Confidence interval for the mean
# Sample size
# Confidence intervals for the difference between two means
# Confidence interval for variance and ratio of variance
