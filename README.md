# Implementation of a classifier based on a grid-based clustering algorithm
Here we are implementing a classifier based on a grid-based clustering algorithm called *clique algorithm*.

## Clique Algorithm
The `pyclustering` library provides the implementation of Clique. However, it does not offer any **predict** function to be used in a **classification problem**; therefore, I implemented a wrapper that contains a predict function. The predict function required two things:

1. Recognizing the category(cluster) of given input(x) in that specific clustering model
The clique algorithm will divide the space into a number of grids, which are based on the interval argument of the model; These grids are called **cells**. The `__contains__` function implemented for these cells will tell us whether a specific coordinate belongs to them or not. Unfortunately, this part might be time-consuming, especially if the number of cells is high.

This library will not give us the information about what category cell's points belong to, so I labeled all cells by checking one of its points' cluster and labeling the whole cell with that cluster's label. This is true because, actually, this algorithm categorizes all of one grid's data into one cluster. Additionally, those cells whose points did not belong to any cluster are considered noise and will inherit the label of the noise cluster.

2. Labeling clusters with true categories(y)
Every cluster will be labeled to the actual label of the majority of its points. The noise cluster is not exceptional.