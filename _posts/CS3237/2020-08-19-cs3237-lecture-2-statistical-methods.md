---
layout: post
published: true
title: 'CS3237 - Lecture 2: Statistical Methods'
---
# Advantages 
- Statistical methods have better theretical
- Statistical methods in general are faster to build and train
- Statistical methods usually have fewer hyper parameters to adjust

# Statistical - Linear Regression

We have data that shows the relationship between a dependent variable and one or more independent variables
> e.g The relationship between population growth and time

- Relationship between the dependent variable and the independent variable can be a straight line (Linear) or not (Nonlinear, ie curve)
	- Consider linear relationship with one independent variable (Simple linear regression)
- Previous lecture we build regression model using gradient descent
  - Our model will be based on equation of a straight line
  > Good example of how statistical methods have better theoretical basis than neural networks

## Simple linear regression
- Independent variable: Uncontrollable variable. (GDP growth)
- Dependent variable: The variable that we are interested in predicting agaisnt the independent variable. (Sale)

![CS3237-2-1.PNG]({{site.baseurl}}/img/CS3237-2-1.PNG)

> The in


### Assumptions

![CS3237-2-2.PNG]({{site.baseurl}}/img/CS3237-2-2.PNG)


- There exist a correlation between dependent (y) and independent (x) variables
- y depends on x through a linear equation:
	`yi = a . xi + b` (Blue line)
- We add a random noise e in the observation 
	`yi = a . xi + b + ei`
- Our task
	- Test if there is a relationship between x and y
    - Find a and b

> We are trying to make a relationship so that we are able to predict the future

### Covariance 

If there is a change in one variable when the other variable change, this is a covariance

#### Example
![CS3237-2-3.PNG]({{site.baseurl}}/img/CS3237-2-3.PNG)

- (Xi - X) shows the difference between both pointss value will be large 

Calculating the avg for the GDP and Sales figures:
- Avg(GDP)
- AVG(sales)
- Cov(Sales, GDP)
> If COV is positive, sales figure grow in the same direction as GDP

We know that there is a correlation but we dont know if the relation is strong. 

### Correlation

![CS3237-2-4.PNG]({{site.baseurl}}/img/CS3237-2-4.PNG)

Correlation will give us a better idea of the relationship. Correlation will scale our values from -1 to 1. This will allow us to determine the strenth of the relationship

- If the value is close to 1, we can see that the figures are strongly related

### Parameter estimation

yi = a . xi + b + ei

- The error is therefore:
   - ei = yi -a . xi - b

- Lost function:
![CS3237-2-5.PNG]({{site.baseurl}}/img/CS3237-2-5.PNG)

> This gives us an idea on how good our model is.

- To minimize Q(a,b), we take:
![CS3237-2-6.PNG]({{site.baseurl}}/img/CS3237-2-6.PNG)

- Doing the second equation
![CS3237-2-7.PNG]({{site.baseurl}}/img/CS3237-2-7.PNG)


> Solve for b

- Setting it to 0 and solving for b we have
	- b = ySIGMA - a . xSIGMA

> This makes sense because our avg are going to be dependent on both x and y. Therefore the avg will restrict on where the intercept is

![CS3237-2-8.PNG]({{site.baseurl}}/img/CS3237-2-8.PNG)

#### Example

![CS3237-2-9.PNG]({{site.baseurl}}/img/CS3237-2-9.PNG)

> Even thou we got 255.1 unit, this is just a rough estimation due to the noise

# Naive Bayes Classification
Given a set of data X and a set of class C, we want to compute the likelihood of some x in X belongs to some class in C

#### Examples
- X is a set of news article and x is a article
- C is a set of news article types e.g sports, politics
- Our task is then to decide what kind of article x is

## Assumption

![CS3237-2-10.PNG]({{site.baseurl}}/img/CS3237-2-10.PNG)

- Each vector represent a word.. we want to see the frequency of the words. 
- But theres a problem because it does not consider the order of words
- This could cause error because sometiems order of words are important > This is where we get classiification error


Using Chain rule:
![CS3237-2-11.PNG]({{site.baseurl}}/img/CS3237-2-11.PNG)
> we are looking at the probability of some xi given xi+1...etc
> 
> We take the naive assumption that all these values occur independent of each other. (This does not make sense in normal english) e.g "Joint probability" happens more often compared to "final joint"

![CS3237-2-12.PNG]({{site.baseurl}}/img/CS3237-2-12.PNG)

## Parameter estimation
- Uniform: For n classes, the probability is simply 1/n
- Base on training set: There is a total of S training samples and sk samples for class ck, then p(ck) = sk/S

Estimation assumption:
- Gaussian: Assumes that the probaility of a feature xi taking a particular value v in class c follows a normal distribution
	- Good for linear values
- Multinomial: Assumes 
	- Good for frequency
- Bernoulli:
	- Good for binary

## Continous variables 
- Classes contains continous variables
	- E.g when classifying male and female, we may just consider height, weight etc

![CS3237-2-14.PNG]({{site.baseurl}}/img/CS3237-2-14.PNG)

#### Example
![CS3237-2-13.PNG]({{site.baseurl}}/img/CS3237-2-13.PNG)
![CS3237-2-15.PNG]({{site.baseurl}}/img/CS3237-2-15.PNG)

> We use a gaussian distribution here. 

- Since our training set has 4 male and 4 females, p(male) = 0.5

![CS3237-2-16.PNG]({{site.baseurl}}/img/CS3237-2-16.PNG)
![CS3237-2-17.PNG]({{site.baseurl}}/img/CS3237-2-17.PNG)

> Because the p(female|...) > p(male|..), we can conclude that this person is "female"

## Naive Bayes - Multinomial 
![CS3237-2-18.PNG]({{site.baseurl}}/img/CS3237-2-18.PNG)

### Issues

1. Raw frequencies in document classification face some problems
	- Bias towards longer documents
    - Bias towards connector words such as "the" because they occur more frequently

We try to fix this by using tf.idf (term frequency inverse document frequency):
![CS3237-2-19.PNG]({{site.baseurl}}/img/CS3237-2-19.PNG)

> Adds a small number to it such that the word that occur many times in document will get a punishing term. (Total number of documents / Documents containing the word i)

2. Zero frequency
	- Pik = 0 and P(x|ck) becomes 0
    - Laplace smoothing: Add 1 to every xi so that it wont be 0

### Naive Bayes - Bernoulli

Sometimes we are interested if the event even occurs at all.

![CS3237-2-20.PNG]({{site.baseurl}}/img/CS3237-2-20.PNG)

> No. of times it occurs / Samples


# Decision trees
Classification to be explainable or calculate on the expectant values

![CS3237-2-21.PNG]({{site.baseurl}}/img/CS3237-2-21.PNG)


Appealing because: 
- easy make decisions
- Provides a way to explain decisions

#### Example
![CS3237-2-22.PNG]({{site.baseurl}}/img/CS3237-2-22.PNG)

- If too much water, plant die
- If too little, plant die
- Just nice.. good for farmer

#### Deriving trees

- Guesswork based on expert opinion
- Based on historical data


Entropy: Amount of uncertainty in a data

![CS3237-2-23.PNG]({{site.baseurl}}/img/CS3237-2-23.PNG)

> The entrophy is 1 which is the worse case if its evenly distributed

![CS3237-2-24.PNG]({{site.baseurl}}/img/CS3237-2-24.PNG)

> We will use ID3 algo to generate the tree


### ID3 algo

- Choose a decison criterial that reduce uncertainty as much as possible

![CS3237-2-25.PNG]({{site.baseurl}}/img/CS3237-2-25.PNG)

- p(x) = nx / n and H(S|A) is the entropy

#### Example

- We want play tennis
- We need to see weather outlook, temp, humidty and wind to decide
- Looking at bob;s pattern of decision making and try to learn

![CS3237-2-26.PNG]({{site.baseurl}}/img/CS3237-2-26.PNG)
![CS3237-2-27.PNG]({{site.baseurl}}/img/CS3237-2-27.PNG)

> We have to go through each of the decision factors in turn

p(x|Wind=weak) : Probability of yes or no given wind is weak

![CS3237-2-28.PNG]({{site.baseurl}}/img/CS3237-2-28.PNG)

> We can find our entrophy base on the decision made after making the graph smaller.

![CS3237-2-29.PNG]({{site.baseurl}}/img/CS3237-2-29.PNG)
> The entrophy here is 1

*Therefore*


![CS3237-2-30.PNG]({{site.baseurl}}/img/CS3237-2-30.PNG)


We have to do this for the other graph and pick the highest gain


![CS3237-2-31.PNG]({{site.baseurl}}/img/CS3237-2-31.PNG)

We will get the tree:

![CS3237-2-32.PNG]({{site.baseurl}}/img/CS3237-2-32.PNG)

> Repeat this for the other variables such as humidity/Wind/Outlook


Look at wind:

![CS3237-2-33.PNG]({{site.baseurl}}/img/CS3237-2-33.PNG)

![CS3237-2-34.PNG]({{site.baseurl}}/img/CS3237-2-34.PNG)

The final tree after finding all:

![CS3237-2-35.PNG]({{site.baseurl}}/img/CS3237-2-35.PNG)

> We start from the largest gain and go downwards

### Drawbacks
- It only works with nominal values (factors has values that are clear categories)

> C4.5 actually addresses it by take the discontinous ranges and chunks them into bins

> Decision trees can also be use for regression


# Support Vector Machines
![CS3237-2-36.PNG]({{site.baseurl}}/img/CS3237-2-36.PNG)

A hyperplan is a d dimennsional plane defined by its normal vector w
	- in 2D, a hyperplan is a strightline
    - normal w is orthogonal to all points on the plane
    - The hyper plan seperates the d dimensional space into two halves
    - Hyperplanes always pass through the origin
    > This restricts its ability to partiiton the space
    > To fix this we add a d-dimesnion bias b
    
![CS3237-2-37.PNG]({{site.baseurl}}/img/CS3237-2-37.PNG)
