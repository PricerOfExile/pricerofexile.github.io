Base Principles
===============

Data investigation and preparation
----------------------------------

### Requirements on the data

When we are dealing with neural network and their training, the size of the inputs matters a lot.
Roughly, for an input tensor or X element, we expect around 10X different inputs to start having decent
results.

### Outlier detection

Generally, the outliers are defined as any entry above or below a certain threshold.
This threshold is most of the time determined using the `IQR` [(Interquartile Range) method](https://en.wikipedia.org/wiki/Interquartile_range).

For the `IQR` method, we first need to determine the first and third quartile of our data set.
Then, we calculate the `IQR` as the difference between the third and first quartile.
Finally, we define the threshold as `1.5 * IQR` and any data point above or below this threshold is considered an outlier.

LEDDZIP-TODO: some visual representation would be nice


### K-Means clustering (and elbow method)

[K-means](https://en.wikipedia.org/wiki/K-means_clustering) is central in data analysis and specifically in clustering analysis. 
The base method is quite simple and consists of partitioning the data into N clusters so that
the sum of the squared distance between each element of each cluster to their centroid is minimized.

Here, for this iteration of the project at least, no need to understand the mathematical details of the method.
Only knowing that this is one of the standard ways to build clusters is enough.
Python offers a pretty decent set of scientific libraries that provide implementation of the method.
However, the clustering method used could be an optimization point on the data preparation and hence a way to build a better training set for a better model.

The elbow method, when dealing with K-Means clustering, is a way to find the optimal number of clusters to use.
We don't know the number of clusters needed, so we need a way to find it.

Here, we measure the `within-cluster sum of squares` (WCSS) for different numbers of clusters.
At some point, with the number of cluster increasing, the WCSS will decrease less and less, meaning that we might over clusterize out data set.
To find the critical number of clusters (meaning, the number that will make the WCSS decrease less faster after it), 
we plot the WCSS for different numbers of clusters and look for the `elbow` point, the point where the WCSS decrease less.

In other words, it consists of finding the point at which the tangent slopes shift from below -1 (from -90 to -45 degrees) to more than -1 (from -45 to 0 degrees).

LEDDZIP-TODO: some visual representation would be nice


Neural network
--------------

We use several concepts for our neural network. Such concepts will be detailed in the following sections.

> The neural network build is highly configurable, and one can choose to either apply or not some of the following concepts
(except the fundamental one s of course). 

### Perceptron and basic neural network

The perceptron is the atomic element of a neural network. It will hold the meta-parameter of the networks that will
change between each iteration in order to find the optimum of the network (they will be the parameter used for the gradient descend).

It consist of M number of input, a coefficient for each input (the weight of the input), a core that will do the sum of all
those weighted input, and an activation function that will determine if this sum is enough or not to activate the perceptron.

In our case, we used a simple architecture for our neural network which is the fully connected network.

While simple, it has the disadvantage that it can require a longer time and higher resources to train. But since we
want to have a configurable model, agnostic of what we want to achieve, choosing another architecture would be detrimental.

LEDDZIP-TODO: some visual representation would be nice

### Known input, known output, unknown function

Unlike conventional mathematical problem, here the issue is to find the function (or curves) that will minimize the error 
(the spread we have when applying the input to the model and the actual expected answers). 

Here, we will try to find the weights inside the different layers of our network so that the error is minimized.
Here, we have about 3.915.980 (our meta-parameters) to find and variate to find the best suited neural network that has 
an input of 940 parameters and an output of size 6.

LEDDZIP-TODO: some visual representation would be nice

### Re-injecting the gradient for gradient descent

Hidden layer after hidden layer, the gradient can easily disappear or be damped, hence reducing the effectiveness
of the gradient descent. And since optimization is basically following the gradient to find an optimum, the gradient 
loss can heavily impact the learning rate of our neural network.

While re-injecting the gradient is not always needed, especially if we work with "linear like" activation methods,
limiting ourselves to such an activation method is not reasonable since we can't easily bring non-linearity to the model.

LEDDZIP-TODO: perceptron representation of non gradient re-injection and gradient re-injection

### Batch normalisation

The base principle here is to manipulate the input of the neural network by normalizing it.

The input is re-scaled and re-centered to bring stability in the learning process and, empirically, bring better results
in neural network training. 

Here, `empirically` is used since this is still a subject under discussion to determine the real reason on the benefit it
brings. 

LEDDZIP-TODO: visual representation of what normalization mean

### unlearning 

Another optimization method of our learning process is, ironically, unlearning. By making some perceptron forgot what 
they leaned, we can potentially help the optimum search by "un-stucking" the gradient descend who reached a loop or is
descending toward a local optimum.

LEDDZIP-TODO: visual representation of stuck gradient descend AND local optimum