## Project: Follow me

[//]: # (Image References)

[image1]: ./NetworkArchitecture.jpg

[image2]: ./TargetObject.png
[image3]: ./NonTargetObject.png
[image4]: ./TargetfromNonTargetAndBackground.png

## [Rubric](https://review.udacity.com/#!/rubrics/972/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Introduction

In this project, I have build and trained fully convolutional neural network for semantic segmentation to classify target object from background and non-target objects. Utilized trained model to make drone follow target object in simulation.

### Network Architecture

Network architecture of fully convolutional neural network for semantic segmentation is shown below:

![alt text][image1]

Network architecture consist of encoder layers, followed by convolutional layer and then decoder layers. Encoder layers takes an input image and generates a high-dimensional feature vector by aggregating features at multiple levels. The encoder part have pooling features which eventually reduces the risk of over-fitting but reduces the spatial dimension. Decoder layers takes a high-dimensional feature vector and generates a semantic segmentation mask by decoding features aggregated by encoder at multiple levels. The decoder part recovers the spatial dimension. In the process, we lose some resolution because the activations were downscaled and therefore to add back some resolution by adding activations from the previous layer called as skip connections. 1x1 convolutional layer is chosen instead of fully connected layer to retain the spatial information.

In this project, I have chosen 3 encoder layers with initial filter size as 32, followed by 1x1 convolutional layer and then followed by 3 decoder layers. We can add more layers in future or increase filter size to inrease the overall accuracy.

### Parameters chosen for the neural network

* Learning rate: From Keras documentation, there are various optimizers like SGD, RMSprop, Adam, Nadam, etc. can be used. In this project, I have used Nesterov Adam optimizer which is Adam RMSprop with Nesterov momentum where learning rate is kept as default as 0.002.

* Epoch: Epoch is number of times the entire training dataset gets propagated through the network. In this project, I have chosen number of epoch as 40.

* Batch size: Batch size is number of training samples/images that get propagated through the network in a single pass. Initially I had chosen batch size as 40 and yield around 36%. Then I chose batch size as 20 and yield around 41%.

* Workers: Workers is maximum number of processes to spin up. Since I was not able to use my AWS account due to lack of limit and had to use my local machine to train my neural network, I kept the parameters as default. 

### Conclusion

With trained model, we are able to extract target object from background by labelling the target object as shown below:

![alt text][image2]

We were also able to extract target object from non-target and background as shown below:

![alt text][image4]

However, the trained model won't be able to classify other target object like dog, cat, car, etc. because the model was trained only for target object with human being of particular shape and color. To classify other target object like dog, cat, car, etc. and follow other target object, then model needs to be trained for other target object like dog, cat, car, etc. We could use the same network architecture unchanged but train on image data by collecting datasets for the target object that needs to make drone follow that object. To make drone follow particular object, the model always needs to be trained for that same particular object.  

Due to lack of support from AWS, I had to train my neural network on my local machine which took lot of time to train the FCN neural network. The only variation I was able to conduct is my reducing the batch size to achieve an accuracy of 41%. In future with AWS support, I will train the neural network by increasing number of epochs and see where it overfits the model and increase the initial filter size to achieve better accuracy. 
