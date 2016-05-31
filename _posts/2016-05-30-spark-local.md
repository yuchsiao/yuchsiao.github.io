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


## Toree magics

You can use Toree magics in Jupyter notebook to configure project and jar depedencies. 
For instance, to add [`jodi-time`](http://mvnrepository.com/artifact/joda-time/joda-time/2.9.4) for better date-time support, 
```
%adddeps joda-time joda-time 2.9.4
```

Its popular [Scala wrapper](http://mvnrepository.com/artifact/com.github.nscala-time/nscala-time_2.11/2.12.0) can also be used instead:
```
%adddeps com.github.nscala-time nscala-time 2.12.0 --transitive
```

To list all magics, 
```
%lsmagic
```

Magics are case-insensitive.

There are also "cell" magics, which re-purpose the entire cell to, for instance, HTML, SQL, etc. 

The official documents are buried in the [Wiki of the original Spark Kernel project](https://github.com/ibm-et/spark-kernel/wiki/List-of-Current-Magics-for-the-Spark-Kernel).

