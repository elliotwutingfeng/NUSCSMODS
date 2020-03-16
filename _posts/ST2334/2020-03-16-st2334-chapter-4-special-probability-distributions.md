---
layout: post
published: true
title: 'ST2334: Chapter 4 - Special probability distributions'
---
# Discrete Distributions

## Discrete Uniform distribution
If the random variable X assumes the values x1, x2..xk with equal probability which sum up to 1

Then the RV X is said to have a discret uniform distribution and the probability function is given by

fx(X) = 1/k where x = x1...xk

### Mean and variance of discrete uniform distribution
The mean and variance of the discrete uniform distribution are:

u = E(x)
v^2 = sum of (x-u)^2fx(x) = 1/k sum of [(xi - u)^2]
= E((x-u)^2)

#### e.g 1
When a light bulb is selected at random from a box that contains a 40-watt bulb, a 75 and 100 watt bubl
Each element of the sample space S  occurs with 1/4 probability

Therefore we have a discrete uniform distribution of 1/4 = fx(X)

> The general formula of mean is x * corresponding value of x


## Bernoulii and Binomial Distributions

### Bernoulii distribution
It is an random experiment that has only 2 outcomes, failure and success, 1 and 0.

The random variable of X is defined to have a bernoulli distribution if the pdf of X is given by

fx(X) = p^x(1-p)^[1-x], x = 0,1

> What if x = 0.5?

We cannot use this formula then. There is 0 chance that we will get .5

Parameter p satisfy 0 < p < 1

#### Mean and Variance

- Mean:

u = E(x) = p

- Variance:

v^2 = V(x) = p(1-p) = pq

where q = 1-p

> Variance of X is E(x^2) - (E(x))^2 = p-p^2

#### E.g 1
A box with 4 blue and 6 red balls. We take one ball
What is the probability that blue is chosen?

> We do not need to care about the other balls

- Let X = 1 if a blue is chosen and 0 otherwise
- P(x = 1) = 4/10
- P(x = 0 ) = 1 - .4 = 0.6
- That is 

       fx(x) = 

                 { 0.4 if x = 1
      
                 { 0.6 if x = 0
                 
                 
### Binomial Distribuition
A random variable X has BD with 2 parameters n and p
if the probability function of X is given by:

P(X = x) = 

fx(X) = NCX * p^x(1-p)^[n-x] = nCx * p^x * q^(n-x)

X is the number of scucess that occure in n independent bernoullie trials

Note:

X~B(10,0.5) -> Symmetric

X~B(10,0.2) -> Skew to the right

X~B(10,0.9) -> Skew to the left

> Look at the tails to determine the direction

#### Mean and variance
- Mean:

u = E(x) = np

- Variance:

v^2 = V(c) = np(1-p) = npq

The sum of the probability function is 1

> E(x) = E(x1) + ... E(xn), each E(x1) is p and since we add it n times, E(x) = np

#### Conditions for a binomial experiement
- Must consists of n repeated Bernoulli trials

x1 can be a success, x2 can be a failure
X1 and X2 are similar because it follow the same distribution but does not mean that the outcome is the same.

X1 + X2 != 2X1


- Only 2 possible outcomes: Success and failure in each trial

- P(Success) = p is the same constant in each trial

- Trial are independent

The random variable X is the number of successes among the n trials in a binomial experiement

#### e.g 1
Prob of 6 heads when unbiased coin flipped 10 independent times?

- Let X denote the number of heads in 10 independent tosses
- Since there are 2 outcomes with the same prob of success which is 1/2 for all 10 independent trials, therefore X~B(10,.5)
- Hence:

p(X=6) = 10C6 * 0.5^6 * (1-0.5)^4

= 10!/(6!*4!) * (1/2)^10

- Alternatively, we can find P(x=6) by doing 

p(x=6) = P(x>=6) - p(x>=7) 

by making use of the table of upper tail of the cdf of binomial distribution for n = 10 and p = 0.5


## Negative Binamial Distribution
## Poisson Distribution
## Poisson and Approximation to Binomial Distribution

# Continuous Distribution
## Continuous uniform distribution
## Exponential distribution
## Normal Distribution
## Normal approximation to binomial distribution
