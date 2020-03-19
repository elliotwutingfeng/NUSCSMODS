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

#### e.g 3

- Man claims to be ESP
- Fair coin is flipped 10 times and asked to predict the outcome in advance
- The man gets 7/10 correct
- Does he have the ability? What is the probability that he would have done at least this well if he had no esp

1. Show the chance for ordinary people

p(each outcome) = .5
Hence the number X of correct guesses out of 10 follows the binomial distribution with parameters n=10 and p = 1/2
That is X~B(10,0.5)
P(X=x) = NCx * p^x * (1-p)^(n-x)

Thus the probability that he would have gotten that is p(x>=7) = P(x=7) + p(x=8) + p(x=9) + p(x=10)
= 0.1719

> We can use a graphics calculator/excel to calculate the binomial probability

>Use hypothesis testing to test if what he say is true


#### E.g 5
- At most 10% of power supply units need services during the warranty period
- Testing labotary purchase 20 units and test the claims
- p denote probability that power supply unit needs repair during the period
- lab technicians decide that the experiements supports that claim the p<=10
- let X denote the number of units among 20 sample that need repair thus let x~B(20,p)

1. Consider the rule:
- Reject claim that p<=0.1 in favour of conclusion that p>0,1 if x>=5 (where x is the observed value of X)
- Consider the claim plausible if x<=4 

> My decison rule should be greater or equal then certain number.

*if my claim is >=0, that means i will confirm reject the claim*


2. Assuming that p is 0.1 (an incorrect conclusion is):

P(x>=5 when p = 0.1) = 0.0432

The prob that the claim is not rejected when p = 0.2 (Another incorrect conclusion) is 

p(x<=4 when p = 0.2) 
= 1 - P(x>=5 when p =0.2)
= 0.6296

> If p is really <= 10%, when we do the experiement, as long as the >= 5, the claim will be rejected. (We have 4 percent chance of making a mistake)


This examples highlights on the way that someone claims is being tested. We either reject or accept the claim by checking the probability.

3. Manufactors is understating, there is more than 10 percent that would need servicing.



## Negative Binamial Distribution

1. p - Probability of suuccess
2. x - number of successes
3. n - number of trials

> Let us consider an experiement where the properties are the same as those listed for a binomial experiment, with the exception that the trials will be repeated until a fixed number of successess occur.

Number of trials now is the random variable and x is the fixed constant.

e.g Suppose we want to find the probability that the fifth success occurs in the seventh trials.

**We need 5 success:  6C4 p^5 (1-p)^2.**

p(x=7) = 6C4 * p^4* q^(6-4) * p
- The Xth trial must be a success
- x = k, where k is the number of trials 
- We need x - k failures

we denote this as **NB(k,p)

where the probability function is given by
p(X=x) = fx(x) = (x-1)C(k-1) * p ^k * q^ (x-k)

It can be shown that

**E(X) = k/p

and 

**Var(x) = (1-p)k / p^2

> [E(X)] If p is small, then k/p is big. This means the number of tirals is big. Bigger number of success = more number of trials

> [VAR(x)] If p is small, then var will become huge. If p is large, the the var will become small.


#### E.g 1

- Team wins 4/7 is winner
- Suppose team A and B face each other 
- A has prob 0.55 of winning a game over team B

> Here we use NB because the probability of success is fix

a) What is the prob that team A will win the series of 6 games

p(x=6) = Win the series in 6 games.

5C3 * 0.55 ^ 4 * (1-0.55) ^ (6-4)

b) What is the probability that A will win

p(X>= 4) = P(X=4) + p(x=5) + p(x=6) + p(x=7)

> Note that we do not need to go into game 8

c) What if we play 11/21 to win.. will it be better?

It must be slightly more than half



## Poisson Distribution

Experiment yielding the numerical values of a random variable X, the **number of successes** occuring during the given **time interval** or **region** are called Poisson Experiements

> number of occurance in a fix area/ region

e.g Number of telepjone calls in an **hour**

e.g Number of postponed games due to train during **a football season**

e.g X is the number of mushrooms in a **plot of land**

e.g Number of bacteria in **given culture**

### Properties
1. The _num of success_ occuring in one time interval or specified region are **indepedendent** of _those occuring in any other disjoint time interval_ or region of space

2. The probability of single success is proportional to the length of the time interval

3. The **probability of more than one success** occurring in such a short time interval or falling in such a small region **is negligible**
     
### Definition
- X is called poison random variable

fx(x) = p(x=x) = ( e^-lambda * lambda ^ x ) / x!
for x = 0,1,2,3...

> Remember that e^x is a series

#### Mean and Variance of Possion RV

E(x) = lambda = v(x)

> This is the only distribution that the variance and mean is the same





## Poisson and Approximation to Binomial Distribution

# Continuous Distribution
## Continuous uniform distribution
## Exponential distribution
## Normal Distribution
## Normal approximation to binomial distribution
