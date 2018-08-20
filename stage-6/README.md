# Stage 6: Options

If you've ever coded in Java, chances are that you've encountered a `NullPointerException` at some point. Usually, this happens because code in some place vaguely returned `null` when you weren't expecting it, so you didn't write your client code accordingly. And now you have an exception.

In Scala, we skirt this problem altogether by using the `Option` type. `Option[A]` is a container for an optional value of type `A`--i.e. `Option[String]`, `Option[Int]`, etc. If the value of type `A` is present, the `Option[A]` is an instance of `Some[A]`, containing the present value of type `A`. If the value is absent, the `Option[A]` is the object `None`.

By stating that a value may or may not exist at the _type level_, the compiler forces you to deal with this possibility before gross `NullPointerExceptions` get thrown at runtime.

tl;dr Don't use `null`! \o/

## Creating Options

Usually, you can just create an `Option[A]` for a given value by either instantiating the `Some` case class (we'll talk about case classes later!) or just assigning `None`:

```
scala> val someThing: Option[String] = Some("thing")
someThing: Option[String] = Some(thing)

scala> val noThing: Option[String] = None
noThing: Option[String] = None
```

## Actually Using Optional Values

In the last stage, we looked at `Map`s, and then hilariously moved on without learning how to use them.

That's because the main thing you'll probably want to do with a `Map` is get a value out according to its key--and in Scala, that returns an `Option`!

```
scala> val namesAndTitles = Map("Maulan" -> "Manager 2", "Jon" -> "VP 2", "Alex" -> "Senior Software Engineer", "mbl" -> "Distinguished Engineer")
namesAndTitles: scala.collection.immutable.Map[String,String] = Map(Maulan -> Manager 2, Jon -> VP 2, Alex -> Senior Software Engineer, mbl -> Distinguished Engineer)

scala> namesAndTitles.get("Alex")
res12: Option[String] = Some(Senior Software Engineer)

scala> namesAndTitles.get("kf")
res13: Option[String] = None
```

You can check to see if an `Option` is defined:

```
scala> val maybeAge = Some(5)
maybeAge: Some[Int] = Some(5)

scala> val maybeBirthYear = None
maybeBirthYear: None.type = None

scala> maybeAge.isDefined
res14: Boolean = true

scala> maybeBirthYear.isEmpty
res15: Boolean = true
```