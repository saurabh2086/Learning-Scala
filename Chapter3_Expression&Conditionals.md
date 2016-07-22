##Exercise
---

*1) Given a string name, write a match expression that will return the same string if non-empty, or else the string "n/a" if it is empty.*

**Answer**
```javascript
val name = "myname"
val ans = name.isEmpty match {
    case false => name
    case true => "n/a"
}

println(ans)
```

*2) Given a double amount, write an expression to return "greater" if it is more than zero, "same" if it equals zero, 
and "less" if it is less than zero. Can you write this with if..else blocks? How about with match expressions?*

**Answer**

using if else block
```javascript
import scala.io.StdIn.{readLine,readInt,readDouble}
println("Enter a number")                                                       
val n = readDouble()                                                            
val ans = if(n > 0) "greater" else if(n < 0) "less" else "same"                 
println(ans) 
```
Using match expression
```javascript
import scala.io.StdIn.{readLine,readInt,readDouble}
println("Enter a number")                                                       
val n = readDouble()                                                            
val ans = n match{  
    case x if x > 0 => "greater"                                                    
    case x if x < 0 => "less"                                                       
    case other => "same"                                                            
    }                                                                               
print(ans)  
```
*3) Write an expression to convert one of the input values "cyan", "magenta", "yellow" to their 6-char hexadecimal equivalents in 
string form. What can you do to handle error conditions?*

**Answer**
```javascript
scala> val color = "magenta"
color: String = magenta

scala> color match {
     |   case "cyan" => "00ffff"
     |   case "magenta" => "00ff00"
     |   case "yellow" => "ffff00"
     |   case x => {
     |     println(s"Didn't expect $x !")
     |     "333333"
     |   }
     | }
res0: String = 00ff00
```
*4) Print the numbers 1 to 100, with each line containing a group of 5 numbers. For example:*
```
1, 2, 3, 4, 5,
6, 7, 8, 9, 10
....
```

**Answer**
```javascript
for(i <- 1 to 100 by 5){
    for(j <- i to i+4){
        if(j != 100) print(f"$j, ") else print(j)
    }
    println("")
}
```
this code outputs
```
1, 2, 3, 4, 5, 
6, 7, 8, 9, 10, 
11, 12, 13, 14, 15, 
16, 17, 18, 19, 20,
....
```
*5) There is a popular coding interview question I’ll call "typesafe", in which the numbers 1 - 100 must be printed one per line. 
The catch is that multiples of 3 must replace the number with the word "type", while multiples of 5 must replace the number with 
the word "safe". Of course, multiples of 15 must print "typesafe".*

**Answer**
```javascript
for(i <- 1 to 100 by 5){
    for(j <- i to i+4){
        if(j != 100){
        print( j match {
            case s if(s % 15 == 0) => "typesafe"
            case s if(s % 5 == 0) => "safe"
            case s if(s % 3 == 0) => "type"
            case other => j
        })
        print(", ")
        }
        else print(j)
    }
    println("")
}
```
**output**
```
1, 2, type, 4, safe, 
type, 7, 8, type, safe, 
11, type, 13, 14, typesafe, 
16, 17, type, 19, safe, 
type, 22, 23, type, safe, 
26, type, 28, 29, typesafe, 
31, 32, type, 34, safe, 
....
```

*6) Can you rewrite the answer to question 5 to fit on one line? It probably won’t be easier to read, but reducing code to its 
shortest form is an art, and a good exercise to learn the language.*

**Answer**
```javascript
for(i <- 1 to 100 by 5){for(j <- i to i+4){if(j != 100){print(if(j % 15 == 0) "typesafe, " else if(j % 5 == 0) "safe, " else if(j % 3 == 0) "type, " else j + ", ")} else print(j)}; println("")}
```
