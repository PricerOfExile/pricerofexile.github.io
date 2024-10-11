Base Principles
===============

Data investigation and preparation
----------------------------------

### Requirements on the data

When we are dealing with neural network and their training, the size of the inputs matters a lot.
Roughly, for an input tensor or X element, we expect around 10X different inputs to start having decent
results.

### Outlier detection

### K-Means clustering (and elbow method)

Neural network
--------------

We use several concepts for our neural network. Such concepts will be detailed in the following sections.

> The neural network build is highly configurable, and one can choose to either apply or not some of the following concepts
(except the fundamental one s of course). 

### Perceptron and basic neural network

### Known input, known output, unknown function

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