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
- Idea: Train a neural network to take an input x and generate the same output x. We will build a deep learning netwrok that does:

![CS3237-4-14.PNG]({{site.baseurl}}/img/CS3237-4-14.PNG)

> The stuff at the center is actualy the compress version of the input

- Achieving compression:
	- if the code layer is substantially smaller than the input, we can feed the input and use the resultant code as a compressed version of the input
    - We can feed this code into the decoder network to recover the original
    - AE however are very bad at this: recovered data will be highly lossy and the AE can only reconstruct data of the type it was trained on
    
> But remember that because its a neural network, it is not really precise. (There might be some inaccuracy) Therefore the reconstructed data might be lossy (Noise and imperfection introduced)
    
- Detect anomalies:
	- When AE sees typical data it was trained on, it can reconstruct the input with minimal error
    - When the data becomes atypical, reconstruction error rises. We can flag anomalies when this error exceeds a threshold.
    
> Autoencoders are very good to spot defects in teh system
    
### Simple
![CS3237-4-15.PNG]({{site.baseurl}}/img/CS3237-4-15.PNG)

- F can be our throttle position sensor
- Train the neural network to guess the acceleration base on the position of the trottle position



## Architecture: Generative Adversarial Netowrks (GANs)

Motivation:
- Often dont have enough training data
- Want to build a neural network that will produce fake data from real data



Consist of:
- A generator network that learns how to counterfeit the data
- A disciminator networks that learn how to differentiate betweem the real and fake data
- We can use GANs to do things like: Producing images of people who dont exist


##### What are they
- Generator:
	- Random noise is presented to the generator
    - The generator uses this to create its fake data
- Discriminator
	- both fake and real data are presented to the discriminator
    - discriminator is trained how to differentiate them

![CS3237-4-16.PNG]({{site.baseurl}}/img/CS3237-4-16.PNG)


##### How do they work
- Training generator
	- Weights for discriminator are frozen
    - The GAN is trained of the assumption that the fake data is real
    - End result: The generator adjusts its weights to try to maximise the realness of the fake data
    - The process repeats
- Training alternates between:
	- Maximising the discriminator ability to tell fake data from real
    - Maximising the quality of the fake data to minimise the discriminator ability to differentiate
    
> This is why it is called an adversarial networks as both netoworks try to fight each other

#### Generating
{Check notes 48-56}

### Training 
- Create generator, discriminator and GAN networks and load the data
- In each epoch for discriminator
	- Generate fake data using random numbers
    - Randomly choose real data and combine with fake data
    - Tag the real data with 1 and fake with 0
    - Train the discriminator
- In each epoch, for the generator
	- Freeze the discriminator weights
    - Generate the fake data using random numbers
    - Train the GAN with the assumption that the fake data is real
    - This forces the generator to optimise its weights to maximise its score from the discriminator
    - the discriminator itself is not affected since its weights are frozen

> See slides for epoch example


## Architecture: Convulutional Neural Networks (CNNs)

### Convolution layers
The CNN primary distinguishing feature is the convulution layer. 
	- Made up of kernals that convolve over the input and over each other


The depth of the kernal is equal to the depth of the data.
- E.g with colour images, there are 3 channels and the kernal is 3 layers deep:


- The kernal function as feature extractors and the output from the convolution operation is called a feature map
	- As training progresses the kernals become optimised to extract key infomation like edges, repeating patterns, etc in input data
- Many kernals can be use on one layer
	- This will produce a volume of feature maps instead of a single feature map
    - Due to the randomness of the initial kernal, each feature map ends up extracting a different feature of the input.
    
    
- You can convolve kernals over earlier kernals
	- The feature maps generated will represent higher level features of the input
    - E.g the lower kernal might extract lines, the higher kernal might extract shapes

##### Parameters:



##### Layers:


### Pooling layer
- The pooling layer takes a nxn region of the feature map and either picks the max of takes avg

- pooling layers:
	- reduce dimensionality and hence computing power
    - Ewxtract the most dominant featueres (Max pool)
    - Averages the features

Hyperparameters:



> Generally the first few layers of the CNN consist of alternating convolution and pooling layers
> BUT, stacking to many pooling layers can result in loosing all data





# Slides
