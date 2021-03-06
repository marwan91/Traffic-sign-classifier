# **Traffic Sign Recognition** 

## Writeup



---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/bars.jpg "Visualization"
[image2]: ./examples/equalized.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/1.jpg "Traffic Sign 1"
[image5]: ./examples/3.jpg "Traffic Sign 2"
[image6]: ./examples/11.jpg "Traffic Sign 3"
[image7]: ./examples/35.jpg "Traffic Sign 4"
[image8]: ./examples/38.jpg "Traffic Sign 5"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/marwan91/Traffic-sign-classifier/blob/master/Traffic_Sign_Classifier-final.html)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the following functions and variables to determine the sizes of the sets : .shape   , len()  ,   set()

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x3
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data ...

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to apply histogram equalization to all the images because the brightness of some images was significantly lower than the others and that caused low validation accuracy when training the neural network. after applying histogram equalization the accuracy improved.

I did not settle with converting the images to grayscale because that loweered the validation accuracy.

Here is an example of a traffic sign image before and after histogram equalization.

![alt text][image2]

As a last step, I normalized the image data because it optimizes the learning speed of the neural network.


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 25x25x9 	|
| RELU					|												|
| Max pooling	  2x2  	| 2x2 stride,  outputs 11x11x9 				|
| Convolution 5x5	    |  1x1 stride, valid padding, outputs 7x7x16 							|
| RELU					|												|
| Max pooling	  2x2  	| 2x2 stride,  outputs 4x4x16 				|
| flatten 	| convert 3d tensor to 1d tensor				|
| Fully connected		|    outputs 120     									|
|RELU				|        									|
| Fully connected		|        outputs 84  									|
|RELU				|        									|
| Fully connected		|          outputs 43									|

 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used the AdamOptimizer from the tensoflow library. I chose a learning rate of 0.001 as it is not too large to cause fluctuations in the validation accuracy, and also not too small to make the learning process slow, though , when the validation accuracy reaches 90% or above , it starts to fluctuate. A possible solution for this problem is a decaying learning rate. but in this project I used a constant rate.

The number of epochs for the training process is 12 which was the minimum to reach a suffiicient learning validation accuracy.
I went for a relatively small batch size as I found that it makes the training process significantly faster.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.912
* validation set accuracy of 0.936
* test set accuracy of 0.925


* For this project I used the LeNet architecture.
* The LeNet architecture is proven to achieve good results in image classification applications.
* With this architecture the network achieved a validation accuracy of 0.36 and test accuracy of 0.925 which is considered good performance.
* I have tweeked the architecture parameters in several ways to optimize the accuracy. I found that the larger the filter width and height of the convolutional layer the lower the accuracy becomes. and found that the greater the depth pf the convolutional layer the better the accuracy becomes.
 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]

The first image might be difficult to classify because ...

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Speed limit (30km/h)     		|Speed limit (30km/h)  									| 
| Speed limit (60km/h)    			| Speed limit (60km/h)										|
| Right-of-way at the next intersection				|Right-of-way at the next intersection										|
|Ahead only     		|Ahead only				 				|
| Keep right			| Keep right  							|


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a 'Speed limit (30km/h)' sign (probability of 0.99), and the image does contain a 'Speed limit (30km/h)' sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 0.999        			|Speed limit (30km/h)  									| 
| 0.00006     				|Speed limit (20km/h)										|
| 0.000003					|Speed limit (80km/h)										|
|0.0000004     			|Speed limit (70km/h)					 				|
| 0.0000001				    | Speed limit (50km/h)     							|


For the second image , the model is relatively sure that this is a 'Speed limit (60km/h)' sign (probability of 0.982), and the image does contain a 'Speed limit (30km/h)' sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 0.982         			|Speed limit (60km/h)  									| 
| 0.017    				|Speed limit (50km/h)										|
| 0.0000007				|Speed limit (80km/h)										|
|0.00000001   			|Wild animals crossing				 				|
|0.000000001				    |Dangerous curve to the left    							|

For the third image , the model is relatively sure that this is a 'Right-of-way at the next intersection
' sign (probability of 0.985), and the image does contain a 'Right-of-way at the next intersection
' sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 0.985       			|Right-of-way at the next intersection  									| 
| 0.011   				|Beware of ice/snow									|
| 0.002				|Pedestrians										|
|0.00009   			|General caution			 				|
|0.0000005		    |Dangerous curve to the right  		|

For the fourth image , the model is relatively sure that this is a 'Ahead only' 
sign (probability of 0.999), and the image does contain a 'Ahead only' sign. 
The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 0.999       			|Ahead only					| 
| 0.0000002   				|Roundabout mandatory							|
|0.00000008		|	Go straight or right								|
|0.000000001  			|Turn right ahead 				|
|0.00000000002	    |Turn left ahead 		|


For the fifth image , the model is relatively sure that this is a 'Keep right' sign (probability of 0.999), and the image does contain a 'Keep right' sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 0.999       			|Keep right  									| 
| 0.0000002    				|Roundabout mandatory									|
| 0.00000000008		|Go straight or right									|
|0.00000000005  			|Turn left ahead	 				|
|0.00000000001			    |Priority road   							|

