# maven-experiment
Understanding Maven source exclusion

## Steps to run the source exclusion experiment:

### Clone this repository:
```
$ cd && mkdir maven-experiment-clone && cd maven-experiment-clone && \
  git clone https://github.com/keghani/maven-experiment.git && cd maven-experiment
```

### See pom.xml:
```
...
        <configuration>
          <directory>com/keghani/hello</directory>
        </configuration>
...
```

### Generate the jar file:
```
$ mvn package
$ jar tf target/maven-experiment-1.0.0.jar
```
Check that you see ```Hello.class``` and ```Exclude.class```.
```
$ java -cp target/maven-experiment-1.0.0.jar com.keghani.hello.Hello
```
Get "Hello".
```
$ java -cp target/maven-experiment-1.0.0.jar com.keghani.hello.Exclude
```
Get "Hello" again.

### Update pom.xml to exclude ```Exclude.java```:
```
...
        <configuration>
          <directory>com/keghani/hello</directory>
          **<excludes>
            <exclude>com/keghani/hello/Exclude.java</exclude>
          </excludes>**
        </configuration>
...
```

### Confirm that the jar file now excludes ```Exclude.class```:
```
$ mvn clean
$ ls
```
Check that the ```target``` directory is no longer present.
```
$ mvn package
$ jar tf target/maven-experiment-1.0.0.jar
```
Check that you see ```Hello.class``` but not ```Exclude.class```.
```
$ java -cp target/maven-experiment-1.0.0.jar com.keghani.hello.Hello
```
Get "Hello".

## Acknowledgements:
Thanks to @jias0001 for the references!

## References:
*    [Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)
*    [Viewing the Contents of a JAR File](https://docs.oracle.com/javase/tutorial/deployment/jar/view.html)
*    [Stackoverflow: "Maven: excluding java files in compilation"](http://stackoverflow.com/questions/17920920/maven-excluding-java-files-in-compilation/19713000#19713000)
