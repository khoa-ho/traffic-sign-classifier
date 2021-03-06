# **Traffic Sign Recognition** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

## Dependencies
This project requires:

* [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit)

The lab environment can be created with CarND Term1 Starter Kit. Click [here](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) for the details.

## Writeup

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./summary_statistics.png "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./test_images/1.jpg "Traffic Sign 1"
[image5]: ./test_images/2.jpg "Traffic Sign 2"
[image6]: ./test_images/3.jpg "Traffic Sign 3"
[image7]: ./test_images/4.jpg "Traffic Sign 4"
[image8]: ./test_images/5.jpg "Traffic Sign 5"
[image9]: ./test_images/6.jpg "Traffic Sign 6"
[image10]: ./test_images/7.jpg "Traffic Sign 7"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/khoa-ho/traffic-sign-classifier/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

* The size of training set is 34799
* The size of the validation set is 34799
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing the number of examples of each class in the training set.

![summary statistics][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

I normalized the images to help with gradient descent.


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, 'valid' padding, outputs 28x28x16 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x16 				|
| Convolution 5x5     	| 1x1 stride, 'valid' padding, outputs 10x10x32 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x32 				|
| Flatten | outputs 800 |
| Fully connected		| outputs 120      									|
| RELU					|												|
| Fully connected		| outputs 84      									|
| RELU					|									|
| Fully connected		| outputs 43      									|
| Softmax				|         									|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an Adam Optimizer with the following hyperparameters:
* Learning rate: 0.001
* Epochs: 7
* Batch size: 32


#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.998
* validation set accuracy of 0.968
* test set accuracy of 0.950

I adapted the LeNet architecture for this task because LeNet has been shown to be very effective at classifying small images. My network has two convolution layers, each followed by a relu activation and a max pooling layer. The second part of the network are two fully connected layers (with relu activation) and an output layer, followed by softmax. I added dropout at the two fully-connected layers to reduce over-fitting. 


### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are 7 German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8] ![alt text][image9]
![alt text][image10]

The sixth image might be difficult to classify because after being rescaled to 32x32, it's hard to identify the features inside the triangle.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Right-of-way at the next intersection      		| Right-of-way at the next intersection   									| 
| Go straight or right     			| Go straight or right 										|
| Priority road					| Priority road											|
| Road work	      		| Beware of ice/snow					 				|
| Priority road			| Priority road      							|
| No entry	      		| No entry					 				|
| Stop			| Stop      							|


The model was able to correctly guess 6 of the 7 traffic signs, which gives an accuracy of 85.7%.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

Following are the top 5 predicted labels and their corresponding softmax probablities for each test image.

Right-of-way at the next intersection ( 1.0 )
Pedestrians ( 7.94515e-17 )
Double curve ( 4.22816e-17 )
Beware of ice/snow ( 2.32742e-18 )
Dangerous curve to the left ( 6.27883e-24 )

Go straight or right ( 0.999654 )
Dangerous curve to the right ( 0.0003442 )
General caution ( 1.53929e-06 )
Children crossing ( 2.12725e-07 )
Keep right ( 2.05118e-07 )

Priority road ( 1.0 )
Traffic signals ( 5.34864e-22 )
End of all speed and passing limits ( 1.1122e-24 )
Stop ( 6.70461e-28 )
No entry ( 1.31896e-31 )

Beware of ice/snow ( 0.501217 )
Road work ( 0.413236 )
Bicycles crossing ( 0.0438114 )
No entry ( 0.019929 )
Bumpy road ( 0.0091911 )

Priority road ( 1.0 )
Traffic signals ( 1.75551e-13 )
End of all speed and passing limits ( 2.60566e-14 )
End of no passing by vehicles over 3.5 metric tons ( 3.06605e-16 )
Turn right ahead ( 6.07776e-17 )

No entry ( 1.0 )
Stop ( 5.05376e-15 )
Speed limit (20km/h) ( 2.16937e-19 )
Double curve ( 5.29553e-20 )
Right-of-way at the next intersection ( 6.38568e-21 )

Stop ( 1.0 )
Speed limit (80km/h) ( 5.85452e-08 )
Speed limit (60km/h) ( 3.23047e-08 )
No entry ( 2.71293e-08 )
End of no passing by vehicles over 3.5 metric tons ( 1.99775e-08 )
