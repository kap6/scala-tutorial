# Stage 4: Functions

Functional programming languages like Scala are designed to support the creation and usage of highly composable _functions_ and to help developers organize their codebase around them.

https://www.youtube.com/watch?v=3oQTSP4FngY

(That talk's related to Clojure, another functional programming language on the JVM, and it's _really_ fantastic--assuming you ignore the stuff about macros, which aren't quite as relevant to Scala.)

## Functions

In Scala, _functions_ are named, reusable expressions. Generally, when we can, we strive for functional purity. A _pure_ function

* Has one or more input parameters,
* Performs calculations using only the input parameters,
* Returns a value,
* Always returns the same value for the same input,
* Doesn't use or affect any data outside the function, and
* Is not affected by any data outside the function.

Given the kinds of projects we work on--Pulsar, for example, is effectively a wrapper around a database--it often isn't feasible to write pure functions all across the codebase. So, instead, we try to keep the code fairly modular, isolating the portions where I/O is necessary and keeping whatever's left "pure."

Anyway, functions are defined using the `def` keyword, then called by name. Here's how to define and invoke a function with no inputs:

```
scala> def howdy = "howdy"
howdy: String

scala> howdy
res13: String = howdy
```

Though, you should really define input-less functions using parens:

```
scala> def aloha(): String = "aloha"
aloha: ()String

scala> aloha
res14: String = aloha

scala> howdy()
<console>:9: error: not enough arguments for method apply: (index: Int)Char in class StringOps.
Unspecified value parameter index.
              howdy()
                   ^
```

And, naturally, you can define a function with inputs, as well:

```
scala> def max(x: Int, y: Int): Int = if (x > y) x else y
max: (x: Int, y: Int)Int

scala> max(1, 100)
res15: Int = 100
```

Note that the bodies of functions consist essentially of expressions or expression blocks, where the final line becomes the return value of the expression and thus the function.

There _are_ ways to get around this using an explicit `return` statement, but you shouldn't do that! ;)

## Procedures

A _procedure_ is a function that doesn't have a return value. Any function that ends with a statement, such as a `println`, is also a procedure. Fore example:

```
scala> def log(s: String): Unit = println(s)
log: (s: String)Unit

scala> log("RUNNING THIS HERE FUNCTION")
RUNNING THIS HERE FUNCTION
```

You may also see an alternate syntax for procedures, which is to define them without the `Unit` type annotation _and_ without an equals sign before the procedure body, like so:

```
scala> def log(s: String) { println(s) }
log: (s: String)Unit
```

However, this is frowned upon. With this syntax, the compiler discards the final return value or final expression, which can result in all kinds of programmer error. So, don't add ^^ to the codebase any longer! ;)

## Methods

So far, we've been discussing functions without reference to where they will actually be used. Functions in the REPL are helpful for learning the basics of Scala, but in practice, functions will usually exist in objects--acting on data from the object. So, a more accurate term for them is usually "methods".

The most popular way of invoking a method is _infix dot notation_:

```
scala> val s = "someFile.pdf"
s: String = someFile.pdf

scala> val isPDF = s.endsWith(".pdf")
isPDF: Boolean = true
```

Here, the value `s` is of type `String`, and the `String` class has a method called [`endsWith()`](http://www.scala-lang.org/api/2.11.5/index.html#scala.collection.immutable.StringOps@endsWith[B](that:scala.collection.GenSeq[B]):Boolean).

If you're using an IDE, you should have a list of methods available on each object pop up as your typing. Alternatively, if you're like me, you can [read the docs](http://www.scala-lang.org/api/2.11.5/index.html)...! ;D

### Operator Notation

There's also a second way to invoke methods, _infix operator notation_, so-called because the operator (the object's method) is located between the two operands:

```
scala> val d = 15.23
d: Double = 15.23

scala> d.+(3.41)
res19: Double = 18.64

scala> d + 3.41
res20: Double = 18.64
```

Note that operator notation is meant for use on methods with only parameter, though you can wrap multiple parameters in parens if you _really_ want to use it. (Probably don't, though.)

# Exercises

1. Write a function that computes the area of a circle given its radius. 