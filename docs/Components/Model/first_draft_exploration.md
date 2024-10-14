First Draft: Exploration
========================

The first draft was exclusively exploratory. We had a set of 1000 items, not fully formatted.
But it was enough to start a little refresher on the different algorithm and tool we will use,
bot the analysis and the modeling.

The notebooks:

- data-exploration.ipynb
- data-exploration-outlier-removal.ipynb
- data-exploration-no-removal.ipynb
- data-transformation.ipynb
- model-simulation.ipynb 

were all part of this exploratory phase.

## outliers

The biggest concern we had was the outliers and how to deal with them?

Usually we simply exclude them. They have a value so different from the others that they could introduce error in the all process
and are most of the time mistakes.

Here, it is a little different. While removing them indeed show better graph, we should keep most of them and rely on our 
subject matter expert to differentiate between an outlier and an actual value.

This is mandatory since the pricing is not linear between sections and one value that is detected as an outlier could be an actually good object.

> **Further analysis:** something to explore would be to do the analysis on the log scale. 
It should remove the explosion on the price on some items while still allowing to determine the clusters and identify true outliers.


## training

This one was purely experimental. We generated 1000 random data following a mean and variance for each estimated clusters.

We did this to have a first model architecture with all the different optimization method we wanted to be able to use.

The highly configurable nature of our neural network mainly come from this part.

Another interesting part or this training, and the generation of random data, was that we already see an issue in clusterization 
that will hinder the performance of our v2 model (and fixed in our v3 model). Basically, the way those random data are built,
make the clusterization mostly focused on the highest values where 3 clusters where wrongly identified in one group of data.

> Thanks to this, we know that we should not blindly rely on the clusterization method and we should be critics on the results.