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
