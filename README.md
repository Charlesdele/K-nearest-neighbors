# 🖥️ KNN algorithm

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com) [![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)](http://forthebadge.com)

<img src=https://user-images.githubusercontent.com/63778269/136999590-e56014f0-6f45-469c-bf29-a8550e77f3d8.png width=400/>

Python project about the K-Nearest Neighbors Algorithm.

In this project, we will use the KNN algorithm to solve a **classification problem**. The output of our classification problem is to predict the class (class A, B, C, D, or E) of the new combinations given in the _finalTest.csv_ file. Combinations are numbers. To train our algorithm we have two training data files which are _preTest.csv_ and _data.csv_.

<br/>

## Set up

Download the 3 csv files _(data, preTest, finalTest)_ and place them in one folder somewhere.

Change the line **number 12** by the path where you put the csv files.
```python
file = open(r"C:\Users\your_user\...\the_folder_you_put_them\{}.csv".format(nomdufichier),"r")
```
Change also the line **number 130** by the place you want to place the predictions.
```python
myfile = open(r"C:\Users\your_user\...\prediction.txt", "w+")
```
For this project we will use the following libraries :
```python
import csv # to read the  csv files
import time # to calculate how much time did the algorithm took
```
Use the package manager [pip](https://pip.pypa.io/en/stable/) if you don't have them.

<br/>

## The KNN algorithm

### Selection of the number K and the distance calculation method

A very low value for K can lead to errors in the model and large values for K are good, but it may find some difficulties. So we did some tests with our training data using different methods to calculate the distance to find the best K.

The most popular distance metric is the Euclidian distance. But there are other ways of calculating distance, and one way might be preferable depending on the problem we are solving. We will test Euclidian distance, Manhattan distance, and Tchebychev distance. 

* **Euclidian distance** : d = √(x2 - x1)² + (y2 - y1)²
* **Manhattan distance** : d = |x1-x2| + |y1-y2|
* **Tchebychev distance** : d = max(|x1-x2|,|y1-y2|)

To find the best method to calculate the distance and then the best K we will take the training data from _data.csv_ deleting the classes and predict the classes, using our algorithm that we will explain after, by using the same data again as training data but with the outputs. Thus we will have the satisfaction rate we will decide what distance method is the best and with which K. We will use the following function :

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

<img src = https://user-images.githubusercontent.com/63778269/137002363-609faff3-10ea-42ba-8798-0542ebd8cd43.PNG width = 900/>

Base on the test we did we can see the **Manhattan distance** is the best method to calculate the distance with our algorithm. Furthermore, with the K value equal to **5** we have a **91.15% satisfaction rate**.

Using this method again, we find that the best K value for the _preTest.csv_ file is **K = 4**. We will also create a last training dataset unifying both data from _data.csv_ and _preTest.csv_. For this training dataset that we will call _both_ we find the best **K = 4**.

### Take the K nearest neighbors and predict the class of the new combinations

To predict the class of the combinations in the finalTest.csv file. We're gonna use our KNN algorithm 3 times. We will predict the class of the new combinations data using 3 different training dataset: the preTest.csv file, the data.csv file, and the union of both. 

<img src = https://user-images.githubusercontent.com/63778269/136999678-6e72a6f2-a1a9-4305-9528-406cb373e1e5.PNG width = 600/>

To predict the class of the new combination we will use the KNN principle with the function **k_plus_proches(k,table,nouveau)** which returns a list of the K nearest neighbors depending on their distance from the new combination calculated with the function **distance_manhattan(data1,data2)**. 

Now we need to find the most frequent class, among this list of the K nearest neighbors. That's why we will call the **class_majoritaire(table)** function which will return the most frequent class among this list by counting how many times each class appears in the k-nearest neighbors list thanks to the function **frequence_class(table)**.

To finish we will take the most frequent prediction, for each combination we predicted the class, between the 3 ones we found and write all the final predictions in a text file. This is what the function **final_prediction(data,preTest,both)** does.

## Note

The python code and the report are in French but do not hesitate to contact me if you want more details in English.

### Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
