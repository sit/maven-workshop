# A hands-on introduction to Maven

The goal of this repository is to provide you with a small set of exercises
that will help you learn key concepts in Maven and how to use them.

## What is Maven?

* Build tool that also tries to do many other things (like manage web sites)
* Favors convention (with configuration) over explicit rules
    * "Build me a jar out of stuff in src/main/java" vs
    * "Run `javac` if these files change, then run `jar cf foo.jar`"
* Based on a plugin architecture to allow extensibility
* Executes a series of build phases ("lifecycle stages")

## Exercises

The following exercises are intended to allow you to explore basic features of
Maven live on your own computer. You should not need to use an IDE. You should
be able to use a terminal and text editor (vim/nano/emacs/Atom/SublimeText/etc)
to edit files. You will also probably need to search the web for various bits
of information about Maven.

1. [Maven basics](0-basics/)
2. [Java essentials](1-java/)

## Other build tools

* [gmake](https://www.gnu.org/software/make/) and [automake](https://www.gnu.org/software/automake/)
    * Make. So great that we built a tool to generate Makefiles!
* [ant](http://ant.apache.org/):
    * Do you like writing build scripts in XML?
* [gradle](http://gradle.org/):
    * "Modern Open-Source Enterprise Build Automation"
    * Adopted by Android
    * Highly configurable DSL based on Groovy, processes dependency graph
* [pants](http://www.pantsbuild.org/) or [buck](https://buckbuild.com/) or [Bazel](http://www.bazel.io/):
    * Flexible beyond Java, fast incremental builds
    * Open Source versions of things built at Twitter and Facebook

## Problems with Maven

* Not fast:
    * Does not know how to incremental build (may be smarter now, but it will run tests on unchanged sources)
    * Not particularly parallelizable, no locking of m2/repository
* Not flexible:
    * Rely on poorly documented, hard to understand plugins
* Not natively multi-module:
    * Try running mvn in a sub-directory

## Resources

* [How Maven Works](http://www.kyleblaney.com/introduction-to-maven/)
* [Maven build lifecycle](http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)
* [POM reference](https://maven.apache.org/pom.html)
* [Maven coordinates](https://maven.apache.org/pom.html#Maven_Coordinates): groupId, artifactId, version and repositories (remote and local)
* [Inheritance](https://maven.apache.org/pom.html#Inheritance) and [aggregation](https://maven.apache.org/pom.html#Aggregation), and how to abstract configuration using inheritance
* [dependencyManagement](https://maven.apache.org/pom.html#Dependency_Management)
* [SNAPSHOT versions](http://books.sonatype.com/mvnref-book/reference/pom-relationships-sect-pom-syntax.html)
