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



Correlation will give us a better idea of the relationship. Correlation will scale our values from -1 to 1. This will allow us to determine the strenth of the relationship

### Parameter estimation



# Naive Bayes Classification
# Decision trees
# Support Vector Machines
