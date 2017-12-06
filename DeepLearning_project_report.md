## Project: Follow me

[//]: # (Image References)

[image1]: ./NetworkArchitecture.jpg

## [Rubric](https://review.udacity.com/#!/rubrics/972/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Introduction

In this project, I have build and trained fully convolutional neural network for semantic segmentation to classify target object from background and non-target objects. Utilized trained model to make drone follow target object in simulation.

### Network Architecture

Network architecture of fully convolutional neural network for semantic segmentation is shown below:

![alt text][image1]

Network architecture consist of encoder layers, followed by convolutional layer and then decoder layers. Encoder layer reduces the spatial dimension whereas decoder layers does an opposite operation. 1x1 convolutional layer is chosen instead of fully connected layer to retain the spatial information.

In this project, I have chosen 3 encoder layers with initial filter size as 32, followed by 1x1 convolutional layer and then followed by 3 decoder layers.

### Parameters chosen for the neural network

* Learning rate: From Keras documentation, there are various optimizers like SGD, RMSprop, Adam, Nadam, etc. can be used. In this project, I have used Nesterov Adam optimizer which is Adam RMSprop with Nesterov momentum where learning rate is kept as default as 0.002.

* Epoch: Epoch is number of times the entire training dataset gets propagated through the network. In this project, I have chosen number of epoch as 40.

* Batch size: Batch size is number of training samples/images that get propagated through the network in a single pass. Initially I had chosen batch size as 40 and yield around 36%. Then I chose batch size as 20 and yield around 41%.

* Workers: Workers is maximum number of processes to spin up. Since I was not able to use my AWS account due to lack of limit and had to use my local machine to train my neural network, I kept the parameters as default. 

### Conclusion
