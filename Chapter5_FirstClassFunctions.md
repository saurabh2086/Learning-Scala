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
*2) The library function util.Random.nextInt returns a random integer. Use it to invoke the "max" function with two random integers plus a function that returns the larger of two given integers. Do the same with a function that returns the smaller of two given integers, and then a function that returns the second integer every time.*

**Answer**
Creating a rand function to generate random number 
```javascript
scala> def rand() = util.Random.nextInt                                         
rand: ()Int
```
Creating a general function on which we can apply max min and pick seond function
```javascript
scala> def utilFunction(t: (Int,Int), f:(Int,Int)=>Int) = f(t._1,t._2)          
utilFunction: (t: (Int, Int), f: (Int, Int) => Int)Int                          
```
get a tuple 
```javascript
scala> val t = (rand,rand)                                                      
t: (Int, Int) = (-611942706,-233909952)
```
applying max function thtat is defined in the previous example
```javascript
scala> utilFunction(t,max)                                                      
res4: Int = -233909952                                                          
```
Lets pass other functions as function literals
Applying min
```javascript
scala> utilFunction(t,(a: Int,b: Int) => if (a < b) a else b)                   
res5: Int = -611942706                                                          
```
applying the pick second function
```javascript
scala> utilFunction(t,(a: Int,b: Int) => b)                                     
res7: Int = -233909952                                                          
```
*3) Write a higher-order function that takes an integer and returns a function. The returned function should take a single integer argument (say, "x") and return the product of x and the integer passed to the higher-order function.*

**Answer**\
I am applying *currying* here
```javascript
scala> def productOf(x:Int)(y:Int) = x * y                                      
productOf: (x: Int)(y: Int)Int                                                  
```
Lets test this
```javascript
scala> val doubler = productOf(2)_                                              
doubler: Int => Int = <function1>                                               

```
*4) Let’s say that you happened to run across this function while reviewing another developer’s code:
```
def fzero[A](x: A)(f: A ⇒ Unit): A = { f(x); x }
```
What does this function accomplish? Can you give an example of how you might invoke it?*

**Answer**
As we can see this is an example of a higher order function. It applies currying in whic we a re passing a functino literal with Unit return type. Unit return type generally tells us that there is nothing interesting is beign returned.
Example
```javascript
scala> def fzero[A](x:A)(f: A => Unit):A = {f(x); x}                            
fzero: [A](x: A)(f: A => Unit)A                                                 

scala> val reversePrint = fzero("Saurabh")_                                     
reversePrint: (String => Unit) => String = <function1>                          

scala> reversePrint(x => println(x.reverse))                                    
hbaruaS                                                                         
res1: String = Saurabh                                                          

```
*5) There’s a function named "square" that you would like to store in a function value. Is this the right way to do it? How else can you store a function in a value?*
```
def square(m: Double) = m * m
val sq = square
```
**Answer**
This is not the way to assign function value 
if you try this you would get following error
```javascript
scala> val sq = square                                                          
<console>:11: error: missing arguments for method square;                       
follow this method with `_' if you want to treat it as a partially applied funct
ion                                                                             
       val sq = square                                                          
                ^                                                               
```

There are many ways to assign function value
Following are few 

Function Literal
```javascript
scala> val sq = (m: Double) => m * m                                            
sq: Double => Double = <function1>                                              
```
```javascript
scala> val sq: (Double) => Double = square                                      
sq: Double => Double = <function1>                                              
```
Using wildcard operator
```javascript
scala> val sq = square _                                                        
sq: Double => Double = <function1>
```
*6) Write a function called "conditional" that takes a value x and two functions, p and f, and returns a value of the same type as x. The p function is a predicate, taking the value x and returning a Boolean b. The f function also takes the value x and returns a new value of the same type. Your "conditional" function should only invoke the function f(x) if p(x) is true, and otherwise return x. How many type parameters will the "conditional" function require?*

**Answer**
```javascript
scala> def conditional[A](x: A, p: A => Boolean, f: A => A) = {                 
     | if(p(x)) f(x) else x                                                     
     | }                                                                        
conditional: [A](x: A, p: A => Boolean, f: A => A)A   

scala> conditional(5,(x:Int) =>  x > 5, (y:Int) => y * 3)                       
res11: Int = 5                                                                  
                                                                                
scala> conditional(6,(x:Int) =>  x > 5, (y:Int) => y * 3)                       
res12: Int = 18                                                                 
```
