# Hello, World

## Hello World Example in Java

Here is a simple "Hello, World!" program in Java:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

## Instructions to Run the Program

1. **Install Java Development Kit (JDK)**:
    - Download and install the JDK from the [official Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) or use a package manager like `brew` on macOS:
      ```sh
      brew install openjdk
      ```

2. **Set Up Your Environment**:
    - Ensure that the `JAVA_HOME` environment variable is set correctly. You can add the following line to your `.bash_profile`, `.zshrc`, or equivalent:
      ```sh
      export JAVA_HOME=$(/usr/libexec/java_home)
      export PATH=$JAVA_HOME/bin:$PATH
      ```

3. **Create the Java File**:
    - Create a new file named `HelloWorld.java` and paste the above code into it.

4. **Compile the Java Program**:
    - Open a terminal and navigate to the directory where `HelloWorld.java` is located.
    - Compile the program using the `javac` command:
      ```sh
      javac HelloWorld.java
      ```

5. **Run the Compiled Program**:
    - After compilation, a file named `HelloWorld.class` will be generated in the same directory.
    - Run the program using the `java` command:
      ```sh
      java HelloWorld
      ```

You should see the output:
```
Hello, World!
```