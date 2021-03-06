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
Applying function to a listof numbers
```javascript
scala> def factors(n: List[Int]) = {                                            
     | n.flatMap(x => (2 to x-1).filter(y => x % y == 0).toList).toList         
     | }                                                                        
factors: (n: List[Int])List[Int]                                                
                                                                                
scala> factors(List(9,11,13,15))                                                
res7: List[Int] = List(3, 3, 5)                                                 
```
Another version wen you do not pass list of numbers but more than 1 number 
```javascript
scala> def factors(n: Int*) = {                                                 
     | n.flatMap(x => (2 to x-1).filter(y => x % y == 0).toList).toList         
     | }                                                                        
factors: (n: Int*)List[Int] 

scala> factors(9,11,13,15)                                                      
res6: List[Int] = List(3, 3, 5)                                                 
```
*3) Write a function, first[A](items: List[A], count: Int): List[A], that returns the first x number of items in a given list. For example, first(List('a','t','o'), 2) should return List('a','t'). You could make this a one-liner by invoking one of the built-in list operations that already performs this task, or (preferably) implement your own solution. Can you do so with a for-loop? With foldLeft? With a recursive function that only accessed head and tail?*

**Answer**
We can use `take` from the built in function 
```javascript
scala> def first[A](items: List[A], count: Int): List[A] = items.take(count)    
first: [A](items: List[A], count: Int)List[A]                                   
```
*Using for loop*
```javascript
scala> def first[A](items: List[A], count: Int): List[A] = {                    
     | (for(i <- 0 to count -1 ) yield items(i)).toList                         
     | }                                                                        
first: [A](items: List[A], count: Int)List[A]                                   
                                                                                
scala> first(List("a","b","c"),2)                                               
res0: List[String] = List(a, b)                                                 
```
*Using foldLeft*
While uisng Fold we have to define the type of list for the leftFold function
```javascript
scala> def first[A](items: List[A], count: Int): List[A] = {                    
     | items.foldLeft[List[A]](Nil){(a: List[A], i: A) =>                       
     | if(a.size > count) a else i :: a                                         
     | }                                                                        
     | }                                                                        
first: [A](items: List[A], count: Int)List[A]                                   
                                                                                
scala> first(List("a", "b", "c", "d"),3)                                        
res1: List[String] = List(d, c, b, a)                                           
```
*A  recursive function using just head and tail function*
```javascript
def first[A](items: List[A], count: Int): List[A] = {
    if(count > 0) { 
        items.head :: first(items.tail, count-1)
    }
    else Nil
}
println(first(List(1,2,3,4,5,6),3))

List(1, 2, 3)
```
*4) Write a function that takes a list of strings and returns the longest string in the list. Can you avoid using mutable variables here? This is an excellent candidate for the list-folding operations we studied. Can you implement this with both fold and reduce ? Would your function be more useful if it took a function parameter that compared two strings and returned the preferred one? How about if this function was applicable to generic lists, ie lists of any type?*

**Answer**
Using Fold 
```javascript
scala> def longestString(str: List[String]): String = {
     | str.fold(""){ (x,y) => if(x.length > y.length) x else y}
     | }
longestString: (str: List[String])String

scala> longestString(List("ram", "shayam", "ghanshayam")
     | )
res31: String = ghanshayam
```
Using reduce
```javascript
scala> def longestString(str: List[String]): String = {
     | str.reduce{(x,y) => if(x.length > y.length) x else y}
     | }
longestString: (str: List[String])String

scala> longestString(List("robert", "lion", "peter"))
res35: String = robert
```
Applying this function for any list 
```javascript
scala> def largeOne[A](lst: List[A], large: (A,A) => A): A = {
     | lst.reduce(large)
     | }
largeOne: [A](lst: List[A], large: (A, A) => A)A

scala> largeOne[String](names, (x,y) => if(x.length > y.length) x else y)
res41: String = tamatar
```
*6) Write a function that takes a List[String] and returns a (List[String],List[String]), a tuple of string lists. The first list should be items in the original list that are palindromes (written the same forwards and backwards, like "racecar"). The second list in the tuple should be all of the remaining items from the original list. You can implement this easily with partition, but are there other operations you could use instead?*

**Answer**
```javascript
scala> def findPalindrome(lst: List[String]):(List[String], List[String]) = {
     | lst.partition(x => x == x.reverse)
     | }
findPalindrome: (lst: List[String])(List[String], List[String])

scala> val strings = List("asdfghgfdsa","peter", "kalia","rammar")
strings: List[String] = List(asdfghgfdsa, peter, kalia, rammar)

scala> findPalindrome(strings)
res42: (List[String], List[String]) = (List(asdfghgfdsa, rammar),List(peter, kalia))
```
Other that partition we can use groupby method 
```javascript
scala> def findPalindrome(lst: List[String]):(List[String], List[String]) = {
     | val groups = lst.groupBy(x => x == x.reverse)
     | (groups(true), groups(false))
     | }
findPalindrome: (lst: List[String])(List[String], List[String])

scala> findPalindrome(strings)
res43: (List[String], List[String]) = (List(asdfghgfdsa, rammar),List(peter, kalia))
```
*7) The last exercise in this chapter is a multi-part problem. We’ll be reading and processing a forecast from the excellent and free OpenWeatherMap API.

To read content from the url we’ll use the Scala library operation io.Source.fromURL(url: String), which returns an io.Source instance. Then we’ll reduce the source to a collection of individual lines using the getLines.toList operation. Here is an example of using io.Source to read content from a url, separate it into lines and return the result as a list of strings.*
`scala> val l: List[String] = io.Source.fromURL(url).getLines.toList`
*Here is the url we will use to retrieve the weather forecast, in XML format.*
`scala> val url =  "http://api.openweathermap.org/data/2.5/forecast?mode=xml&lat=55&lon=0"`
*Go ahead and read this url into a list of strings. Once you have it, print out the first line to verify you’ve captured an xml file. The result should look pretty much like this:*
```
scala> println( l(0) )
<?xml version="1.0" encoding="utf-8"?>
```
If you don’t see an xml header, make sure that your url is correct and your internet connection is up.

Let’s begin working with this List[String] containing the xml document.
