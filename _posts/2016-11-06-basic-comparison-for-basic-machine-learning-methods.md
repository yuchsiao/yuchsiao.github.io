---
title: Basic Comparison for basic machine learning methods
tags: [machine learning, comparison]
---

This article summarizes the following post

+ [How true is this slide on deep learning](https://www.quora.com/How-true-is-this-slide-on-deep-learning)


## Logistic Regression

+ For linearly separable data
+ Pretty robust. Can avoid overfitting by l1 or l2 regularization
+ Easily distributable
+ Get probability. Can do ranking directly
+ With l2 regularization, LR can be used as a baseline for any other fancier solutions
+ Not so good for categorical variables
+ Then go for SVM for Tree Ensembles models
+ Discriminative model
+ Can be online. Just update with new data using online gradient descent

## Naive Bayes 

+ Simple. Just do a bunch of counts.
+ Can be used as a baseline as well (just don't dismiss it... yet)
+ High bias and low variance. But still useful for small data size [Domingos](http://web.cs.ucdavis.edu/~vemuri/classes/ecs271/Bayesian.pdf)
+ Low variance means less likely to overfit
+ Generative model

## SVM

+ Hinge loss
+ Maximum margin
+ Quite a few nonlinear kernels (probably better than LR with a nonlinear transformation)
+ Good for high dimensional space. 
+ Reported better for text classification problems
+ Inefficient training. Not for industry-scale applications
+ Memory intensive

## Tree Ensembles

+ Good for high dimensional space
+ Good for nonlinear variables
+ Good for categorical variables
+ Non-parametric. Don't need to worry about outliers or linearly separable.

### Random Forest

+ Usually work out of box

### Gradient Boost Tree

+ Generally perform better, if getting it right
+ More hyper-parameters to tune
+ Prone to overfitting

## Deep Learning

+ Not general-purpose
+ Applied when you believe you can still squeeze more after trying above

## Interesting reading

+ [Do we need hundreds of classifiers to solve real world classification problems?](http://jmlr.org/papers/volume15/delgado14a/delgado14a.pdf)


# Off topic below

## Deep learning development

### Supervised learning

+ Better initialization: introduced in 2010
+ ReLu: introduced in 2011
+ Dropout: a better regularizer in 2014
+ RNN cannot remember things for more than a couple of steps long back then.
+ Momentum
+ Dropcoeonnect
+ Maxout

### Unsupervised learning

+ Pure unsupervised learning
+ Transfer learning 
+ Semi-supervised learning 
+ Domain adaptation
+ Self-taught learning

## ML in late 90's 

+ SVM and convex optimization
+ L1 regularization and sparsity
+ Automated feature detecteion like NMF

## Potentially interesting readings

+ [Why does deep learning work?](https://charlesmartin14.wordpress.com/2015/03/25/why-does-deep-learning-work/)
+ [Why does deep learning work II](https://charlesmartin14.wordpress.com/2015/04/01/why-deep-learning-works-ii-the-renormalization-group/)

## Some quotes

>Better data often beats better algorithms.

>All learning is non-convex.


