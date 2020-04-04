---
layout: post
published: true
title: 'ST2334 - Chapter 5: Sampling and Sampling distribuitions'
---
# Population and sample

> How does each sample's avg behaves?
That is the sampling distribution

- The totality of possible outcomes or observation of a surve or experiment is populate
- Sample is a subset of population
- Every outcome or observation can be recorded as a numerical or categorical value. Thus each member of a population is a value of a random variable.


## Finite population

- Finite number of elements

e.g
1. All citizen of singapore
2. All books in science library

> Population is a collection of something that has a value and it can have more than one of these value.

## Infinite Population

- Infinite is one that consists of an infinitely (**Countable and uncountable**) large number of elements.

e.g 
1. The results of all possible rolls of a pair of dice
2. Random digits numbers taken with replacement from a sample space of 10 digits. like {0,1,2,3,4,5,6,7,8,9}

> Although they are only 10 distinct integers, there can be a replacement, thus it is infinite


3. The depths at all conceivable position of a lake
> There is infinite number of points

### Remark
Some infinite pop are so large that intheory we assume to be infinite such as the pop of lives of a certain type of storage battery.


# Random Sampling

## Simple random sample
- A set of n members takne from a given population is called a **sample** of size n
- A simple random sample of n members is a sample that is chosen in such a way that every subset of n observation of the population has the same prob of being selected

> We want to select a sample of 3 from 1,2,3,4,5,6,7,8,9,10,11,12

> We can select using 12C3 -> e.g {1,8,9}

> Each of these are equally likely of being selected

## Sampling from a finite population

1. Sampling without replacement
- In general, there are NCn samples of size n that can be drawn from a finite population of size N **without replacement**

- Each sample has an equal chance of being selected

p(select) = 1/Ncn

2. Sampling with replacement
- Using the population {A,B,C,D}, there are 4^2 = 16 samples of size 2

- There are N^n sample of size n that can be drawn from a finte pop of size N with replacement

## Sampling from an infinite population (with or without)

- It wont affect the remaining if you take one out because it is infinite.

#### E.g 1
- 15 tosses of a coin with the hypothetical infinite population as the result
- If prob of getting heads is the same 
- 15 tosses are independent

-> Therefore, the sample is random
> Each of these values are independent and has an even distribution

> The joint distribution is equal to the product of the joint marginal for each values.

1) same prob of being selected
2) Independent

#### E.g 3
- Consider the pop of the sum of all possible rolls of a pair of dice
- the population is consider to be infinite
- We choose a random sample of size n from a random variable X having probability function given by

![2334_5_2.PNG]({{site.baseurl}}/img/2334_5_2.PNG)

> is infiite cos we can roll the dice many times

- To obtain a random size of size 100, we simply roll the pair of dice 100 times independently under the same conditons
- If xi represent the result on the ith roll, we then obtain x1,x2,x100
- All these are random variables with the same prob/same distribution as the population variable X

> no matter is what roll, the outcome will follow the same distribution

### Definition
- Let X be random variable with prob distribution
- Let x1,x2.. xn be n independent random variables each having the same distribution as X
- then x1,x2..xn is called a random sample of size n from a population with distribution fx(x)


# Sampling distribution of sample mean

- Selecting random sample to elicit infomation about unknown population parameters

e.g we just toss a coin

fx(x) = p^x * (1-p) ^ (1-x) * x 

> We draw inference from a subset of a population

- We want to know the proportion of people in singapore who prefer a certain brand of coffee

- A large random sample is then selected from the population and the proportion of this sample favouring the brand of coffee in question is calculated

> All these answer being correct or incorrect, they are all answer since we are selecting a random sample

## Statistic and sampling distribution

- A function of a random sample is call statistic

> A function is when we have one value mapped to another value

- A statistic is also called a random variable
- The prob distribution of a statstic is called a **sampling distribution**

## Sample mean

![2334_5_3.PNG]({{site.baseurl}}/img/2334_5_3.PNG)

> This is the realisation of the statistic

> This happen wehen the values in the random sample is observed

#### E.g 1
- Consider a discrete uniform population
- 3,5,7,9,11
- Population N = 5

Hence, fx(X) = 1/5

- The population mean 
![2334_5_4.PNG]({{site.baseurl}}/img/2334_5_4.PNG)

> Note: Mean is not the average, we must use the fomular

v(xspa) = v(x) / n

E(xpa) = e(x) 

> The variation of xpa is smaller than the variation of x. Because variance of xspa is v(x) * n. If n is a big number, then the varation of xspa is close to 0 compared to v(x) 

## Theorem
- FOr random samples of size n taken from infinite population or finite with replacement, having population mean (u)and population deviation(sigma)

![2334_5_5.PNG]({{site.baseurl}}/img/2334_5_5.PNG)

## Law of large number
> The number is very big

![2334_5_6.PNG]({{site.baseurl}}/img/2334_5_6.PNG)

-> Seems to tend to 0 when n is big

#### Remark:
- The sample size increase, the prob that the sample mean differes from the population mean tends to 0



# Central Limit theorem and its application
# Sampling distributions of difference of two sample means
# chi square distruution
# Sampling distribution of (n-1)S^2 / ![2334_5_1.PNG]({{site.baseurl}}/img/2334_5_1.PNG)

# t-distribution
# F-distribution
