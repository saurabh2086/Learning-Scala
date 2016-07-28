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
