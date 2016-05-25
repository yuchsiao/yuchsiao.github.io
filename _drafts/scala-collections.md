---
title: Scala Collections Compared with Python, C++
tags: [scala, data structure]
---

Scala's collection data types are imporessively rich and complex. Picking the best suitable one may not be straightforward and some of the distinctions are subtle in actual use cases. This post aims to summarize the commonly used types, compared with their counterparts in Python and in C++. This comparison is more for helping position the mindset and making analogies than being precise, espeicially from the data structure perspective.

## Summary

|Scala     |       |Java|Python|C++|Description|
|----------|-------|----|------|---|-----------|
|*abstract*|*class*|    |      |   |           |
|`Seq.IndexedSeq`|`Array`|`Array`| |`[]`|Fixed length seq. Mutable in elements but not in length|
|`Seq.IndexedSeq`|`Vector`| | | `const std::vector`|Fixed length seq. Immutable both in elements and length|
|`Seq.IndexedSeq`|`ArrayBuffer`| | list | `std::vector` | Variable length seq. Mutable both in elements and length|
|`Map`|`Map`| | | | Mutable and immutable map implemented as [hash trie]|
|`Map`|`HashMap`| | dict | | Both mutable and immutable |
|`Map`|`TreeMap`| | |`const std::map`| Immutable RB tree map |
|     |         |`TreeMap`| |`std::map`| Mutable RB tree map |


[hash trie]: http://www.scala-lang.org/docu/files/collections-api/collections_19.html


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

### `val` vs `var`
 `var` allows operations such as `+=`. But what's under the hood is that a new collection is being created and attached to the same reference. You still can't modify values.
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

+ [docs.scala-lang](http://docs.scala-lang.org/overviews/collections/performance-characteristics.html)



