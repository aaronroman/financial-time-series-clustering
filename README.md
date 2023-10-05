![Header](https://raw.githubusercontent.com/aaronroman/financial-time-series-clustering/main/img/header.png)
# Financial time-series clustering
This is a small example of how to create new features from a financial time series, then apply a clustering algorithm to group similar financial assets together. The data used is the daily closing prices of some random USA stocks, from 2015 to 2023. The clustering algorithm used is the K-means algorithm, and the features are created using just the smooth adjusted closing prices.

## Params
```
sma_window = 5
cluster_window = 50
window_offset = 10
```
`sma_windows` the window size for calculating the moving average; a larger value will result in a smoother curve
`cluster_window` the length of days the time series will have and consequently the length of the feature vectors
`window_offset` the number of days to skip when creating the feature vectors, it's just for speeding up the process

## Segmentation
In order to train our model we need a dataset with shape `(n_samples, cluster_window)`. We do so creating chunks of every time series with length `cluster_window` and skipping `window_offset` days. The result is a dataset with shape `(n_samples, cluster_window)`, where `n_samples` is the number of chunks created.
![Segments](https://raw.githubusercontent.com/aaronroman/financial-time-series-clustering/main/img/segments.png)

## Scaling / Normalization
I found that scaling the data works well for this problem. I used the `MinMaxScaler` from `sklearn.preprocessing` to scale the data between 0 and 1. The result is a dataset with shape `(n_samples, cluster_window)`, where `n_samples` is the number of chunks created, and each sample is scaled between 0 and 1. Now every timeserie y able to be compared with the others.

## Finding the optimal number of clusters
With the elbow method we can find the optimal number of clusters for our dataset. The elbow method consists in plotting the sum of squared distances of samples to their closest cluster center for different values of `k` and choosing the `k` for which the curve starts to flatten out. In our case, the curve starts to flatten out at `k~100`, but we choose `k=10` only to make the visualization easier.

![Elbow curve](https://raw.githubusercontent.com/aaronroman/financial-time-series-clustering/main/img/elbow.png)

## Results
As we can see in the plot, the algorithm was able to group similar stocks together. The stocks in the same cluster have similar price movements, and the stocks in different clusters have different price movements.
![Elbow curve](https://raw.githubusercontent.com/aaronroman/financial-time-series-clustering/main/img/centroids.png)
![Elbow curve](https://raw.githubusercontent.com/aaronroman/financial-time-series-clustering/main/img/output_example.png)

## Improvements
- Use more data (more stocks and more time)
- Set SMA to a confortable value for you
- Check the elbow method to find the best number of clusters
- Use other clustering algorithms
- Use other distance metrics
- Use other dimensionality reduction algorithms

## Conclusions
In this example we saw how to create new features from a financial time series with very low effort, and how to use those features to cluster similar financial assets together. There are many other ways to create features from a financial time series, and many other clustering algorithms to use, but I think this example is a good starting point for anyone who wants to start experimenting with financial time series clustering.

I hope this example was useful for you. If you have any questions or suggestions, please let me know. Thanks for reading!

### How to reach me
<a href="https://linkedin.com/in/aaronroman"><img src="https://img.shields.io/badge/-aaronroman-gray?style=flat-square&logo=Linkedin&logoColor=white&link=https://linkedin.com/in/aaronroman/"></a>
<a href="https://twitter.com/aaronroman"><img src="https://img.shields.io/badge/-aaronroman-blue?style=flat-square&logo=Twitter&logoColor=white&link=https://twitter.com/aaronroman"></a>