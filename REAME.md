## Data Set Summary & Exploration

### Summary Of Data Set

I used Pickle and Panda to open and read the Data set files. Since they have been structured as Dictionaries, easily stored the data 
in train , test and validation lists.
Training set includes 34799 samples, so the size of training set is 34799. We use this data set to train our model. 
Validation set includes 4410 samples, so the size of our Validation set is 4410. We use this set to validate our model. Test set is 
the part of data seperated for the final evaluation of our model and will not be introudeced to model during the trainig or validation,
untill the tuning of our hyper parameters is done. The size of our Test set 12630.
The shape of a traffic sign image is 32 by 32 pixels, in 3 channels(3 colors). So the depth of our images is 3 and width and height of
them are both 32.
I used Panda to read the Labels in our "signnames.csv" and extract the number of unist labels/class we have for our classifier, which is
43 unique classes.

### Exploratory visualization of the dataset

Here is an exploratory visualization of the data set. I have used matplotlib to plot a histogram of y_train to show how many of images
are in each class.
