# Exercise: The Basics

Maven describes builds using a POM file, `pom.xml`, which describes the "project object model".

## Getting started

There is a `pom.xml` file in this directory but it does not contain enough information to do anything.

What happens when you ask Maven to process this file?

    mvn package

Set the properties that are needed based on the error message and the reference doc below. (There
are 3, the Maven coordinates.) What happens now when you run `mvn package`?

## Lifecycle stages

Maven builds projects by following a set of steps called "lifecycles".

Examine the output of running `mvn package`.

1. What lifecycle stages are executed?
2. What files are created in the filesystem?

The output (e.g., a `jar`) from a build is referred to as an _artifact_. What
is the filename of the artifact from your build?

Here is another common Maven invocation:

    mvn clean

What happens here?

Can you run some of the lifecycle stages independently? (You can run `mvn` with no arguments to
see a list of possible lifecycle stages.) What happens when you provide multiple stages? How does
clean compare to the other stages?

How does Maven's behavior compare to other build tools that you are familiar with?

## Exploring the build and POM

Try running:

    mvn -X package
    mvn help:help
    mvn help:effective-pom

What do these commands tell you? When might these commands be useful?

## Bonus

Can you make the `[WARNING]`s in the build output go away?

# References

* [Maven in 5 minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)
* [POM reference](https://maven.apache.org/pom.html)
