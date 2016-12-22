1) We're working on a gaming site, and need to track popular consoles like the Xbox Two and Playstation Five (I'm planning for the future here). 

a) Create a console class that can track the make, model, debut date, wifi type, physical media formats supported, and maximum video resolution. Override the default `toString` method to print a reasonably-sized description of the instance (< 120 chars).

* The debut date (or launch date) should be an instance of `java.util.Date`
* Keep the wifi type (b/g, b/g/n, etc) field optional, in case some consoles don't have wifi.
* The physical media formats should be a list. Is a `String` the best bet here, or an `Int` that matches a constant value?
* The maximum video resolution should be in a format that would make it possible to sort consoles in order of greatest number of pixels.

b) Test our your new console class by writing a new class that creates 4 instances of this console class. All of the instances should have reasonably accurate values.

c) Now its time for games. Create a game class that includes the name, maker, and a list of consoles it supports, plus an "isSupported" method that returns true if a given console is supported. 

d) Test out this game class by generating a list of games, each containing one or more instances of consoles. Can you convert this list to a lookup table of consoles to a list of supported games? How about a function that prints a list of the games, sorted first by maker and then by game name?

*Answer*
following is my strategy
1. The make and model can be a `String`
2. The debutDate is of type java.util.Date
3. Wifi field is optional so we are using Option[String]
4. physicalMedia can be written as list of strings
5. maxVideoRes is definitely Int

So lets prepare our class 

```javascript

scala> :paste -raw
// Entering paste mode (ctrl-D to finish)

class Console(val make: String, val model: String, val debutDate: java.util.Date, val wifi: Option[String], val physicalMedia: List[String], val maxVideoRes: Int) {
  override def toString = s"Console is model: $model, and make: $make, it has support to physical media: $physicalMedia and has resolution $maxVideoRes"
}

// Exiting paste mode, now interpreting.

defined class Console
 ```
