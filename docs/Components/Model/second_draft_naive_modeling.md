Second Draft: Naive Modeling
=============================

Here we started to have the actual values (50.000-ish of them), correctly formatted.

The sheer number of data introduced some challenge with github and how to store the files.

## Cluster determination

We used outliers detection to find if there are outliers. However, based on this method,
we had too many outliers, which was suspicious.

Our subject matter expect told us that, indeed, some values of those outliers are well priced.

To find out the real outliers, we applied the outliers detection multiple times, each iteration on the output of the previous iteration.

As a result, we applied this process four times and found out there were... 10 outliers out of 50.000.

> here we have the feeling that each application of outlier detection is actually able to
find clusters candidate for non common value.

We identified 3 clusters with this method. Then we applied the elbow method on the
items detected as non-outliers on the first outlier detention. We found out 3 potential clusters.

Finally, we applied the k-means method to find 6 clusters among all the non outliers and the false outliers.

## training

The training did not deviate from what we put in place in the first draft. However the results were odd.

A deeper investigation shown that the clusters were built wrongly. The first cluster had
around 48.000 elements and the remaining 5 had between 100 and 20 elements.

With such a clusterization, it is impossible to have decent results.
