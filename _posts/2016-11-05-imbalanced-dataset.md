---
title: Handling of Imbalanced Dataset in ML
tags: [machine learning, imbalanced]
---

This post collects and summarizes the methods from the following posts

+ [8 Tactics to Combat Imbalanced Classes in Your Machine Learning Dataset](http://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/) by Jason Brownlee
+ [In classification, how do you handle an unbalanced training set?](https://www.quora.com/In-classification-how-do-you-handle-an-unbalanced-training-set) from Quora
+ [Classification when 80% of my training set is of one class](https://www.reddit.com/r/MachineLearning/comments/12evgi/classification_when_80_of_my_training_set_is_of/) from Reddit
+ [scikit-learn-contrib/imbalanced-learn](https://github.com/scikit-learn-contrib/imbalanced-learn)
+ [Learning Imbalanced Classes](http://svds.com/learning-imbalanced-classes/) from SVDS blog

## Different metrics

+ Precision, Recall, and F1 score
+ Kappa (Cohen's Kappa)
+ ROC (the development for multi-class problems are reletively less mature)

## Resampling

### Upsampling

Lowers the variance of the minority class.

#### Cluster-based sampling method (cluster-based oversampling - CBO)

### Downsampling

Increases the variance of the majority class.

#### Tomek link

From [Tomek1978].
Remove the samples of majority classes that are very close to the minority cases. Python package is [here](https://github.com/ojtwist/TomekLink)

#### Informed undersampling (EasyEnsemble and BalanceCascade)

### Other sampling techniques

#### Resampling and bagging

From [Wallace2011]. Steps are as below

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
+ Interpolate at halfway for each pair of the sample and its K-nearest neighbors to generate K synthetic samples
+ Note the limitation: "Formally, SMOTE can only fill in the convex hull of existing minority examples, but not create new exterior regions of minority examples."

#### Adaptive Synthetic Sampling (Borderline-SMOTE and ADA-SYN)

## Penalization, cost-sensitive learning

Penalize making mistakes for the minority classes.

## Different algorithms

Consider decision tree models

## Different perspectives

Anomaly or Change detection

## Transform problems

+ [One-class classification](https://en.wikipedia.org/wiki/One-class_classification): anomaly detection, change detection, novelty detection, outlier detection. This may be the worst-case scenario.
+ Subdivide the large class into L small classes, and train L predictors against the minority class. Then average the prediction scores. e.g. [Wallace2011].
+ Cluster large class into N clusters and use the N mediods to represent the large class. N is the sample size of the minority class.
+ Corrupt feature data with known distributions to add robustness of training (same sample size though)[van der Maaten-2013]. Similar to drop-out or zero-out.
+ A boosting algorithm by [Schapire](http://rob.schapire.net/papers/strengthofweak.pdf)


[Tomek1978]: https://www.scopus.com/record/display.uri?eid=2-s2.0-0016969272&origin=inward&txGid=8E86CF1FBDAADB531ACE35C3C1A4C41B.wsnAw8kcdt7IPYLO0V48gA%3a7
[Wallace2011]: http://ieeexplore.ieee.org/document/6137280/
[van der Maaten-2013]: http://jmlr.csail.mit.edu/proceedings/papers/v28/vandermaaten13.pdf


