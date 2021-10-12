# 🖥️ KNN algorithm

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com) [![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)](http://forthebadge.com)

Python project about the K-Nearest Neighbors Algorithm.

In this project, we will use the KNN algorithm to solve a classification problem. The output of our classification problem is to predict the class (class A, B, C, D, or E) of the new combinations given in the finalTest.csv file. Combinations are numbers. To train our algorithm we have two training data files which are preTest.csv and data.csv.

## Installation

Download the 3 csv files (data, preTest, finalTest) and place them in one folder somewhere.

Change the line number 12 by the path where you put the csv files.
```python
file = open(r"C:\Users\your_user\...\the_folder_you_put_them\{}.csv".format(nomdufichier),"r")
```
Change also the line number 130 by the place you want to place the predictions.
```python
myfile = open(r"C:\Users\your_user\...\prediction.txt", "w+")
```
For this project we will use the following libraries :
```python
import csv # to read the  csv files
import time # to calculate how much time did the algorithm took
```
Use the package manager [pip](https://pip.pypa.io/en/stable/) if you don't have them.

## The KNN algorithm

### Selection of the number K and the distance calculation method

A very low value for K can lead to errors in the model and large values for K are good, but it may find some difficulties. So we did some tests with our training data using different methods to calculate the distance to find the best K.

The most popular distance metric is the Euclidian distance. But there are other ways of calculating distance, and one way might be preferable depending on the problem we are solving. We will test Euclidian distance, Manhattan distance, and Tchebychev distance. 

* Euclidian distance d = √(x2 - x1)² + (y2 - y1)²
* Manhattan distance d = |x1-x2| + |y1-y2|
* Tchebychev distance d = max(|x1-x2|,|y1-y2|)

To find the best method to calculate the distance and then the best K we will take the training data from data.csv deleting the classes and predict the classes, using our algorithm that we will explain after, by using the same data again as training data but with the outputs. Thus we will have the satisfaction rate we will decide what distance method is the best and with which K. We will use the following function :

```python
def compare(train,test,k):
  same = 0
  for i in range(len(test)):
    if(train[i]["class"] == attribution(k,train,test[i])):
      same += 1
  satisfaction = (same/len(test))*100
  print("for k = ", k, " satisfaction rate :",satisfaction,"%") 
```

Using this function we have.

(taux de satisfaction photos)

Base on the test we did we can see the Manhattan distance is the best method to calculate the distance with our algorithm. Furthermore, with the K value equal to 5 we have a 91.15% satisfaction rate.

Using this method again, we find that the best K value for the preTest.csv file is K = 4. We will also create a last training dataset unifying both data from data.csv and preTest.csv. For this training dataset that we will call _both_ we find the best K = 4.

### Take the K nearest neighbors and predict the class of the combination



## Note

The python code and the report are in French but do not hesitate to contact me if you want more details in English.

### Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
