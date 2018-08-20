# Stage 2: Using the REPL

Fortunately, Scala has a [read-eval-print loop (REPL)](http://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop), which allows us to try out code without creating a formal project. 

## Starting the REPL

If you've used Python's `python` or Ruby's `irb`, then success! You're in luck, as Scala's REPL is pretty similar.

You can start a new REPL session by executing the `scala` command in your terminal:

```
$ scala
Welcome to Scala version 2.11.4 (Java HotSpot(TM) 64-Bit Server VM, Java 1.7.0_67).
Type in expressions to have them evaluated.
Type :help for more information.

scala>
```

Afterwards, you should see a "Welcome to Scala" message, followed by the version of Scala you're running and the version of Java you're using; above, it says that I'm using Scala 2.11.4 and the Java 7 JDK.

## Working with Data in Scala

In Scala, there are several different ways to represent data:

* Literals, which appear directly in the source code;
* Variables, which are mutable, typed storaged units; and
* Values, which which are immutable, typed storage units;
* Types, which are definitions of the kinds of data you're working with.

### Literals

The basic Scala literals include:

* Integers,
* Floats,
* Booleans,
* Characters,
* Strings, and
* Null

As an example, let's type an integer literal into the Scala REPL:

```
scala> 42
res0: Int = 42
```

Here, we've entered `42`, and the REPL has created a new _value_ of type _Int_ that equals `42`.

If we'd like to refer to that value later in the REPL session, we can do so using the value name:

```
scala> res0
res1: Int = 42
```

To continue we'd like an integer literal of type `Long`, we can add an `L` to the end of our literal:

```
scala> 42L
res2: Long = 42
```

Floating-point literals are created when the data contains all numbers and one period, or when followed by either `F` or `f`, and are of type `Double`:

```
scala> 15.0
res3: Double = 15.0
```

Booleans can be either `true` or `false` and are of type `Boolean`:

```
scala> true
res4: Boolean = true

scala> false
res5: Boolean = false
```

Characters are single characters enclosed in single quotes:

```
scala> 'a'
res6: Char = a
```

You can see a list of escape sequences [here](???).

Strings are sequences of characters enclosed in double quotes:

```
scala> "Howdy"
res7: String = Howdy
```

They are also multi-line sequences of characters enclosed in three double quotes:

```
scala> """This string spans four lines
     | because I like to live dangerously
     | and who can fault me for that
     | I am super-cool"""
res9: String =
This string spans four lines
because I like to live dangerously
and who can fault me for that
I am super-cool
```

And, finally, there's Null:

```
scala> null
res10: Null = null
```

Note that, although `Null` exists in Scala, most people don't use it; we'll talk about why later.

### Variables

As in other contexts, in Scala, the word "variable" refers to an identifier corresponding to an allocated or reserved memory space, into which values can be stored and from which values can be retrieved. As long as the memory space is reserved, it can be assigned new values over and over again. Thus, the contents of the memory space are dynamic, or "variable."

In Scala, we can define these variables using the format

```
var <identifier>[: <type>] = <data>
```

where `<identifier>` is a name for the data, like `numWords`; `<type>` is the type of the data, like `Int`; and `<data>` is the literal, like `42`. Note that the `<type>` annotation is optional; Scala can generally infer the type of your data, so it's often more an annotation for you and your fellow coders than for the compiler's benefit.

Anyway, we can assign and reassign variables by defining the variable once, then repeating the assignment statement without the `var` notation:

```
scala> var x = 12
x: Int = 12

scala> x = 24
x: Int = 24
```

Note that once you assign a variable, all reassignments of that variable must be of the same type. So, while `x` can equal `24`, attempting to reassign `x` to `"twenty-four"` results in a type error:

```
scala> x = "twenty-four"
<console>:8: error: type mismatch;
 found   : String("twenty-four")
 required: Int
       x = "twenty-four"
           ^
```

The only exception to this rule is when one type can be automatically converted to another. For example, defining a variable of type `Double`, then reassigning it to a value of type `Int`:

```
scala> var myDouble = 2.7
myDouble: Double = 2.7

scala> myDouble = 85
myDouble: Double = 85
```

However, the same is not true in reverse:

```
scala> var myInt = 85
myInt: Int = 85

scala> myInt = 2.7
<console>:8: error: type mismatch;
 found   : Double(2.7)
 required: Int
       myInt = 2.7
               ^
```

### Values

In most languages, variables are the pattern for working with named, assigned memory storage. However, Scala is a multi-paradigm language that supports aspects of both imperative and functional programming--and in functional programming, one goal is to minimize the number of ["moving parts"](https://twitter.com/mfeathers/status/29581296216).

That is, in Scala, we want to avoid as much mutability and as many side-effects as possible. So, instead of reassigning variables throughout the codebase, we try to use as many _values_ as possible, instead.

Values, like variables, are typed storage units, but instead of being mutable, they are _immutable_--that is, once you assign a value to a piece of data, that assignment never changes. Values are the default method for storing data in Scala, and you can define a new value using the `val` keyword:

```
val <identifier>[: <type>] = <data>
``` 

For example we can assign `x` to the value `25`, but attempting to reassign `x` afterwards will result in an error:

```
scala> val x: Int = 25
x: Int = 25

scala> x = 30
<console>:8: error: reassignment to val
       x = 30
         ^
```

Note that for the sake of convenience, _while in the REPL_ you can override previous values, but this is not possible in static files.

### Types

Types are, essentially, definitions of what _kinds_ of data you're working with.

I won't get super into them here, because a lot of the context for types is clearer when you start talking about object-oriented programming in Scala, IMHO.

# Exercises

1. In the Scala REPL, convert the temperature value of 22.5 Centigrade to Fahrenheit. The conversion formula is cToF(x) = (x * 9/5) + 32.

2. The REPL can load and interpret Scala code from an external file with the `:load <file>` command. Create a new file named `Hello.scala` and add a command that will print a greeting, then execute it from the REPL.
