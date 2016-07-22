Exercise
---

*1) Write a new centigrade-to-fahrenheit conversion (using the formula (x * 9/5) + 32), saving each step of the conversion into separate values. What do you expect the type of each value will be?*
**Answer**
```javascript
scala> val centigrade = 22.5
centigrade: Double = 22.5

scala> val f1 = centigrade * 9
f1: Double = 202.5

scala> val f2 = f1 / 5
f2: Double = 40.5

scala> val fahrenheit = f2 + 32
fahrenheit: Double = 72.5
```

*2) Modify the centigrade-to-fahrenheit formula to return an integer instead of a floating-point number.*

**Answer**
You can change the return type of the answer
```javascript
scala> val fahrenHeit = ((22.5 * 9 / 5) + 32).toInt
fahrenHeit: Int = 72
```
*3) Using the input value 2.7255, generate the string "You owe $2.73 dollars". Is this doable with string interpolation?*

**Answer**
```javascript
val input = 2.723555
println(f"You owe me $$$input%.2f dollars")
```

*4) Is there a simpler way to write the following?*
```javascript
val flag: Boolean = false
val result: Boolean = (flag == false)
```
**Answer**
simpler way is to use "!" operator
```javascript
val flag: Boolean = false
val result: Boolean = !flag
```
*5) Convert the number 128 to a Char, a String, a Double, and then back to an Int. Do you expect the original amount to be retained?\
Do you need any special conversion functions for this?*

**Answer**
```javascript
scala> val num = 128
num: Int = 128

scala> val numChar = num.toChar
numChar: Char = ?

scala> val numStr = numChar.toString
numStr: String = ?

scala> val numDble = numStr(0).toDouble
numDble: Double = 128.0

scala> val numInt = numDble.toInt
numInt: Int = 128
```
Just take care of the fact that to conver string to double use the first element of the string array

*6) Using the input string "Frank,123 Main,925-555-1943,95122" and regular expression matching, retrieve the telephone number. 
Can you convert each part of the telephone number to its own integer value? 
How would you store this in a tuple?*

**Answer**
break the string into 3 parts
```javascript
scala> val input = "Frank,123 Main,925-555-1943,95122"
input: String = Frank,123 Main,925-555-1943,95122

scala> val pattern = """.*,(\d+)-(\d+)-(\d+),.*""".r
pattern: scala.util.matching.Regex = .*,(\d+)-(\d+)-(\d+),.*

scala> val pattern(p1,p2,p3) = input
p1: String = 925
p2: String = 555
p3: String = 1943
```
convert strings to numbers and put them in tuple 
```javascript
scala> val phoneNumber = (p1.toInt, p2.toInt, p3.toInt)
phoneNumber: (Int, Int, Int) = (925,555,1943)
```

