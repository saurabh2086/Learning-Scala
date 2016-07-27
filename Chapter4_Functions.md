##Exercise
---
*1) Write a function that computes the area of a circle given its radius.*

**Answer**
```javascript
def areaOfCircle(r: Double): Double = { 
  math.Pi * math.pow(r,2)
}
```

*2) Provide an alternate form of the function in #1 that takes the radius as a String. 
What happens if your function is invoked with an empty String ?*

**Answer**

Function with radious as string
```
def areaOfCircle(r: String): Double = { 
    val radious = r.toDouble 
    math.Pi * math.pow(radious,2)
}
print(areaOfCircle("1.0"))
3.141592653589793
```
When an empty string is provided a NumberFormatException is thrown
```
java.lang.NumberFormatException: empty String
	at sun.misc.FloatingDecimal.readJavaFormatString(FloatingDecimal.java:1842)
	at sun.misc.FloatingDecimal.parseDouble(FloatingDecimal.java:110)
	....
```
*3) Write a recursive function that prints the values from 5 to 50 by fives, without using for or while loops. 
Can you make it tail-recursive?*

**Answer**
```javascript
@annotation.tailrec
def printByFiveFunction(i: Int,max: Int): Unit= {
    if(i <= max){
    println(i) 
    printByFiveFunction(i + 5,max)
    }
}

printByFiveFunction(5,50)

5
10
15
20
25
30
35
40
45
50
```
*4) Write a function that takes a milliseconds value and returns a string describing the value in days, hours, minutes and seconds. 
What’s the optimal type for the input value?*

**Answer**
 ```javascript
def miliConv(t: Int) = {
    val days = t/86400000
    val hour = (t - days * 86400000) / 3600000
    val minute = (t - 86400000 * days - 3600000 * hour) / 60000
    val sec =  (t- 86400000 * days - 3600000 * hour - 60000 * minute)/ 1000
    s"Days $days, Hours: $hour Minutes: $minute, Seconds: $sec "
}

print(miliConv(100864000))
Days 1, Hours: 4 Minutes: 1, Seconds: 4
 ```
*5) Write a function that calculates the first value raised to the exponent of the second value. Try writing this first using math.pow, then with your own calculation. Did you implement it with variables? Is there a solution available that only uses immutable data? Did you choose a numeric type that is large enough for your uses?*

**Answer**
Using math.pow is a very easy implementation
```javascript
def power(x: Double, y: Double): Double = math.pow(x,y)
print(power(2,3))
8.0
```
Second implementation without using the immutable data
```javascript
@annotation.tailrec
def power(x: BigInt, y:BigInt, a: BigInt = 1): BigInt = if(y == 0) a else power(x,y-1,a * x) 
print(power(3,2))
9
```
Do i have numeric type large enough
I guess I have :P

*Q6)Write a function that calculates the difference between a pair of 2d points (x and y) and returns the result as a point. Hint: this would be a good use for tuples.*

**Answer**
I have used Integer tuples 
```javascript
def difference(p1: (Int, Int), p2:(Int,Int)): (Int, Int) = {
  (p2._1 - p1._1, p2._2 - p1._2)
}

println(difference((1,2),(2,1)))
(1,-1)
```
Q7)Write a function that takes a 2-sized tuple and returns it with the Int value (if included) in the first position. Hint: this would be a good use for type parameters and the isInstanceOf type operation.

**Answer**
```javascript
def intFirst[A,B](t: (A,B)): (Any,Any) = if(t._2.isInstanceOf[Int]) (t._2,t._1) else t
                  
println(intFirst((2,"string")))
println(intFirst(("string",2)))
println(intFirst((2.0,2)))
println(intFirst((2,2.0)))

(2,string)
(2,string)
(2,2.0)
(2,2.0)
```
*8) Write a function that takes a 3-sized tuple and returns a 6-sized tuple, with each original parameter followed by its String representation. For example, invoking the function with (true, 22.25, "yes") should return (true, "true", 22.5, "22.5", "yes", "yes"). Can you ensure that tuples of all possible types are compatible with your function? When you invoke this function, can you do so with explicit types not only in the function result but in the value that you use to store the result?*

**Answer**
```javascript
def expandTuple[A,B,C](t:(A,B,C)): (A,String,B,String,C,String) = (t._1,t._1.toString,t._2,t._2.toString,t._3,t._3.toString)

println(expandTuple('a',2,false))
println(expandTuple(true,22.25,"yes"))
```
