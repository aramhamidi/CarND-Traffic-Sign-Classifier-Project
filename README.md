## Data Set Summary & Exploration

### Summary Of Data Set

I used *Pickle* and *Panda* to load the data set files. Since they have been structured as Dictionaries, easily stored the data in train, test and validation lists.

Training set includes 34799 samples, so the size of training set is 34799. We use this data set to train our model. 

Validation set includes 4410 samples, so the size of our Validation set is 4410. We use this set to validate our model. 

Test set is the part of data seperated for the final evaluation of our model and will not be introudeced to model during the trainig or validation, untill the tuning of our hyper-parameters is done. The size of our Test set 12630.

The shape of a traffic sign image is 32 by 32 pixels, in 3 channels(3 colors). So the depth of our images is 3 and width and height of
them are both 32.

I used Panda to read the Labels provided in *"signnames.csv"* and extract the number of unist labels/class we have for our classifier, which is 43 unique classes.

### Exploratory visualization of the dataset

Here is an exploratory visualization of the data set. I have used matplotlib to plot a histogram of y_train to show how many of images
are in each class.

![alt text](https://github.com/aramhamidi/CarND-Traffic-Sign-Classifier-Project/blob/master/image06.png)

### Design and Test a Model Architecture

**Preprocessing**

I tried training my model with both grayscale images and RGB colored images. However I got better accuracy result using colored images so I chose to not to go with grayscaling them.

I have also normalized the image pixels. My understanding is that of the pixel values are normalized between 0 to 1 with covariance of 1, traingin the CNN would be much easier. Having the real values of pixels will add un-necessary information to our set, and the CNN needs to learn about all those information as well, while it is not needed. For example in our case, there should not be any differentce between a traffic sign image taken in day light or evening time, both of them should be interpreted the same. So here the brightness of picture is additional information which our CNN does not need to care about.

I have also shuffled the trainig set just to make sure, training process is not biased by the order of images. Here is a sample of the difference between a normalized and regular image:

<image>
  
### Model Architecture

Final model consisted of the following Five layers:


|    Layer      |               | Describtion|
| ------------- |:-------------:|:-----------:|
|       1       |     input     | 32x32x3 RGB image|
|       1       |Convolution 5x5| 1x1 stride, valid padding, outputs 28x28x6 |
|       1       |      ELU      |  -                                          |
|       1       |Max pooling 2x2| 2x2 stride, valid padding, outputs 14x14x6 |
|       2       |     input     | 14x14x6 RGB image                          |
|       2       |Convolution 5x5| 1x1 stride, valid padding, outputs 10x10x16|
|       2       |      ELU      |   -                                         |
|       2       |Max pooling 2x2| 2x2 stride, valid padding, outputs 14x14x6 |
|       2       |    flattern   | outputs 400                                |
|       3       |     input     | 400                                        |
|       3       |Convolution 5x5|Fully Connected, outputs 120                |
|       3       |      ELU      |   -                                         |
|       3       |    Dropout    | keep_prob = 0.7                            |
|       4       |     input     | 120                                        |
|       4       |Convolution 5x5| Fully Connected, outputs 84                |
|       4       |      ELU      |  -                                          |
|       4       |    Dropout    | keep_prob = 0.7                            |
|       5       |     input     | 120                                        |
|       5       |Convolution 5x5| Fully Connected, outputs 43                |



As you can see dropouts are used with keep_prob = 0.7 in each fully connected layers 4 and 5. I have also noticed if I use Elu function instead of ReLu as activation, results have better accuracy.

### Train, Validate and Test 

To train the model, I used learning rate of 0.001, with 15 epoches each with size of 128. I hgave also used Adam Optimizer algorithm, which is more sophisticated than

As you can see I have used dropouts with keep_prob = 0.7 in each fully connected layers 4 and 5. I have also noticed if I use Elu function instead of ReLu as activation I can get better accuracy results.

**Final Model Results**

validation set accuracy of 0.937 test set accuracy of 0.912 accuracy of downloaded images set of 0.6 or 60%.

### Model Test Results on New Images

Here are five German traffic signs that I found on the web:

![alt text](https://github.com/aramhamidi/CarND-Traffic-Sign-Classifier-Project/blob/master/image01.jpeg)
![alt text](https://github.com/aramhamidi/CarND-Traffic-Sign-Classifier-Project/blob/master/image02.jpeg)
![alt text](https://github.com/aramhamidi/CarND-Traffic-Sign-Classifier-Project/blob/master/image03.jpeg)
![alt text](https://github.com/aramhamidi/CarND-Traffic-Sign-Classifier-Project/blob/master/image04.jpeg)
![alt text](https://github.com/aramhamidi/CarND-Traffic-Sign-Classifier-Project/blob/master/image05.jpeg)
         

Preprocessing for test images was pretty much the same as preprocessing on training set, including normalizing images, however I needed to resize these pictures to 32x32 pixels images to be able to feed to the classifier. Since I skiped grayscaling my training set, I did the same for these images as well.

The first 5 images which I tried my classifier with, gave me an accuracy as low as 40%. Then I realized the reason might be the low resolution of the original images downloaded from the web. So found another 5 images with better resolutions and I made sure that the correct labels for these images exist in among 43 classes. I manually extracted those labels and compared them with the result of my classifier, which turned out to be right 3 out of 5 images, or 60%. Although this accuracy is much lower than the test set, but some how it make sense, because I am using only 5 images, in my test case and these 5 images, might not be German Traffic Signs exatly.

Here are the result of predictions:
correct labels: [ 1 12 18 27 14] predictions: [ 1 12 18 19 12]

And my 5 top Softmax Probabilities are [19, 18, 12, 12, 1] for indices [3, 2, 1, 4, 0].
