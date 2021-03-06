# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/hist.png "Visualization"
[image2]: ./examples/random_sign.png "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/ni40in/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32 x 32
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a histogram showing the dictribution of the training set over the categories. We can see that it's quite imbalanced with some categories having x10 times more samples than others. However, the training still achieved reasonable accuracy so we won't worry too much about equalizing the distribution.

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

I've decided to keep things simple and just normalized the data as a preprocessing step. For that, I have converted the arrays into numpy and changed the data type to float. Then I substracted the mean value from every pixel and divided by mean (standard scaling).


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x16 |
| RELU					|												|
| Max pooling	      	| 2x2 stride, valid padding, outputs 5x5x16 				|
| Flatten	      	| input 5x5x16, outputs 400	|
| Fully connected		| input 400, outputs 200	|
| RELU					|												|
| Fully connected		| input 200, outputs 100	|
| RELU					|												|
| Fully connected		| input 100, outputs 43 (number of classes)	|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I coded a version of LeNet. Used batch size of 128 and ran it for 15 of epochs. Learning rate was set to 0.0005.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 99.7%
* validation set accuracy of 93.3%
* test set accuracy of 91.8%

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?
Initially i went LeNet architecture.
* What were some problems with the initial architecture?
the highest accuracy I was able to achieve was about 90.5%. I've introduced some minor changes in the fully connected layers but not sure if the effect was significant. 
* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
* Which parameters were tuned? How were they adjusted and why?
I've changed learning rate and batch size. Lower learning rate and larger number of epochs helped to achieve the result.
* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?
Haven't used the dropout because was able to achieve desired accuracy. Can guess that dropout can help against overfitting so the network will get better at generalizing.

If a well known architecture was chosen:
* What architecture was chosen?
* Why did you believe it would be relevant to the traffic sign application?
* How does the final model's accuracy on the training, validation and test set provide evidence that the model is working well?
 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

<img src="./examples/1.jpeg" alt="Traffic Sign 1" height="150"> <img src="./examples/2.jpeg" alt="Traffic Sign 2" height="150"> <img src="./examples/3.jpeg" alt="Traffic Sign 3" height="150"> <img src="./examples/5.jpeg" alt="Traffic Sign 4" height="150"> <img src="./examples/6.jpeg" alt="Traffic Sign 5" height="150">

All the images were of good quality and shoudn't pose any difficulties for the model to predict them correctly. I had to resize and center crop the images to have them in correct size for the model consumption.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Speed limit (30 km/h)      		| Speed limit (30 km/h)   									| 
| Road work     			| Road work 										|
| Right-of-way at the next intersection					| Right-of-way at the next intersection											|
| Go straight or right	      		| Speed limit (80 km/h)					 				|
| Railroad intersection			| Slippery Road      							|


First three images were predicted correctly but the third one is completely wrong. Such sign is present in the training set, so i have no reasonable explanation about why the prediction is so off.
The last image prediction might be off because of the resizing and these two signs actually do look somewhat alike, especially when blurry/low res.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For some reason, the model was 100% confident when giving predictions to the web test images. I coudln't find the root cause of the problem

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1         			| Speed limit (30 km/h)   									| 
| 1     				| Road work 										|
| 1					| Right-of-way at the next intersection											|
| 1	      			| Go straight or right					 				|
| 1				    | Railroad intersection      							|


For the second image ... 

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


