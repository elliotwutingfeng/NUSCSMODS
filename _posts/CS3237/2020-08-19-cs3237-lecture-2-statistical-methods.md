---
layout: post
published: false
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
> 


![CS3237-2-12.PNG]({{site.baseurl}}/img/CS3237-2-12.PNG)




# Decision trees
# Support Vector Machines
