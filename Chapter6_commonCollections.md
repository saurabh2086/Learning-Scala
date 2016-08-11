*1) Create a list of the first 20 odd Long numbers. Can you create this with a for-loop, with the filter operation, and with the map operation? What’s the most efficient and expressive way to write this?*

**Answer**
*With a for loop*
```javascript
scala> for( i <- 1 to 20; if i % 2 > 0) yield i                                 
res2: scala.collection.immutable.IndexedSeq[Int] = Vector(1, 3, 5, 7, 9, 11, 13,
 15, 17, 19)
```
*with a filter operation*
```javascript
scala> (1 to 20).filter(_ % 2 > 0).toList                                       
res11: List[Int] = List(1, 3, 5, 7, 9, 11, 13, 15, 17, 19)                      
```
*with a map operation*
```javascript
scala> (0 to 9).map( _ * 2 + 1).toList                                          
res13: List[Int] = List(1, 3, 5, 7, 9, 11, 13, 15, 17, 19)                      
```
*2) Write a function titled "factors" that takes a number and returns a list of its factors, other than 1 and the number itself. For example, factors(15) should return List(3, 5).

Then write a new function that applies "factors" to a list of numbers. Try using the list of Long numbers you generated in exercise 1. For example, executing this function with the List(9, 11, 13, 15) should return List(3, 3, 5), as the factor of 9 is 3 while the factors of 15 are 3 again and 5. Is this a good place to use map and flatten? Or, would a for-loop be a better fit?*

**Answer**
```javascript
scala> def factors(n: Int) = {                                                  
     | (2 to n-1).filter(n % _ == 0).toList                                     
     | }                                                                        
factors: (n: Int)List[Int]                                                      
```
