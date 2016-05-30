---
title: Set up Spark on Local Mac
tags: [spark, scala, jupyter, installation]
---

This post is a note of installing Scala, Spark, and Toree on OS X Yosemite 10.10.5 as of 2016-05-30.

## Install Spark

```
brew install apache-spark
```
This installation comes with scala of version `2.10.5`.
The spark version is `1.6.1`.


## Make Jupyter notebook work with Spark

```
pip install --pre toree
jupyter toree install --spark_home="/usr/local/Cellar/apache-spark/1.6.1/libexec/"
```
The default spark location is not identified automatically so we have to specify `spark_home` manually.
Apache Toree was originally Spark Kernel, which is one of the most popular interactive and remote connector of Spark developed by IBM Cloud.

Once this installation is completed successfully and after launching `jupyter notebook`, you should be able to find a kernel 
called "Apache Toree - Scala". More about Toree can be found on [Github](https://github.com/apache/incubator-toree) 
and the [Toree](https://toree.incubator.apache.org/) page.
