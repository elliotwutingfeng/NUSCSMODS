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

## Known variance case
Confidence interval for mean with

- Known variance case

![2334_6_12.PNG]({{site.baseurl}}/img/2334_6_12.PNG)
![2334_6_13.PNG]({{site.baseurl}}/img/2334_6_13.PNG)


# Sample size for estimating mean

> How big the sample must i get in order to get inference? -> Depends

![2334_6_14.PNG]({{site.baseurl}}/img/2334_6_14.PNG)

![2334_6_15.PNG]({{site.baseurl}}/img/2334_6_15.PNG)

> This is to get the sample size

![2334_6_16.PNG]({{site.baseurl}}/img/2334_6_16.PNG)


- If e is small, then n will be big.
- if n is big, e will be big


> This is the same as saying that if the variance is big, we need a larger sample size in order to achieve a higher level of confidence

*E.g 1*

- Mean of CAP of random sample of 36 seniors is 3.5
- muel is 0.3 
i) find the confidence interval for the mean of the entire seniors

> We can just sub in the fomula

![]({{site.baseurl}}/img/2334_6_17.PNG)![2334_6_17.PNG]({{site.baseurl}}/img/2334_6_17.PNG)


ii) How large a sample is required if we want to be 95 percent confidence that our estimate of u is off by less than 0.05?

![2334_6_18.PNG]({{site.baseurl}}/img/2334_6_18.PNG)

## Unknown Variance case

![2334_6_19.PNG]({{site.baseurl}}/img/2334_6_19.PNG)
![2334_6_20.PNG]({{site.baseurl}}/img/2334_6_20.PNG)

- We are thinking of small sample size (n<30)

![2334_6_21.PNG]({{site.baseurl}}/img/2334_6_21.PNG)

1. Point estimate
2. Construct an interval: some multiple of the sd


For large n,
![2334_6_22.PNG]({{site.baseurl}}/img/2334_6_22.PNG)

*E.g 1*
![2334_6_23.PNG]({{site.baseurl}}/img/2334_6_23.PNG)

*E.g 2*

![2334_6_24.PNG]({{site.baseurl}}/img/2334_6_24.PNG)
![2334_6_25.PNG]({{site.baseurl}}/img/2334_6_25.PNG)

- The population is the customers that uses credit card
- u, the avf amount spent on their first visit to the chain's new store in the mall

> We are interested in certain characteristic of the individual which is the amount spent

-> We assume that they follow a normal distribution

- Since n is large, we use z value instead of t-value

A 90 percent confidence interval for the mean is given by:

![2334_6_26.PNG]({{site.baseurl}}/img/2334_6_26.PNG)

![2334_6_27.PNG]({{site.baseurl}}/img/2334_6_27.PNG)


# Confidence intervals for the difference between two means

We normally like to look at the difference. It does not matter which mean is one or two, we can swap accordingly

- Assume have 2 population with u1 and u2 and varaince a1 and a2

Then 

     Xspa1 - Xspa2

is the point estimator of u1 - u2

## Known variances

![2334_6_30.PNG]({{site.baseurl}}/img/2334_6_30.PNG)


![2334_6_28.PNG]({{site.baseurl}}/img/2334_6_28.PNG)

![2334_6_29.PNG]({{site.baseurl}}/img/2334_6_29.PNG)

## Large Sample C.L for unknwon variance
![2334_6_31.PNG]({{site.baseurl}}/img/2334_6_31.PNG)
![2334_6_32.PNG]({{site.baseurl}}/img/2334_6_32.PNG)

> We use s1^2 because we trying to use the best known


*E.g 2*

![2334_6_33.PNG]({{site.baseurl}}/img/2334_6_33.PNG)
![2334_6_34.PNG]({{site.baseurl}}/img/2334_6_34.PNG)
![2334_6_35.PNG]({{site.baseurl}}/img/2334_6_35.PNG)


## Unknown but equal variances

> We can still apply the t distribution

![2334_6_36.PNG]({{site.baseurl}}/img/2334_6_36.PNG)
![2334_6_37.PNG]({{site.baseurl}}/img/2334_6_37.PNG)
![]({{site.baseurl}}/img/2334_6_38.PNG)

> We can use chi - square (they are independent)

![2334_6_39.PNG]({{site.baseurl}}/img/2334_6_39.PNG)
![2334_6_40.PNG]({{site.baseurl}}/img/2334_6_40.PNG)


### Unknwon but equal variance for large sample

![2334_6_41.PNG]({{site.baseurl}}/img/2334_6_41.PNG)


Just check these conditions:

1) Approximately normal
2) Equal variance

> This will give us a range for u1 - u2

# Confidence interval for variance and ratio of variance
