---
layout: post
published: false
title: 'ST2334 - Chapter 7: Hypothesis testing base on normal distribution'
---
# Hypotheses testing base on normal distribution

## Null and alternative hypothesis
- A statistical hypothesis is an assertion on conjecture concerning one or more populations

- Consider 2 characteristics of a population
  - Ratio
  - Mean
  - Variance
- "do not reject" and reject 

### Statistical hypothesis
The rejection of a hypo is to conclude is false

Acceptance of Hypo implies that we have insufficient evidence to believe otherwise


Because of this terminology, the statsician will often choose to state the hypo in a form that hopefully will be rejected

### Null hypothesis
- Denoted by H0
- Fomulate in hope of rejecting
- Concern a population parameter will always be stated to specify an exact value of the parameter

### Alternative Hypothesis
- Denoted by H1
- More than one values
- Rejection H0 this leads to the acceptance of alternative hypothesis denoted by H1


*E.g 1*

- We want to determine if the mean of IQ of pupils in a certain sch is different from 100
- We have H0: u = 100 against H1: u != 100

This is call two side alt

![2334_7_1.PNG]({{site.baseurl}}/img/2334_7_1.PNG)


![2334_7_2.PNG]({{site.baseurl}}/img/2334_7_2.PNG)

# Type 1 and 2 error

![2334_7_3.PNG]({{site.baseurl}}/img/2334_7_3.PNG)

> Type 1: Reject the null given that it is true
> Type 2: Do not reject the null given that it is false

Type 1 is a serious error

- Probability of committing a type 1 error is 5 percent or 1 percent, this is also known as level of significance

Type 2 is beta

## Acceptance and rejection region
- Select a suitable test statistic for parameter under hypothesis
- Once the sig level a is given, a decision rule can be found such that it divides the set of all possible values of the test statistic into two regions

1) Rejection region/critical region

2) Acceptance regions

The value that seperates the rejection and acceptance region is called critical value

![2334_7_4.PNG]({{site.baseurl}}/img/2334_7_4.PNG)

*E.g 1*
- A certain type of vacchine is known to be 25 percent effective after 2 years
- To determine if a new and more expensive vaccine is superior (Can protect for longer time)

p of origin = effective = 0.25

> If we want to be superior, we must have p>0.25

- 20 people choose at random and use new vaccine
- If more than 8 of these people surpass the 2 year period, then the new vacchine will be considered superior to the one presently in use

X = num of individual out of 20 that surpass the 2 year period without contracting the disease 

> This is consider a success

This is equivalent to test H0 = p = 1/4 and h1 = p >1/4

![2334_7_5.PNG]({{site.baseurl}}/img/2334_7_5.PNG)

We reject H0 when X > 8 when p = 1/4

> Follow binomial distribution of X~B(20,1/4)


![2334_7_6.PNG]({{site.baseurl}}/img/2334_7_6.PNG)

This means that chance of getting type 1 is 4 percent


But we want to ask what is the probability of committing of type 2 error?

- We cannot compute unless we have a *Specific* alternative hypothesis

If let say p = 1/2

![2334_7_7.PNG]({{site.baseurl}}/img/2334_7_7.PNG)

Chance of not committing an error is 1-beta = 1 - 0.2517 = 0.7483

This is vert good because the chance of not commiting the error is very big

# Hypotheses testing concerning mean

Consider the problem of testing the hypo concerning the mean.

Considerations:
1. Variance is known
2. Underlying distribution is normal or n is very large (>30)

We are going to look at the difference to tell if its big or not. 

![2334_7_8.PNG]({{site.baseurl}}/img/2334_7_8.PNG)

## Two sided test
![2334_7_9.PNG]({{site.baseurl}}/img/2334_7_9.PNG)

### Critical value approach
We will try for the interval of Xspa
where

         x1spa < Xspa < x2spa
defines the acceptance test

![2334_7_10.PNG]({{site.baseurl}}/img/2334_7_10.PNG)

p(x1spa < Xspa < x2spa) = 1-a

> We will put xspa at one side of the inequality

![2334_7_11.PNG]({{site.baseurl}}/img/2334_7_11.PNG)


- Reject when Xspa is between x2spa and x1spa
- Critical region is usually stated in terms of Z rather then Xspa


![2334_7_12.PNG]({{site.baseurl}}/img/2334_7_12.PNG)

> However, we can represent it as a t distribution


*E.g 1*
- Breaking strength 35 kg
- SD is 1.5 kg
- Determine if breaking machine has those stats
- Random sample of 49 piece
- Mean breaking strength of 34.5

-is there evidence that the machine is not meeting the specification for mean breaking strenrh

Letting u be the mean breaking strength by the machine

1)

h0: u =35
h1: u !=35

2)
Set a = 0.05 (Not stated in question)

3)
![2334_7_13.PNG]({{site.baseurl}}/img/2334_7_13.PNG)

![2334_7_14.PNG]({{site.baseurl}}/img/2334_7_14.PNG)

![2334_7_15.PNG]({{site.baseurl}}/img/2334_7_15.PNG)

# Critical value approach and p-value approach
# Hypotheses testing concerning difference between two means
# Hypothesis testing concerning variances
