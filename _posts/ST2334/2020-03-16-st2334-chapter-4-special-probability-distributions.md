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

#### E.g 1
The avg number of robberies in a day is four
What is the prob that 6 robberies occur in 2 days

This follows a distribuition of x~possi(lamda) where lambda is 2*4 = 8

P(x=6) = e^ -8 (8)^6 / 6!

#### E.g 2

The avg number of oil tankers arriviing each day at a port is 10. But the facilities at the port can handle at most 15 tankers per day
What is the prob that on given day tankers will have to be sent away

period = one day
x =10
lambda = 10*1 

This follows the distribution of X~p(10)

P(x>15) = 1 - [ sum of e^-10*10^x / x ! from 0 to 15]

= 0.0487

> Since we want the tme where the tankers have to be sent away thus we should find the time where it is greater than its max cap


#### E.g 3
Breakdowns per 8 hour shift with a mean of 1.5

> Follows the distribution x~poss(1.5)

a) Exactly two breakdown during the midnight shift

p(x=2)

b) Fewer than 2 breakdown in afternoon

p(x<2)

c) No breakdown during 3 consecutive 8hr shift

P(A n B n C )

or

> Each shift has one trail and each trail has a success or a failure, no failure = success, some breakdown = failure. Formulate this question in such a way that it is broken down into a binomial distribution with y~B(3, 0.2231)
It is 0 because we want all to not breakdown
P(y=3)

P(x=0) = e^-1.5 = 0.2231

find Pr(Y=3) using binomial


#### E.g 4 
Avg of 1 sq foot of door surface contain 0.5 minor flaw.

a) Fail inspection

Let X be the num of flawas found in 1 sq foot of door
then X~p(0.5)

p(x>=2)

b) Pass inspection

P(x<2) = 1 - a)

> There might be another alternative, but in this case we only have fail or pass.


## Poisson and Approximation to Binomial Distribution

Let X be binomial random variable with parameters p and n.

P(X=x) = nXr * p ^x * q^(n-x) 

suppose n is very large and p is very small in such a away that lambda = np remains a constant as n tends to infinity

Then X will have a possi distribution with a parameter np.

> We are trying to link up the possion and binomial together and this only happens if the n is v large


#### E.g 1
- probability of accident is 0.0001
- If there are 1000 cars in a day

What is the prob of 2 or more accident during that period

This follows a bin dis of x~B(1000, 0.0001)

> THis is v big and can be linked to poisson

(e^-np * np ^x) / x! where np is 0.1


P(x>=2) = 1 - P(x= 0 ) - p(x-1)  = 1 -  (e^-0.1 * 0.1 ^1) / 1!

> We can use this if n is large and P is large as well. We can do this by swapping the definition of success and failure

# Continuous Distribution

## Continuous uniform distribution
A random variable is said to have a uniform distribution over an interval if its PDF is given by

fx(x) = 1/ (b-a) where x is within a and b

> This is also refered to as a rectangular distribution because of the area under the graph

### Mean and variance

E(x) = ( a + b ) / 2

V(x) = 1/12 * (b-a)^2

> The expectation is calculated through integration of the area * x with the range of b to a
The integration will be seperated into 3 due to it happening over 3 different areas.
This is similiar for variance where it is integrated with *x^2 instead over the range of b to a

#### E.g 1
Choose a point randomly at line segment [0,2]

>Since it is random, it is uniform

What is the prib that the point lies between 1 and 3/2?

Let X be the position of the point which follows the distribution X~U(0,2)


#### E.g 2
Find the c.d.f of a uniformly distributed random variable x between [a,b]

fx(x) = integrate fx(t) from x to -infinity

## Exponential distribution

A continuous random variable assume alll non neg values is said to have an exponential distribution with parameter a>0 

fx(x) = ae^(-ax)

### Mean and variance
- If X has exp distribution wiht para a>0

E(x) = 1/a

V(x) = 1/a^2

> Depending of the form of pdf, if the pdf is given like 1/u * e^ (-x/u), then
- E(x) = u
- v(x) = u^2


> E(x) is calculated through an integration of the range of infinity to 0 

### No memory property of exp distribution

Supppose that X has an exp distribution with para a>0, then for any two positive numbers s and t, we have

Pr(X > s + t | X > s) = P(X > t)

| -------- | ----------|
      s          t    (s+t)
 
 
E.g Given that a person has waited 30 mins for a bus. what is the chance that he has to wait another 5 mins (ie wait for 35 mins)
This is similiar as to the person was waiting for 5 mins. We ignore the fact that he was already waiting for 30 mins.


Let X denote the life length of a bulb
Given that the bulb has lasted s time units (X>s)

- The the probability that it will last for the next t units (X>s+t) is the same as the probability that it will last for the first t units as brand new.

CDF: 1 - e^ (-ax) for x>=0

CDF : 0, other wise


#### E.g 2
- Failure time T of a sys has a mean 5
- What is the prob that at least 2 out of 5 are still functioning after the end of 8 years?


PDF: 1/5 * e ^ (-1/5 * T) where T >0

Y~ B(5,p), 
where the success is P(T > 8) = 0.2
Hence T ~ Exp(1/5)

> Since we have the prob of a sys >8, we can use this for bin distribution


Let X represent the sys out of the 5 sys that are still functioning after 8 years
Then X ~ B(5,0.2), Where 

P(x>=2) = 0.2627

### Applications
- Model for the distribution of times between the occurance of successive events.

e.g Customers arriving at a service facilities or calls coming into a switch board.



## Normal Distribution

The random variable X assuming al real values ifninity ti neg infinity has a normal distribution if its pdf is

( 1/sqrt(2*pi * sigma) ) * exp( - (x-u) ^2 / (2*signma) ^2 )

Where u is betweeen -infinity and infinity and signma > 0
This is denoted by N(u, signma^2) 

>Sigma is standard deviation

### Properties

1. The graph of this distri is bell shapped and called normal curve and is sym about the vertical  x = u

2. The maximum point occurs at x = u (centre) and its value is

1/ sqrt(2 * pi * sigma)

> If variance is big, the max pdf is small

3. The normal curve approaches the horizontal axis asumptotically as we proceed in either direction away from the mean

4. The total area under the curve and above the hosrizontal axis is equal to 1
> This is true for all distribution

5. E(x) = u , v(x) = signma^2

6. Two normal curves are identical in shape if they have the same sigma^2. But they are centered at different positions when their means are different

> The difference is in the mean.


7. As sigma increases, the curve flattens and as sigma decrease, the curve sharpens

8. If X has a distribution N(u, signma^2) and if

Z = (X - u) / signma

Then Z has the N(0,1) distribution

> The importance if standardized normal distribution is the fact that it is tabulated

When ever X has distribution N(u, signma^2), we cna always simplify the processd of evaluared the values of P(x<X<x2) by using the transformation 

X = (X - u) / signma

hence, x1 < X < x2 is same as

(x1 - u) / sigma < Z < (x2 -u) /sigma

> Remmeber ti reverse the inequality if multiplied by a negative number

#### E.g 1
Given X ~ N ( 50 , 10 ^2)

Find P(45< x < 62)

= P[(45- 50)/ 10 <  Z < (62-50)/10 

= P(-0.5 < Z < 1.2)

= P(Z < 1.2) - P(z < -0.5)

> It is better to draw the graph

=  1 - P(Z >= 1.2) - P(Z > 0.5)

= 1 - 0.1151 - 0.3085 = 0.5764

### Using statistical table

if X ~ N ( 3,0.5^2)

a) P(X < 2.3) = P (Z < -1.4) 

> Standard normal is symmetrical

#### E.g 1 
- Avg grade was 74 and the SD was 7
- If 12 percent of class are given A's and grades follow a curved normal dist
- Whats the lowest possible A and the highest possible B

We want to find P(X >x ) = 0.12

X ~ N (74, 7^2)

P(X > x) = 0.12 implies that P(Z > (x-74)/7) = 0.12
where Z = (X -74) /7 = 1.175

Therefor x = 74 + (1.175)7 = 82.225

Hence the lowest possible A is 83 and the highest possible B is 82

> Linear interpolation

Let P(Z >a ) = 0.12
From the normal table we have
P(Z > = 1.17 ) = 0,.121 and P (Z >= 1.18) = 0.119

Hence (a - 1.17) / (1.18-1.17)


#### E.g 2 
- Find the 6oth percentile from e.g 1

P(x<x60 ) = 0.6

We are trying to have P(Z< 0.2533) = 0.6 where Z~N(0,1)

#### E.g 3
- Let x be amt of sugar which filling machines put into 500g packets
- The actual amount of sugar filled varies from packet to packets
- Suppose X ~ N( u, 4^2)
- If only 2 percent of the packets contain less than 500g of sugar.

-> Set the machine
-> We Are only expecting 2percent
-> Since it is a normal, it is symetrical
-> P(Z < -2.053) = 0.02
-> -(500 - u)/5 = 2.0537
-> The mean is 508.2g

> Decrease the variance so that the probability of dispensing less sugar is smaller

## Normal approximation to binomial distribution

if X~b(n,p), we can approx such that

x~ N (np, np (1-p)), if p is very small or v big and n is very large

- Use only if np > 5 and n(1-p) > 5

If X is a binomial random variable with mean u = np and variance np(1-p)

Z = X -np / sqrt(npq) is approc ~ N(0,1)
where q is 1-p

#### e.g 1 
if X ~ B(15,0,4) then
p(X = 4 ) = 15 C 4 * (0.4) ^4 * (0.6) ^ 11 = 0.1268
