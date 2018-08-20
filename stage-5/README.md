# Common Collections

A collections framework provides data structures for collecting one or more values of a given type, such as with arrays, lists, maps, sets, and trees. Most popular programming languages have their own collections frameworks--at the very least, lists and maps--because such structures are widely applicable in software enginering.

The notion of "collections" was first popularized by the Java collections library, which is high-performance, object-oriented, and typed. Fortunately, since Scala is a JVM language, you can use the entire Java collections library from your Scala code. However, there are benefits to using the Scala collections library that we'll discuss in a bit.

## Lists: All the Things

The Scala collections library defines _many_ functions on all of the different types of collections, so we'll start with one type of collection, and then you can just assume the other collections behave similarly. ;)

`List` is an immutable, singly-linked list. You can create a list using the following syntax:

```
scala> val names = List("Jon", "Maulan", "Alex", "kf", "Pete", "mbl")
names: List[String] = List(Jon, Maulan, Alex, kf, Pete, mbl)
```

One thing you can do with `List`s--collections in general--is iterate over them using for-comprehensions, as we did before:

```
scala> for (name <- names) {
     |   name match {
     |     case "Jon" | "Alex" | "kf" | "Pete" | "mbl" =>
     |       println(s"$name is an engineer!")
     |     case "Maulan" =>
     |       println(s"$name is a manager!")
     |     case _ =>
     |       println(s"IDK $name!")
     |   }
     | }
Jon is an engineer!
Maulan is a manager!
Alex is an engineer!
kf is an engineer!
Pete is an engineer!
mbl is an engineer!
```

### Higher-Order Functions

Scala also provides a number of _higher-order_ functions defined on collections, which makes it easier to manipulate collections without manually iterating over them. Higher-order functions are functions that either (1) take another function as a parameter or (2) return another function.

One example of a higher-order function is `foreach`, which takes a procedure and invokes it with every item in the list. Instead of writing

```
scala> for (name <- names) { println(name) }
Jon
Maulan
Alex
kf
Pete
mbl
```

we can write

```
scala> names foreach println
Jon
Maulan
Alex
kf
Pete
mbl
```

Similarly, if we want to get the number of letters in each person's name, instead of writing

```
scala> for (name <- names) yield { name.length }
res3: List[Int] = List(3, 6, 4, 2, 4, 3)
```

we can use `map`, which takes a function that converts a single list element to another value and/or type: 

```
scala> names map { n => n.length }
res4: List[Int] = List(3, 6, 4, 2, 4, 3)
```

We could even shorten this further using an underscore

```
scala> names map { _.length }
res5: List[Int] = List(3, 6, 4, 2, 4, 3)
```

where the underscore replaces a variable name we don't particularly care about.

Finally, let's say we wanted to concatenate all the names in our list together. Instead of creating a `for` loop, creating a `var`, and iterating over `names`--updating the `var` every time we wanted to add a name--we can use the higher-order function `reduce`:

```
scala> names.reduce{(acc, n) => acc + ", " + n }
res10: String = Jon, Maulan, Alex, kf, Pete, mbl
```

Note that, when using higher-order functions, you can either use the anonymous function syntax, or just pass in a function directly.

#### Other Higher-Order Functions

There are lots of other higher-order functions built into the Scala collections library, but to be honest, the CAP codebases don't use them very frequently.

One such function is `foldLeft` which maybe appears once somewhere in Pulsar vaguely:

```
scala> List(4, 5, 6).foldLeft(0)(_ + _)
res11: Int = 15
```

Here, we're performing a reduce from right to left, with 0 as the initial accumulator.

## Maps

Another type of collection that appears in lots of places is the `Map`! You can create a `Map` like so:

```
scala> val namesAndTitles = Map("Maulan" -> "Manager 2", "Jon" -> "VP 2", "Alex" -> "Senior Software Engineer", "mbl" -> "Distinguished Engineer")
namesAndTitles: scala.collection.immutable.Map[String,String] = Map(Maulan -> Manager 2, Jon -> VP 2, Alex -> Senior Software Engineer, mbl -> Distinguished Engineer)
```

How to actually fetch keys out of the map will come next!

# Exercises

Using built-ins...

1. Find the last element of a list.

2. Find the kth element of a list.

3. Find the number of elements of a list.

4. Reverse a list.