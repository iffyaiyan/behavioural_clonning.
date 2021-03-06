## behavioral_cloning

---

## Introduction

The objective of the project is to train a model to drive a car autonomously on a simulated track. The ability of the model to drive the car is learned from cloning the behaviour of a human driver. Training data is gotten from examples of a human driving in the simulator, then fed into a deep learning network which learns the response (steering angle) for every encountered frame in the simulation. In other words, the model is trained to predict an appropriate steering angle for every frame while driving. The model is then validated on a new track to check for generalization of the learned features for performing steering angle prediction.

## Project Goal

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report

## File Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:

 * model.py containing the script to create and train the model
 * drive.py for driving the car in autonomous mode
 * model1.h5 containing a trained convolution neural network
writeup_report.md or writeup_report.pdf summarizing the results

#### 2. Submission includes functional code Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing
```sh
python drive.py model1.h5
```
#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.




[//]: # (Image References)

[image1]: ./images/cnn.png "Model Visualization"
[image2]: ./images/center.jpg "center"
[image3]: ./images/right.jpg "Recovery Image"
[image4]: ./images/left.jpg "Recovery Image"
[image5]: ./images/architecture.png "Recovery Image"


---

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

This model consists of a convolution neural network with 5x5 and 3x3 filter sizes and depths between 24 and 64. The model includes RELU layers to introduce nonlinearity, and the data is normalized in the model using a Keras lambda layer. 

The normalized data is the input to a stack of 3 convolution layers with 5x5 filter sizes and depths between 24 and 48 that include a RELU activation layer each. Then, the model has two convolution layers with 3x3 filter sizes and depths of 64 that also include a RELU activation layer each. Finally, 4 fully-connected layers complete the model with a number of neurons of 100, 50, 10, and 1, respectively.

#### 2. Attempts to reduce overfitting in the model

The data set is randomly shuffled to avoid overfitting. Early termination is the strategy adopted to also avoid overfitting. After experimentation, the number of epochs is set to 3 due to the fact that the mse is no longer considerably minimnized. The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer

#### 4. Appropriate training data

I chose data provide by Udacity to train the model, used various data Augmentation method to make it more versatile. Details of data augmentation is discussed in next paragraph.

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was based on NVIDIA's architecture (https://devblogs.nvidia.com/deep-learning-self-driving-cars/).
![alt text][image1]

My first step was to use a convolution neural network model similar to the Traffic signs classifier. So I used a LeNet architecture. I used 10 epochs in this.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting. 

In order to combat the overfitting, I reduced epochs to 3. By doing so I got a non-overfitted model because the validation mse and the testing mse where similar.

The next step taken by me was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track. To improve the driving behavior in these cases, I changed the architeture for the NVIDIA one. By doing so, I enhanced the performance of the vehicle of the tracked. However, the car still had problems by turning on pronounced curves. I decided to augment my training and validation sets by considereng the images from the right side and left side cameras with a factor correction of 0.2. 

At the end of the process, the vehicle was able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture consisted of a convolution neural network with the following layers and layer sizes:

Here is a visualization of the architecture (note: visualizing the architecture is optional according to the project rubric)

![alt text][image5]

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][image2]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn to come back to the center of the lane.




For augmenting the dataset, I used the images from the left-side camera and right-side camera with a correction of 0.2 degrees.

#### Left-side camera
![alt text][image4]
#### Right-side camera
![alt text][image3]


After the collection process, I had 4512 number of data points. I then preprocessed this data by cropping the upper part of the image where the trees and sky of the road are in order to delete useless information. 

I finally randomly shuffled the data set and put 20% of the data into a validation set. 

I used this training data for training the model. The validation set helped me to determine if the model was over or under fitting. The ideal number of epochs was 3 as evidenced by the matching of the validation set and training set accuracy. I used an adam optimizer to escape the manual training of learning rate.

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).
