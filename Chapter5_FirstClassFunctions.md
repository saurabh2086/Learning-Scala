*1) Write a function literal that takes two integers and returns the higher number. Then write a higher-order function that takes a 3-sized tuple of integers plus this function literal, and uses it to return the maximum value in the tuple.*

**Answer**
Defining max function literal 
```javascript
scala> val max = (x: Int, y: Int) => if(x > y) x else y                         
max: (Int, Int) => Int = <function2>  
```
Writing maximize function 
```javascript
scala> def maximize(t: (Int,Int,Int),f: (Int,Int) => Int) = {                   
     | f(t._1,f(t._2,t._3))                                                     
     | }                                                                        
maximize: (t: (Int, Int, Int), f: (Int, Int) => Int)Int                         
```

applying max function literal to higher order function 
```javascript
scala> maximize((34,32,65),max)                                                 
res0: Int = 65
```
