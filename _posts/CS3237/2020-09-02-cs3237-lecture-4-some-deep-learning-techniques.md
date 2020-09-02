---
layout: post
published: false
title: 'CS3237 - Lecture 4: Some deep learning techniques'
---
# Recap: Overfitting
- All data can be thought of consisting of two things:
	- Some generator process f(x) where x can be time or an actual input
    - Noise
- When we build model, we want it to learn only the generator process f(x)
	- The noise is random, it is unique to the training data
    - If we learn noise, results in **overfitting** 
    
    
Choices to avoid learning noise:
	- Have simple model (few parameters)
    - Have more training data so that the network can avg out the noise


> A single dimension parameter results with a straight line, 3 values will result in a parabola 
> The point is that the higher dimension that we go, the more sophisticted the curve becomes.. This might results in fitting the data too well which includes the noise

    
Catch:
- A simple model may not learn f(x) well, **underfitting**
- The amount of training data needed grows exponentially with model complexity

> If we tryign to learn a cube curve and we are using only enough parameters to learn a parabola, we will not get a good approximation.

#### Earling stopping point
- Stop when we see a certain state where it looks like it is overfitting


## Drop out layer
- a fix percentage of neurons in layers are drop from training for one more epoch
- There are then put back in and another percentage are drop
- Reduce the num of training parameters


![CS3237-4-1.PNG]({{site.baseurl}}/img/CS3237-4-1.PNG)



# Long Short Term memories (LSTM)

