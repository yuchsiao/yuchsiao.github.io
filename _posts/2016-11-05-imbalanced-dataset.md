---
title: Handling of Imbalanced Dataset in ML
tags: [machine learning, imbalanced]
---

This post collects and summarizes the methods from the following posts

+ Basic: [8 Tactics to Combat Imbalanced Classes in Your Machine Learning Dataset](http://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/) by Jason Brownlee
+ Basic: [In classification, how do you handle an unbalanced training set?](https://www.quora.com/In-classification-how-do-you-handle-an-unbalanced-training-set) from Quora
+ Intermediate: [Learning Imbalanced Classes](http://svds.com/learning-imbalanced-classes/) from SVDS blog
+ Advanced: [Classification when 80% of my training set is of one class](https://www.reddit.com/r/MachineLearning/comments/12evgi/classification_when_80_of_my_training_set_is_of/) from Reddit
+ Advanced: [He2009](http://www.ele.uri.edu/faculty/he/PDFfiles/ImbalancedLearning.pdf). Looks an awesome reading.
+ Library: [scikit-learn-contrib/imbalanced-learn](https://github.com/scikit-learn-contrib/imbalanced-learn)

## The Big Picture

The first thing of all is using the proper metric. If the classes are very much skewed, precision-recall curve is better than ROC. However, experience also taught me that if the minority samples in the test set are too few, PR curve may give a zigzag shape of the curve, which is in turn numerically unstable in estimating the area under the curve.

The common strategy for imbalanced learning is to resample the dataset, if getting more data is not an option. Resampling can be either over-sampling, under-sampling, or over-sampling followed by under-sampling, mixed with certain ensample strategies. Over-sampling can be done in a naive way, or use SMOTE-like method to generate synthetic samples. Similarly, under-sampling can be done just taking few samples from the majority class, or in a more informed process, by looking at the potential boundary between classes and removing the sample from the majority class. Ensamble methods can be simple bagging, the majority vote for several weak classifier, or can be much more involved and more learning-algorithm-specific strategy. These over-sampling, under-sampling, ensembling methods have been mixed into various combinations. The above are the main stream of handling imbalanced datasets.

The cost-sensitive learning is another stream for handling imbalanced datasets. 

Yet another weay to handle imbalanced datasets is to go with more unsupervised learning, for instance, anomaly detection and autoencoder.


## Different metrics

+ Precision, Recall, F1 score, G-mean
+ Kappa (Cohen's Kappa)
+ ROC (the development for multi-class problems are reletively less mature)
+ PR curve:
  
  >Although ROC curves provide powerful methods to visualize performance evaluation, they also have their own limitations. In the case of highly skewed data sets, it is observed that the ROC curve may provide an overly optimistic view of an algorithm’s performance. Under such situations, the PR curves can provide a more informative representation of performance assessment

## Resampling

### Over-sampling

Lowers the variance of the minority class.

#### Cluster-based sampling method (cluster-based oversampling - CBO)


### Under-sampling

Increases the variance of the majority class.

#### Tomek link

From [Tomek1978].
Remove the samples of majority classes that are very close to the minority cases. Python package is [here](https://github.com/ojtwist/TomekLink)

#### Cluster majority class

Cluster large class into N clusters and use the N mediods to represent the large class. N is the sample size of the minority class.

#### Informed undersampling, or ensemble sampling (EasyEnsemble and BalanceCascade)


### Over-sampling followed by under-sampling

Under-sampling are performed by T-links or ENN (cleaning rules)

+ SMOTE + Tomek links 
+ SMOTE + ENN 


### Other sampling techniques

#### Resampling and bagging

From [Wallace2011]. Subdivide the large class into L small classes, and train L predictors against the minority class. Then average the prediction scores. Steps are as below

+ Bootstrap
+ Balance by downsampling into N different datasets
+ Train decision trees to each dataset. The decision boundaries are having high variance.
+ Bagging all trees. Make a majority vote.

#### Sampling with data cleaning techniques. 

> Some representative work in this area includes the OSS method [42], the condensed nearest neighbor rule and Tomek Links (CNN+Tomek Links) integration method [22], the neighborhood cleaning rule (NCL) [36] based on the edited nearest neighbor (ENN) rule—which removes examples that differ from two of its three nearest neighbors, and the integrations of SMOTE with ENN (SMOTE+ENN) and SMOTE with Tomek links (SMOTE + Tomek)

#### Integration of sampling and boosting (SMOTEBoost, DataBoost-IM)

#### Over / undersampling with jittering (JOUS-Boost)


## Synthetic samples

#### SMOTE

The original paper "[SMOTE: Synthetic Minority Over-sampling Technique](http://www.jair.org/papers/paper953.html)", [SMOTE](https://arxiv.org/pdf/1106.1813.pdf)
Procedures are as below:

+ For K times replication, find K-nearest neighbors for each minority sample.
+ Interpolate at halfway, or within (0,1) of their distance for each pair of the sample and its K-nearest neighbors to generate K synthetic samples
+ Note the limitation: "Formally, SMOTE can only fill in the convex hull of existing minority examples, but not create new exterior regions of minority examples."

#### Adaptive Synthetic Sampling (Borderline-SMOTE and ADA-SYN)

## Penalization, cost-sensitive learning

Penalize making mistakes for the minority classes.

+ Cost-Sensitive Dataspace Weighting with Adaptive Boosting (AdaC1, AdaC2, and AdaC3)
+ Cost-Sensitive Decision Trees 

  >In regards to decision trees, cost-sensitive fitting can take three forms: first, cost-sensitive adjustments can be applied to the decision threshold; second, cost-sensitive considera- tions can be given to the split criteria at each node; and lastly, cost-sensitive pruning schemes can be applied to the tree.

+ Cost-Sensitive Neural Networks
+ Cost-Sensitive Bayesian Classifiers
+ Cost-Sensitive SVMs


## Different algorithms

Consider decision tree models

## Different perspectives

Anomaly or Change detection.

+ [One-class classification](https://en.wikipedia.org/wiki/One-class_classification): anomaly detection, change detection, novelty detection, outlier detection. This may be the worst-case scenario.
+ Autoassociator or Autoencoder
+ The Mahalanobis-Taguchi System (MTS)

## Transform problems

+ Corrupt feature data with known distributions to add robustness of training (same sample size though)[van der Maaten-2013]. Similar to drop-out or zero-out.
+ A boosting algorithm by [Schapire](http://rob.schapire.net/papers/strengthofweak.pdf)


[Tomek1978]: https://www.scopus.com/record/display.uri?eid=2-s2.0-0016969272&origin=inward&txGid=8E86CF1FBDAADB531ACE35C3C1A4C41B.wsnAw8kcdt7IPYLO0V48gA%3a7
[Wallace2011]: http://ieeexplore.ieee.org/document/6137280/
[van der Maaten-2013]: http://jmlr.csail.mit.edu/proceedings/papers/v28/vandermaaten13.pdf


