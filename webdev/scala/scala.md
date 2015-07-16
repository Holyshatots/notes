# Scala

## Resources

[Scala Style Guide](http://docs.scala-lang.org/style/types.html)

[Coursera Scala Course](https://www.coursera.org/course/progfun)




# [RefCardz Scala](https://dzone.com/refcardz/scala)

## Variables

- Immutable variable : A variable that cannot be modified after it has been created.
    - Thread Safe
    - Easier to reason - the value doesn't change

Example :
```
val first:String = "Hello"
println(string)
```

- Mutable variable : A variable that can be modified after it has been created
    - Not thread safe

Example :

```
var first:String = "Hello"
println(string)
first = "Goodbye"
```

BEST PRACTICE : Start with immutable and make it mutable if needed

### Type Inference
- Scala will automatically detect the Type if not defined
- Type cannot be changed

```
var first = "Hello"
```

### Expression Oriented

- Doesn't require an explicit return statement. The last line will be the value returned.

Examples :

```
val second = {
    val tmp = 2*5
    tmp+88
}
```
98 will be assigned to second.

```
val second = 43
val displayFlag = if (second%2 == 0) {
    "Second is even"
}
else {
    "Second is Odd"
}
```

OR in shorthand notation

```
val displayFlag = if (second%2 == 0)
                    "Second is even"
                  else
                    "Second is odd"
```

## Classes and Objects

- Pure object-oriented language
- Everything is an object
- Every operation is a method call

Example :

NOTE: Added 's' in println is in official example. Not sure if it is supposed to be there.

```
class Recipe(calories: Int) {
    println(s"Created recipe with ${calories} calories")
    var cookTime: Int = _ //sets 0, default value of Int
}
```

### Constructors

- Constructors are different from java. The constructor parameters are in the class definition.
- Statements in the body of the class are considered the primary constructor
- Secondary constructors can be created if needed
- By default, constructor parameters are not visible
- Fields are visible outside of the class

Example :

```
val r = new Recipe(100)
println(r.cookTime)     //prints 0
println(r.cookTime = 2) //sets cookTime to 2
// This will produce an error
println(r.calories)
```

- To promote the constructor parameters to fields, add a val or var

Example :

```
class Recipe(val calories: Int) {
```

### Methods

- Begins with `def`
- Return type can be inferred

```
// declares method that returns an Int (Int return is optional)
def estimatedEffort(servings:Int):Int = {
    println("estimating the effor...")
    servings * cookTime * calories
}
```

### Inheritance

- Constructor parameters of the class extended need to be passed in as well

Example:
```
class Food(calories: Int)
class Salad(val lettuceCalories: Int, val dressingCalories: Int) extends Food(lettuceCalories + dressingCalories)
```

```
// Example of overriding Methods
class Menu(items: List[Food]) {
    def numberOfMenuItems() = items.size
}

// Dinners only consists of Salads
class Dinner(items: List[Salad]) extends Menu(items) {
    // overriding def as val
    override def numberOfMenuItems = 2 * items.size
}

val s1 = new Salad(5,5)
val s2 = new Salad(15,15)
val dinner = new Dinner(List(s1,s2))
// prints 4
println(s"Number Of Menu Items = ${dinner.numberOfMenuItems}")
```

- ``object`` keyword is used to define a class as a singleton
    - Singleton: Members inside of the object are static and can be used without creating an explicit instance.

### Factory objects and apply

- The apply method is like a default factory method that allows the object to be called like a method

Example:

In Recipe.scala above the class declaration
```
object Recipe {
    def apply(calories:Int) = new Recipe(calories * 2)
}
```
Then in Hello main
```
// This call refers to the Recipe object and is the same as calling Recipe.apply(100)
val r = Recipe(100) // apply method is called by default
println(r.calories) // outputs 200
```

- An object is a companion object when it is declared
    - In the same file as the class
    - Shares the name
    - Shares the package
- Companion object are used to hold static definitions related to the class
    - Don't have a special relationship with the class


## Case Classes

- A case class will automatically generate helpful boilerplate code

```
case class Person(name: String, age: Int)
```

Effects of adding case

- Constructor parameters are made immutable (val) fields by default.
- Equals, hashCode, and toString are generated based on the constructor parameters
- A copy method is generated so we can easily create a modified copy of a class instance
- A default implementation is provided for serialization
- A companion object and the default apply factor method is cretead.
- Pattern matching on the class is made possible.

What the Person will be compiled into
```
class Person(val name: String, age: Int) { ... }

// The companion object for person
object Person {
    def apply(name: String, age: Int) = new Person(name, age)
    ...
}
```

So Person can be created using no new keyword

```
val p = Person("John", 26)
```

## Traits

- An interface that provides a default implementation of some of the methods
- Traits may not have constructor parameters
- Not instantiated directly like a class

```
// declaring a trait with an abstract method
trait Greetings {
    def sayHello: String
}

class JapaneseGreetings extends Greetings {
    override def sayHello: String = "konnichiwa"
}
```

- Traits can be used to provide methods and variables that are mixed into a class instead of being extended.

```
trait DefaultGreetings {
    def defaultHello = "Hello"
}

class GermanGreetings extends Greetings with DefaultGreetings {
    override def sayHello: String = "Guten Tag"
}

val g = new GermanGreetings
g.sayHello      // outputs Guten Tag
g.defaultHello  // outputs Hello
```

- Traits can also be mixed-in at the instnace level

```
val j = new JapaneseGreetings with DefaultGreetings
j.sayHello      // outputs konnichiwa
j.defaultHello  // outputs Hello
```

## Functions

- Similar to method
- Attached to a class
- Functions are assigned to variables
- Functions have types
- Methods are not values
- Functions can be passed around like other variables

Example:

```
// creates a function that takes an Int as a parameter and returns Int.
// The variable type in scala is formally declared as Int => Int
val succ = (foo: Int) => {foo + 1}

succ(10) //outputs 11
```

- Foo is the name of the parameter
- What comes after "=>" is the body of the function
- Can be passed as a parameter

Example of passing as a parameter:

```
def succAndLog(someInt: Int, succ: Int => Int) = {
    println(s"Incrementing $someInt")
    succ(someInt)
}

succAndLog(10, (i: Int) => i + 1) // Incrementing 10 and returns 11

## Collections

- Collections are the data structures of scala
- They can be immutable, mutable, and parallel
- Immutable APIs are imported by default

Common tasks using collections

### Transform all the elements of the collection

```
val sx = Vector(10, 20, 30, 40)
//map executes the given anonymous function for each element in the collection

val newList = xs.map(x => x/2)

println(newList) //outputs new sequence Vector(5, 10, 15, 20)
println(xs) //outputs the original collection because its immutable
```

### Filtering

```
val xs = Vector(1, 2, 3, 4, 5).filter(x => x < 3)
println(xs) //outputs new collection Vector(1, 2)
```

### Grouping elements of collections based on the return value

```
val groupByOddAndEven = Vector(1,2,3,4,5).groupBy(x => x % 2 == 0)
println(groupByOddAndEven) //outputs Map(false -> Vector(1, 3, 5), true -> Vector(2, 4))
```

### Sorting

```
val lowestToHighest = Vector(3,1,2).sorted
println(lowestToHighest) //outputs Vector(1, 2, 3)
```

Example of mutable counterpart

```
val numbers = scala.collection.mutable.ListBuffer(10, 20, 30)
numbers(0) = 40     // updates the zeroth element to 40
println(numbers)    // outputs ListBuffer(40, 20, 30)
```

Example of using a parallel collection

```
val numbers = scala.collection.parallel.ParSeq(1, 2, 3, 4, 5, 6, 7)

val newNumbers = numbers.map {x =>
    // prints the name of the current thread
    println(s"Current thread ${Thread.currentThread.getName}")
    x + 1
}
```
