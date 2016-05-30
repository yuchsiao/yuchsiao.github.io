---
title: Scala Collections Compared with Python, C++
tags: [scala, data structure]
---

Scala's collection data types are imporessively rich and complex. 
Picking the best suitable one may not be straightforward and some of the distinctions can be subtle in actual use cases. 
This post aims to summarize the commonly used types, compared with their counterparts in Python and in C++. 
This comparison is more for helping position the mindset and making analogies than being precise, 
espeicially from the data structure perspective.

Changes and additions to this post may be made over time.


## Abstract class and trait hierarchy

![scala collection hierarchy](http://docs.scala-lang.org/resources/images/collections.png)

See more [here](http://docs.scala-lang.org/overviews/collections/overview.html)


## Summary

|Scala     |       |Java|Python|C++|Description|
|----------|-------|----|------|---|-----------|
|*abstract*|*class*|    |      |   |           |
|`Seq.IndexedSeq`|`Array`|`Array`| |`[]`|Fixed length seq. Mutable in elements but not in length|
|`Seq.IndexedSeq`|`Vector`| | | |Fixed length seq. Immutable both in elements and length. Internally as a 32-branch tree. Default for `immutable.IndexedSeq`|
|`Seq.IndexedSeq`|`ArrayBuffer`| | `list` | `std::vector` | Variable length seq. Mutable both in elements and length. Efficient to append.|
|`Seq.LinearSeq`|`ListBuffer`| |`collections.deque`|`std::list`| Internal list. Efficient prepend and append on both ends.|
|`Map`|`Map`| | | | Mutable and immutable map implemented as [hash trie]|
|`Map`|`HashMap`| | dict | | Both mutable and immutable |
|`Map`|`TreeMap`| | |`const std::map`| Immutable RB tree map |
|     |         |`TreeMap`| |`std::map`| Mutable RB tree map |


[hash trie]: http://www.scala-lang.org/docu/files/collections-api/collections_19.html

The underlying implementation is best described here for [mutable collection](http://docs.scala-lang.org/overviews/collections/concrete-mutable-collection-classes.html) and for [immutable collection](http://docs.scala-lang.org/overviews/collections/concrete-immutable-collection-classes).


## Handy literals

+ indexed seq
  + immutable: `Vector(1, 2, 3)`
  + mutable: `collection.mutable.ArrayBuffer(1, 2, 3)`
+ linear seq
  + immutable: `List(1, 2, 3)`
  + mutable: `collection.mutable.ListBuffer(1, 2, 3)`
+ map
  + immutable: `Map(1->"a", 2->"b")`
  + mutable: `collection.mutable.Map(1->"a", 2->"b")`
+ set
  + immutable: `Set(1, 2, 3)`
  + mutable: `collection.mutable.Set(1, 2, 3)`

## Caveats and tricks

### Mutable vs immutable

Immtable collection is optimized based on the agreement that both the size and the content cannot be changed, whereas mutable collection allows changes in both the size and the content. `Array` is something in between: you can change the content but not the size. Therefore, in some sense `Array` is mutable, but due to the underlying data structure, changes in size are natually not allowed. People are arguing on [this point](http://docs.scala-lang.org/overviews/collections/overview.html). The definition of *mutability* in the [official document](http://docs.scala-lang.org/overviews/collections/overview.html) is that "A mutable collection can be updated or extended in place." So logically, if any change can be made after the object being created, it is mutable. But, really, it doesn't matter much.

### `val` vs `var`
 `var` for an immutable collection allows operations such as `+=`. But what's under the hood is that a new immutable collection is being created and attached to the same reference. The old one is then recycled. In this case, you still cannot modify values.
```scala
var x = Map("AL" -> "Alabama")  // still default immutable.Map
x += ("CA"->"California")  // okay because a new map is being generated
x("CA") = "Air China"  // illegal because of an attempt of modifying values
```

### Initialize through other collection objects
```scala
val m = Map(1->"a")
val tm = collection.immutable.TreeMap(m.toArray:_*)
```

## Performance characteristics

The best way to choose a proper collection type is to look at the complexity of operations being used in your applications.
This perhaps is also the easist way to figure out the underlying implementation and data structure.
 
The [official document](http://docs.scala-lang.org/overviews/collections/performance-characteristics.html) provides an excellent summary
of the performance characteristics for each Scala collection class.



