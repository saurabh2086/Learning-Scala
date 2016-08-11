*1) Create a list of the first 20 odd Long numbers. Can you create this with a for-loop, with the filter operation, and with the map operation? What’s the most efficient and expressive way to write this?*

**Answer**
*With a for loop*
javascript
scala> for( i <- 1 to 20; if i % 2 > 0) yield i                                 
res2: scala.collection.immutable.IndexedSeq[Int] = Vector(1, 3, 5, 7, 9, 11, 13,
 15, 17, 19)
'''
