---
layout: note
title: Scala For the Impatient
date: 2015-08-15 20:14:44 -0600
categories: Scala
---

# Chapter 1

REPL is an easy way to test out code. To enter REPL use the command :

`scala`

Highlights of this chapter:

- Defining variables with `var` and `val`

## Declarding Values and Variables

```
val answer = 8 * 5 + 2
```
- Values are constant

```
var counter = 0
counter = 1
```

- Variables can vary
- It is good practice to use `val` unless it is really necessary.
- Type is automatically inferred but can be set manually if needed I.E.:
```
val greeting: String = null
val greeting: Any = "Hello"
```

## Commonly Used Types

Common numeric types:
- Byte
- Char
- Short
- Int
- Long
- Float
- Double
- Boolean
- BigInt
- BigDecimal


- All types are Classes
- `StringOps` class contains many useful string manipulation Functions


## Arithmetic and Operator Overloading

- Same as most other languages
- No ++ or --


## Calling Function and Methods

Examples of math Functions

```
import scala.math._

sqrt(2)
pow(2, 4)
min(3, Pi)
```

- Often classes have companion objects that act like Static classes in java

```
BigInt.probablePrime(100, scala.util.Random)
```

- Some methods don't required (). A rule of thumb is that if the method doesn't
modify the object it doesn't have parentheses.

```
"Hello".distinct
```

## The `apply` method

```
"Hello"(4) // Yields 'o'
```

This is a shortcut for

```
"Hello".apply(4)
```

Can be used for other useful things like:

```
BigInt("123456789") * BigInt("55434593")
```

## Scaladoc

- Scala can be downloaded from (here)[www.scala-lang.org/api]
- Look into `RichInt`, `RichDouble`, etc to know about numeric types
- Look in to `StringOps` for string Operations
- Math functions are in the package scala.math
- Some methods have functions as parameters. Example:
```
s.count(_.isUpper)
```

# Control Structures and Functions

Highlights of this chapter:
- An if expression has a value
- A block has a value - the value of its last expression
- The Scala `for` loop is like an "enhanced" Java `for` loop
- Semicolons are (mostly) optional
- The `void` type is `Unit`
- Avoid using `return` in a function
- Beware of missing `=` in a function definition
- Exceptions work just like in Java or C++, but you use a "pattern matching"
syntax for `catch`
- Scala has no checked Exceptions


## Conditional Expressions

Example:

```
if(x > 0) 1 else -1
```

This can be put into a variable

```
val s = if(x > 0) 1 else -1
// equivalent to
if(x > 0) s = 1 else s = -1
```

The first form is better because it can be initialized as a `val`.

- The statement has the same type as its return
- If the statement has mixed type variables, the type is whatever inherits all of the
return types

Example that will have a return type of `Any`:

```
if (x > 0) "positive" else -1
```

Example of an expression that can return no value (Really a `Unit` type)

```
if(x > 0) 1 else ()
```

- `()` is a placeholder for "no useful value"

## Statement Termination

- Statements don't have to be ended with semicolons unless there are multiple
statements per line

## Block Expressions and assignments

- A {} block contains a sequence of _expressions_.
- The value of the block is the value of the last expression

Example:

```
val distance = { val dx = x - x0; val dy = y - y0; sqrt(dx * dx + dy * dy) }
```

- Assignments (`x = 1`) return a `Unit` value

## Input / Output

Output:

```
print("Answer: ")
println(42)
printf("Hello, %s! You are %d years old.\n", "Fred", 42)
```

Input:

```
val name= readLine("Your name: ")
print("Your age: ")
val age = readInt()
printf("Hello, %s! Next year, you will be %d.\n", name, age + 1)
```

## Loops

```
while (n > 0) {
  r = r * n
  r -= 1
}
```

- There is no direct analog of `for(intialize; test; update)` in scala. Alternative:

```
for (i <- 1 to n)
  r = r * i
```

OR

```
val s = "Hello"
var sum = 0
for ( i <- 0 until s.length) // Last value for i is s.length - 1
  sum += s(i)
```
This can also be written as

```
var sum = 0
for (ch <- "Hello") sum += ch
```

- Loops tend to not be used as much in scala
- There are no `break` or `continue` statements. So to break out of a loop:
  - Use a Boolean control variable instead
  - Use nested functions - you can return from the middle of a function
  - Use the break method in the Breaks object:
    ```
    import scala.util.control.Breaks.)
    breakable {
      for (...) {
        if(...) break; // Exits the breakable block
        ...
      }
    }
    ```
## Advanced `for` Loops and `for` Comprehensions

```
for (i <- 1 to 3; j <- 1 to 3) print((10 * i + j) + " ")
// Prints 11 12 13 21 22 23 31 32 33
```

Each generate can have a `guard`, a Boolean condition preceded by `if`:

```
for(i <- 1 to 3; j <- 1 to 3 if != j) print((10 * i + j) + " ")
// Prints 12 13 21 23 31 32
```

There can be any number of `definitions`

```
for ( i <- 1 to 3; from = 4 - i; j <- from to 3) print((10 * i + j) + " ")
// Prints 13 22 23 31 32 33
```

If the `for` loop starts with `yield`, then the loops constructs a collection
of values, on for each iteration:

```
for(i <- 1 to 10) yield i % 3
  // Yields Vector(1, 2, 0, 1, 2, 0, 1, 2, 0, 1)
```

This type of loop is called a `for comprehension`

## Functions

- Scala has both functions and methods
- A method operates like an object, a function doesn't

Defining a function:

```
def abs(x: Double) = if (x >= 0) x else -x
```

- The parameters must be typed
- The return type doesn't need to be specified unless the function is recursive. Example:

```
def fac(n: Int): Int = if (n <= 0) 1 else n * fac(n - 1)
```

## Default and Named Arguments

- Default arguments can be set for functions

```
def decorate(str: String, left: String = "[", right: String = "]") =
  left + str + right
```

Functions can also be called with named arguments

```
decorate(left = "<<<", str = "Hello", right = ">>>")
```

## Variable Arguments

- A function that can take a variable number of arguments

```
def sum(args: Int*) = {
  var result = 0
  for (arg <- args) result += arg
  result
}

val s = sum(1, 4, 9, 16, 25)
```

but you cannot do this

```
val s = sum(1 to 5) // error
```

but can be done like this

```
val s = sum(1 to 5: _*) // Consider 1 to 5 as an argument sequence
```

## Procedures

- Scala has a special notation for a function that returns no value
- This is to enclose the function body without a preceding = symbol
- This type of function is called a `procedure`
- A procedure returns no value

```
def box(s : String) {
  val border = "-" * s.length + "--\n"
  println(boder + "|" + s + "|\n" + border)
}
```

## Lazy values

- A lazy val defers it's initialization unti it is accessed for the first time

```
lazy val words = scala.io.Source.fromFile("/usr/share/dict/words").mkString
```

This won't open the file unless words is accessed

## Exceptions

```
throw new IllegalArgumentException("x should not be negative")
```

- The current computation will be aborted and the runtime system will look for
an exception handler than accepts an `IllegalArgumentException`.
