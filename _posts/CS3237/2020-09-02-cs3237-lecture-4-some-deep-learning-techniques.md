---
layout: post
published: true
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

> An epoch is one cycle through the training data

Problems:
- Drop too many neurons in each epoch: Underfit


## Noise layers
Add Gaussian noise to change the data to look like new data

![CS3237-4-2.PNG]({{site.baseurl}}/img/CS3237-4-2.PNG)

[Keras link](https://keras.io/layers/noise)

## Regularisers
A penalty that is applied to the loss function of a layer

For example, in regresss our loss function may look like RSS (Square error loss):
![CS3237-4-3.PNG]({{site.baseurl}}/img/CS3237-4-3.PNG)

> This will give us seuqared error


Our optimisation algo will find the values of params to minimise the loss function

- If there are too many para: the models starts to learn the unique noise of the training data -- Overfitting or memorising
- Force a reduction -> Simplication -> In parameters

We can add in a penalty that is proportional to my parameters (l1 regulisation ) or Sequares of parameters (l2 Regulisation) to loss fnction:
![CS3237-4-4.PNG]({{site.baseurl}}/img/CS3237-4-4.PNG)


The hyperparameter lamda controls how much flexibility we give to the parameters, a higher lamba means more strict control

- L1: Eliminates less important parameters and simplifies the output
- L2: More effective in severe overfitting since it squares the parameters

> If lambda is too high, the model will underfit

### Regularizers
- kernal: Controls main weights (Lines connecting the green nodes)
- Bias: Controls the bias weights (Lines connecting the orange nodes)
- Activity: Controls based on layer outputs (o1 and o2)

![CS3237-4-5.PNG]({{site.baseurl}}/img/CS3237-4-5.PNG)


# Deep learning
In the previous lecture we look at neural networks: 
- Unsupervised and supervised techniques
- Selection of hyperparameters
- Overfitting


The neural networks of the previous lectures has an issue:
- There will be many parameters to train
- Complex layers
- Curse of dimensionality

> Trade of from learning ability and space


This is a motivation for deep learning
- consist of many layer
- Layers are not uniform
- Layers can have differnet function
- Transform and simplify the data so that networks at the end will be less dense and easier to use to train




## Architecture: Long Short Term memories (LSTM)
Key issue with MLP:
- Assumption that samples are independent
	e.g the word 'often' usually follows 'is' or 'are'. Words are not indepednent
- Solution: Use pas and sometimes future info to learn about current data

In RNNs we feed the output of the MLP back to the hidden layer and maybe backwards to previous layers

![CS3237-4-6.PNG]({{site.baseurl}}/img/CS3237-4-6.PNG)

> The prev output becomes the input for the hidden layer.

- Training is carried out using standard gradient descent that we talk abt
- If we unroll an RNN in time, we get:
![CS3237-4-7.PNG]({{site.baseurl}}/img/CS3237-4-7.PNG)
- We see that learning each new piece of data is now affected by past pieces

- Recurrent neural networks are good at learning from patterns in past data:
	- Predicting next words in sentence
    - Predict stock performance base on past data
    - Trajectory prediction forrobot
- Standard RNNS have probelm:
![CS3237-4-8.PNG]({{site.baseurl}}/img/CS3237-4-8.PNG)

We will get this very long equation.. The problem here is that when we do our learning, we have to do our partial differential to get our weights. If we apply this chain rule, we will end up with a differential that looks like:
![CS3237-4-9.PNG]({{site.baseurl}}/img/CS3237-4-9.PNG)


- The gradient of signoid is always small, as we multiply this gradient through time... it eventually gets 0
- When it becomes 0, it eventually stop learning

To Solve this, we introduce a special RNN called long short term memory

![CS3237-4-10.PNG]({{site.baseurl}}/img/CS3237-4-10.PNG)


### Input stage
- The inputs are multiplied by weights and put through a tanh function to squeeze it to betweem -1 and 1
- Input gate: Another neural network that is train to a value of 0 to 1, this controls the degree at which the input is allowed to pass to the next stage

![CS3237-4-11.PNG]({{site.baseurl}}/img/CS3237-4-11.PNG)

### Forgot stage
- Forget gate: Learns the range from 0 to 1 and controls the influence of past and current input

![CS3237-4-12.PNG]({{site.baseurl}}/img/CS3237-4-12.PNG)
### Output stage
- Output stage: Decides what output to pass and what to suppress

### Hidden layer size
- Each gate appears to be a single node but they are actually a collection of nodes
- The number of nodes in each gate is called the hideen layer size

Using the LSTM Cells:
![CS3237-4-13.PNG]({{site.baseurl}}/img/CS3237-4-13.PNG)


The network is one column, at the horizontal axis is the netowork over time. 

- Takes the input
- Trains the LSTM
- Takes the memroy from prev time steps and train again and so on and so forth


Time distributed layer:
Take the output over time and perform a classification or regression.

> We can stack LSTM but
>
> - More complex: More parameters


#### Using LSTM in Keras
{Check notes/slides 15 - 32}



## Architecture: Autoencoders (AEs)
## Architecture: Generative Adversarial Netowrks (GANs)
## Architecture: Convulutional Neural Networks (CNNs)

# Slides