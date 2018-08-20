# Stage 3: Expressions and Conditionals

## Expressions

An _expression_ is a single unit of code that returns a value.

One example of an expression is a literal on its own:

```
scala> "Hello World"
res0: String = Hello World
```

Another example of an expression is

```
scala> "Hello" + " " + "World"
res1: String = Hello World
```

This example and the previous example are both valid expressions that, while implemented differently, generate the same result. Accordingly, the important thing to take away from expressions is that the entire point is to return a value that gets captured and used.

### Defining Values and Variables with Expressions

In the last stage, we saw that values and variables could be assigned literal values. However, more accurately, values and variables can be assigned expressions, of which literal values are a subset:

```
val <identifier>[: <type>] = <expression>
var <identifier>[: <type>] = <expression>
```

### Expression Blocks

Multiple expressions can be combined using curly braces to create a single _expression block_. Expressions have their own scopes, so they can contain values and variables local to the expression block. The last expression in the block serves as the return value for the entire block. For example,

```
scala> val tablePrice = 12.50 * 5; val finalAmount = tablePrice * 1.25
tablePrice: Double = 62.5
finalAmount: Double = 78.125
```

can be rewritten as

```
scala> val amount = { val tablePrice = 12.50 * 5; tablePrice * 1.25 }
amount: Double = 78.125
```

while leaving tablePrice inaccessible outside the expression block:

```
scala> tablePrice
<console>:8: error: not found: value tablePrice
              tablePrice
```

Note that expression blocks can span as many lines as you need, so you can remove the semicolon:

```
scala> val amount = {
     |     val tablePrice = 12.50 * 5
     |     tablePrice * 1.25 
     | }
amount: Double = 78.125
```

Expression blocks are nestable, as well.

### Statements

A _statement_ is an expression that doesn't return a value. 

Typically, we try to avoid these whenever possible; one goal of functional programming is to minimize the number of "moving parts", and this includes side effects. As a result, you'll probably only see statements when they're absolutely unavoidable--when doing I/O, for example, to access a database or perform logging.

In Scala, statements have a return type of `Unit`, though we'll have to discuss that later.

## If-Else Expression Blocks

Like most languages, Scala has if-else expressions!

As an example, here's an if block that prints `"Yes!"` if `47` is odd:

```
scala> if (47 % 2 == 1) println("Yes!")
Yes!
```

We can also add an else case. Here's an if-else block that prints `"Yes!"` if `42` is odd and `"No!"` if `42` is even:

```
scala> if (42 % 2 == 1) println("Yes!") else println("No!")
No!
```

And, finally, if-else blocks are expressions, not statements, so we can determine the maximum of two values in one line, for example:

```
scala> val x = 1; val y = 100
x: Int = 1
y: Int = 100

scala> val max = if (x > y) x else y
max: Int = 100
```

Note that, in Scala, this is about as complicated as if-else expressions get! Otherwise, we use match expressions.

## Match Expressions

Scala's match expressions are a bit like "switch" statements in other languages, except more widely applicable. A single input item is evaluated, and the first pattern in the list that "matches" is executed, with its value return. Like "switch" statements, you can also use a wildcard pattern as a catch-all. Unlike "switch" statements, however, only zero or one pattern can match, and if your case statements are not full exhaustive (i.e. you don't cover all corner cases), the Scala compiler will provide a warning.

As an example, here's how we would rewrite `max` using a match statement:

```
scala> val x = 1; val y = 100
x: Int = 1
y: Int = 100

scala> val max = x > y match {
     |   case true => x
     |   case false => y
     | }
max: Int = 100
```

You can also use _pattern alternatives_ to use the same `case` block for multiple patterns:

```
scala> val day = "MON"
day: String = MON

scala> val kind = day match {
     |   case "MON" | "TUE" | "WED" | "THU" | "FRI" =>
     |     "weekday"
     |   case "SAT" | "SUN" =>
     |     "weekend"
     | }
kind: String = weekday
```

Or, you can use an underscore as a wildcard to catch all the cases you'd rather not list out:

```
scala> val num = 5
num: Int = 5

scala> val isFifty = num match {
     |   case 50 => true
     |   case _ => false
     | }
isFifty: Boolean = false
```

### Loops

Loops are the last main expression-based control structure you'll probably see in the codebase. The most important looping structure in Scala is the for-comprehension:

http://nerd.kelseyinnis.com/blog/2013/11/12/idiomatic-scala-the-for-comprehension/

tl;dr For-comprehensions can be just like for loops:

```
scala> for (x <- 1 to 10) { println(x) }
1
2
3
4
5
6
7
8
9
10
```

but you can also use them to condense what would otherwise be really gross nested for loops into something more readable:

```
scala> for {
     |   x <- 1 to 3
     |   y <- 4 to 6
     | } { println(s"($x, $y)") }
(1, 4)
(1, 5)
(1, 6)
(2, 4)
(2, 5)
(2, 6)
(3, 4)
(3, 5)
(3, 6)
```

though, really, this just turns into the equivalent of nested for loops behind the scenes.

You can also use the `yield` keyword to return a collection of values, vs. creating side effects:

```
scala> for {
     |   x <- 1 to 3
     |   y <- 4 to 6
     | } yield { (x, y) }
res11: scala.collection.immutable.IndexedSeq[(Int, Int)] = Vector((1,4), (1,5), (1,6), (2,4), (2,5), (2,6), (3,4), (3,5), (3,6))
```

or even use _iterator guards_ (a.k.a. _filters_) to add if expressions to an iterator:

```
scala> for {
     |   x <- 1 to 10
     |   if x % 2 == 0
     | } yield x
res12: scala.collection.immutable.IndexedSeq[Int] = Vector(2, 4, 6, 8, 10)
```

# Exercise

1. Given a double `amount` write an expression to return "greater" if it is more than zero, "same" if it equals zero, and "less" if it is less than zero. Can you write this with if..else blocks? How about with match expressions?

# Spoilers!

```
scala > if (amount > 0) "greater" else if (amount == 0) "same" else "less"
```

or 
```
scala> amount match {
     |   case _ if amount > 0 => "greater"
     |   case _ if amount == 0 => "same"
     |   case _ => "less"
     | }
```