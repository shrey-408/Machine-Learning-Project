# Machine-Learning-Project

# Hybrid Clustering for Stock Price Analysis

[cite\_start]This project identifies natural clusters and detects anomalies in historical stock price data using a hybrid clustering approach that combines KMeans and DBSCAN[cite: 1]. [cite\_start]The goal is to group stocks or stock-days with similar behavior while identifying unusual patterns or outliers, which can be useful for financial analysis and anomaly detection[cite: 1].

-----

## Problem Statement

[cite\_start]The core problem is to effectively cluster historical stock data to understand market behavior and identify anomalies that may signal significant events[cite: 1].

  * [cite\_start]**KMeans** is fast and efficient for finding spherical clusters but struggles with complex shapes and can be sensitive to outliers, often misclassifying them by forcing them into a cluster[cite: 1].
  * [cite\_start]**DBSCAN** excels at identifying arbitrarily shaped clusters and noise (anomalies) but can be computationally expensive on large datasets and may struggle with clusters of varying densities[cite: 1].

[cite\_start]Our hybrid approach leverages the strengths of both algorithms: KMeans for initial, efficient clustering, and DBSCAN for refining these clusters and flagging outliers[cite: 1]. [cite\_start]This method allows for both structured clustering and robust anomaly detection, providing a more comprehensive view of the data than either algorithm could offer alone[cite: 1].

-----

## Data

The project uses historical stock price data from NASDAQ. The provided `NASDAQ.csv` file contains daily stock information with the following features:

  * [cite\_start]**Date**: The date of the trading day[cite: 1].
  * [cite\_start]**Close/Last**: The closing price of the stock[cite: 1].
  * [cite\_start]**Open**: The opening price of the stock[cite: 1].
  * [cite\_start]**High**: The highest price of the stock during the day[cite: 1].
  * [cite\_start]**Low**: The lowest price of the stock during the day[cite: 1].
  * [cite\_start]**Volume**: The number of shares traded (Note: While present in the raw data, this feature was not used in the provided analysis code)[cite: 1].

[cite\_start]The analysis focuses on the numerical features: **Open**, **High**, **Low**, and **Close/Last**[cite: 1].

-----

## Code

[cite\_start]The analysis is performed in a Python Jupyter Notebook (`PythonCode.ipynb`) using popular data science libraries like `pandas`, `numpy`, and `matplotlib`[cite: 1].

### Dependencies

To run the notebook, you'll need the following libraries:

  * `pandas`
  * `numpy`
  * `matplotlib`
  * `collections` (a standard Python library)

You can install the required packages using pip:

```bash
pip install pandas numpy matplotlib
```

### Key Steps in the Notebook

1.  **Data Loading and Preprocessing**:

      * [cite\_start]The `NASDAQ.csv` file is loaded into a pandas DataFrame[cite: 1].
      * [cite\_start]The `Date` column is converted to datetime objects[cite: 1].
      * [cite\_start]The numerical features (`Open`, `High`, `Low`, and `Close/Last`) are extracted and **normalized** to ensure all features contribute equally to the distance calculations[cite: 1].

2.  **KMeans Clustering**:

      * [cite\_start]A custom implementation of the KMeans algorithm is used[cite: 1].
      * [cite\_start]**Centroid Initialization**: A predefined number of clusters ($k=3$) is set, and centroids are randomly chosen from the data points[cite: 1].
      * [cite\_start]**Iteration**: The algorithm iteratively assigns points to the nearest centroid and updates the centroids to be the mean of the assigned points[cite: 1]. [cite\_start]This process continues until the centroids no longer change significantly, indicating convergence[cite: 1].

3.  **DBSCAN Clustering**:

      * [cite\_start]A custom DBSCAN algorithm is implemented to operate on the data[cite: 1].
      * [cite\_start]**Parameters**: The algorithm uses two key parameters: `eps` and `min_samples`[cite: 1].
          * $N\_\\epsilon(x\_i) = {x\_j | ||x\_i - x\_j|| [cite\_start]\\leq \\epsilon}$ defines the $\\epsilon$-neighborhood of a point $x\_i$[cite: 1].
          * [cite\_start]A point is a **core point** if it has at least `min_samples` in its $\\epsilon$-neighborhood[cite: 1].
          * [cite\_start]A **border point** is within a core point's $\\epsilon$-neighborhood but has fewer than `min_samples` itself[cite: 1].
          * [cite\_start]**Noise** is any point that is neither a core point nor a border point[cite: 1].
      * [cite\_start]**Cluster Expansion**: The algorithm identifies core points and expands clusters by recursively including density-reachable points, leaving unclustered points as noise[cite: 1].

4.  **Hybrid Approach**:

      * [cite\_start]KMeans is run first to get initial cluster labels for each data point[cite: 1].
      * [cite\_start]Then, DBSCAN is applied **within each of the KMeans clusters**[cite: 1]. [cite\_start]This local application of DBSCAN is computationally more efficient and effective at identifying noise points and refining the cluster boundaries[cite: 1].
      * [cite\_start]The final output includes the hybrid cluster assignments, where noise points are typically labeled as `-1`[cite: 1].



### Data Visualization

### Clustering Results

The final scatter plot visualizes the data points colored by their hybrid cluster labels. [cite\_start]Anomalies identified by DBSCAN are marked with a distinct color and are labeled with -1, clearly showing how the hybrid method can partition the data into meaningful groups while also isolating unusual data points[cite: 1].
