## Exercises

*1) Although `println()` is a good way to print a string, can you find a way to print a string without `println`? 
Also, what kind of numbers, strings and other data does the REPL support?*

####Answer
An alternate way is to use `print()` method which prints without the introduction of new line 
```javascript
scala> println("goes to a new line")                                            
goes to a new line                                                              

scala> print("stay at the same line")                                           
stay at the same line 
```
*2)In the Scala REPL, convert the temperature value of 22.5 Centigrade to Fahrenheit. The conversion formula is cToF(x) = (x * 9/5) + 32.*
####Answer
```javascript
scala> (22.5 * 9 / 5) + 32                                                      
res2: Double = 72.5 
```
*3) Take the result from exercise 2, half it, and convert it back to Centigrade. You can use the generated constant variable (e.g. "res0") instead of copying and pasting the value yourself.*
####Answer
We can take the res2 variable from the previous question
```javascript
scala> (res2/2 - 32) * 5/9                                                      
res4: Double = 2.361111111111111 
```
rest of the questions for you to try in your text editor
