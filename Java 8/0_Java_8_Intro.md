# Java 8

### Why was Java 8 introduced?

- Concise and minimal code

- We were missing functional programming benefits in OOPS nature. But Java is still an OOP language.

- To enable parallel programming. More compatible code for multi core processors.

### What are the features of Java 8?

- **Lambda Expressions**

  - Lambda expressions in Java are a concise way to represent anonymous functions. They do not need a name, hence, anonymous.

  - Example:

  ```
      (x, y) -> x + y
  ```

- **Stream API**

  - It allows developers to perform aggregate operations on collections, such as filtering, mapping, and reducing, in a declarative manner.

- **Date and Time API**

  - Java 8 introduced the `java.time` package, which provides a modern Date and Time API.

  - This API addresses many shortcomings of the legacy `java.util.Date` and `java.util.Calendar` classes, including immutability, thread safety, and better support for time zones.

  - **Optional**

  - Optional is a container object that may or may not contain a non-null value.

  - It's designed to provide a more expressive and safer way of handling null values, thereby reducing the likelihood of NullPointerException errors.

- **Method Reference and Constructor Reference**

  - A way to refer to methods or constructors without invoking them.

  - Reference to a static method: `ContainingClass::staticMethodName`

  - Reference to an instance method of a particular object: `containingObject::instanceMethodName`

  - Reference to an instance method of an arbitrary object of a particular type: `ContainingType::methodName`

  - Reference to a constructor: `ClassName::new`

- **Default Method in Interfaces**

  - Allows interfaces to provide method implementations by adding the keyword `default` before the return type.

  - This feature enables the addition of new methods to existing interfaces without breaking backward compatibility with implementing classes.

  - Classes that implement the interface can choose to override the default method if they want to provide a different implementation.

- **Static Method in Interfaces**

  - Interfaces were enhanced to support the declaration of static methods.

  - Static methods in interfaces provide a way to define utility methods that are related to the interface's functionality but do not depend on any specific implementation.

- **Functional Interface**

  - Java 8 introduced the `@FunctionalInterface` annotation, which can be used to declare functional interfaces although using the annotation is not compulsory.

  - Functional interfaces are interfaces that contain exactly only one abstract method and can be used effectively with lambda expressions.

  - The interface can have any number of default/static methods.
