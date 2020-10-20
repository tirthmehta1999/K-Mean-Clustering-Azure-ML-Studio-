# K-Mean-Clustering-Azure-ML-Studio-

# 1.	Problem faced by the business
The business has developed a product which can be used by various companies to ease their work and improve efficiency. Now, they want to know which companies to target so that with their limited marketing resources they could achieve more sales.

# 2.	Approach/ Methodology followed by the business

The business clustered similar companies into same group given their Wikipedia articles and this can also be used to assign cluster to new company.
The business used K-Means clustering algorithm to perform segmentation on companies from the Standard & Poor (S&P) 500 index, based on the text of Wikipedia articles about each company.

K-Means algorithm is an iterative algorithm that tries to partition the dataset into K pre-defined distinct non-overlapping subgroups (clusters) where each data point belongs to only one group.
The way K-Means algorithm works is as follows:
1.	Specify number of clusters K.
2.	Initialize centroids by first shuffling the dataset and then randomly selecting K data points for the centroids without replacement.
3.	Keep iterating until there is no change to the centroids. i.e assignment of data points to clusters isn’t changing.
4.	Compute the sum of the squared distance between data points and all centroids.
5.	Assign each data point to the closest cluster (centroid).
6.	Compute the centroids for the clusters by taking the average of the all data points that belong to each cluster.

# Model
First, the contents of each Wiki article were passed to the Feature Hashing module, which tokenizes the text string and then transforms the data into a series of numbers, based on the hash value of each token.
Even with this transformation, the dimensionality of the data is too high and sparse to be used by the K-Means clustering algorithm directly. Therefore, Principal Component Analysis (PCA) was applied using a custom R script in the Execute R Script module to reduce the dimensionality to 10 variables. You can review the result of PCA by double-clicking the right-hand output of the Execute R Script R module.
From trial and error, we learned that the first variable in the PCA transformed data had the highest variance and appears to have had a detrimental effect on clustering. Therefore, we removed it from the feature set using Project Columns.
Once the data was prepared, we created several different instances of the K-Means Clustering module and trained models on the text data. By trial and error, we found that the best results were obtained with 3 clusters, but models using 4 and 5 clusters were also tried.
Finally, we used Metadata Editor to change the cluster labels into categorical values, and saved the results in CSV format for downloading, using Convert to CSV module.

# 3.	Skillsets , infrastructure and other impact on the business during implementation 
Results:
To view the results:
1.	Right-click the output from Metadata Editor and select Visualize.
 
2.	Plot the Category column (a known feature from the Wikipedia data) against the Assignments columns.
 
The three clusters that we obtained correspond roughly to three plausible categories. Note that the clusters are not clearly delineated.
