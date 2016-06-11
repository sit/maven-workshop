# Exercise: Java essentials

## Source organization

Maven expects certain files to be in certain locations. At a high-level, the tree
it expects looks something like:

     #
     # This is just an example!
     #
     /project
         pom.xml
         src/
             main/
                 java/                    # Maven automatically will build all source in here
                     com/                 # Directory structure mirrors Java package structure
                         toasttab/
                              demo/
                                  A.java  # Defines a class called A
                                  B.java
                              util/
                                  X.java
                                  Y.java
                 resources/
                     custom.properties
                     logo.png
             test/
                 java/                    # This is just test code.
                     com/
                         toasttab/
                              package1/
                                  ATest.java
                                  BTest.java
                              package2/
                                  XTest.java

The POM is at the top and then source files are in `src/main` and test files
are in `src/test`.  This convention helps Maven reduce the amount of
configuration needed to get a build.

Create the file structure and POM needed for a simple project with one class:

    class StringHolder {
        private final String s;
        StringHolder(String s) {
            this.s = s;
        }
        String get() { return s; }
        // You should probably also override equals and hashCode
    }

It's easiest to do this from the Terminal:

    mkdir -p src/{main,test}/java

Then you can create `src/main/java/StringHolder.java`.

After you've written the POM, use `mvn package` to build the jar.

## Build configuration

By default, Maven compiles your code with source and target Java version 1.5. You may
want something newer. To do this, we need to add some `plugin` configuration to the
`build` section of the POM. Add the following snippet to [set the compiler source
and target](http://maven.apache.org/plugins/maven-compiler-plugin/examples/set-compiler-source-and-target.html)

    <build>
      <pluginManagement>
        <plugins>
          <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
              <encoding>utf8</encoding>
              <source>1.8</source>
              <target>1.8</target>
            </configuration>
          </plugin>
        </plugins>
      </pluginManagement>
    </build>

You can verify what happens by running `mvn -X compile` and also setting
`JAVA_HOME` to point to a Java 7 vs a Java 8 JDK.

## Repository structure

Maven coordinates are used to uniquely identify specific versions/builds of
libraries. Maven then supports publishing libraries (`jar`s) in to a
_repository_. There are two types of repositories: local repositories serve
largely as a cache, remote repositories act as canonical stores of artifacts.

### Local repository

To observe your local repository, run:

    mvn install

Where does `install` live in the Maven lifecycle?  Where is your local
repository? What files are placed into the repository? What is the structure of
your local repository? What else is in there already?

Bonus: how does Maven's management of third-party libraries compare to other
languages (Python, C, Node/npm)?

### Remote repositories

Much like Python has pypi, Node has npm, Ruby has Gems, Java has Maven Central
aka https://search.maven.org/

Use the above site to find the coordinates of a common Java library (e.g.,
Google's Guava library) in Central. Then "Click on a link above to browse the
repository." How do the structure and contents of the remote repository relate
to the local one?

Whereas `mvn install` publishes into your local repository, the command `mvn
deploy` will publish artifacts into a remote repository. This will not work (in
general) out of the box because specific credentials are typically needed to
write to a remote repository.

Most companies have an internal remote repository that proxies into Maven
Central but also holds company internal artifacts for internal consumption.
This is typically a product such as Artifactory or Sonatype Nexus. This is
usually configured in `~/.m2/settings.xml`.

## `dependencies`

Dependencies are specified in the `dependencies` section of the POM, by
specifying a `dependency` element with nested Maven coordinates; Maven handles
resolving the dependencies against a repository, downloading and caching the
artifact. Once the artifact is downloaded, Maven makes the jar available in
the classpath of Java during compilation.

Modify your class Java file to import `com.google.common.base.Strings` and modify the
constructor of `StringHolder` to convert null strings to empty ones using
[`Strings.nullToEmpty`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#nullToEmpty(java.lang.String)). Verify that this does not compile.

Add the latest version of Guava as a dependency to your POM. What happens
when you build now?

## scope

Dependencies can also have something called a _scope_. A scope is essentially
a specific classpath. Two common scopes are `compile` and `test`. The `test` scope
is a superset of the `compile` scope.

Add the latest version of JUnit as a `test` scope dependency. (Use the groupId junit
and artifactId junit.)

Verify that adding `import org.junit.Test` to `StringHolder.java` results in a compilation error.
(Then remove the line.)

Now create a simple test in `src/test/java`:

    import org.junit.*;
    public class StringHolderTest {
        @Test
        public void givenNull_returnsEmpty() {
             StringHolder h = new StringHolder(null);
             Assert.assertNotNull(h.get());
        }
    }

Verify that it compiles.

Bonus: What other scopes are there? What are they for?

## Tests!

You just added a test. Yay! What phase compiles test code? Which phase runs
tests?

What files are created in the filesystem as a result of this?

Note that Maven's convention (over configuration) helps make this pretty
seamless. Tests are run by the [Surefire Plugin](http://maven.apache.org/surefire/maven-surefire-plugin/).

## Resources in your jar

There can also be `src/main/resources` and `src/test/resources`. Put a text file in one of these directories.
What happens when you create the jar?

Bonus: You can access this resource using `getResourceAsStream()`. Give it a spin.

## Useful commands

This gives you a basic understanding of how to build and test with Maven.
Here are some other useful commands to play with.

    mvn -DskipTests package
    mvn dependency:help
    mvn dependency:tree

You can read more about the [Dependency Plugin](http://maven.apache.org/plugins/maven-dependency-plugin/).

# References

* [Maven coordinates](https://maven.apache.org/pom.html#Maven_Coordinates): groupId, artifactId, version and repositories (remote and local)
* [Maven central](https://search.maven.org/)
