# Stage 1: Installfest

## Installfest

### Java Runtime

Scala is a language that runs on the Java Virtual Machine (JVM), so first, you'll need to install a Java runtime.

The CAP team currently uses Scala 2.11 on all our active projects, which requires at least Java 6. However, it's better to use a more recent version of the Java JDK; most people (I think?) use the Java 8 JDK (Java Developer Kit), instead.

Accordingly, you can install the Java 8 JDK [directly from Oracle's website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). Installers are available, so you shouldn't need to manually configure your PATH variable to get the applications installed.

### Scala

I'm going to assume that you're using OS X, because that's what everyone on the CAP team has used thus far!

Accordingly, you should be able to install Scala automatically using [Homebrew](http://brew.sh/). To get started, open up a new Terminal window and run the following command to install Homebrew:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Then, install Scala by running the command

```
brew install scala
```

### sbt

Another thing you'll need to install is [sbt](http://www.scala-sbt.org/), which stands for either "Simple Build Tool" or "Scala Build Tool," depending on whom you ask.

Again, you can install this using a one-line Terminal command:
```
brew install sbt
```

### Typesafe Activator

Some folks on the CAP team also use [Typesafe Activator](https://www.typesafe.com/get-started), a wrapper around SBT that includes--amongst other things--the tools needed to get started with several popular Scala frameworks, [Play](https://www.playframework.com/) and [Akka](http://akka.io/).

At some point (now or later!) you'll probably want to install Activator. There are two options for installing Activator:

1. Installing the [full package](http://downloads.typesafe.com/typesafe-activator/1.3.2/typesafe-activator-1.3.2.zip?_ga=1.251349253.2047759469.1432133512), or
2. Installing the [mini package](http://downloads.typesafe.com/typesafe-activator/1.3.2/typesafe-activator-1.3.2-minimal.zip?_ga=1.184838442.2047759469.1432133512), which comes without bundled dependencies.

Note that the full package can take a while to download, but it includes fun things like a graphical user interface (GUI) for exploring Scala project templates, as well as nearly all of the dependencies you'd need to get started with a new Scala project.