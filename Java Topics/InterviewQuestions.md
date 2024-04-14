# Basic Java Interview Questions

## Contents

1. [What is class and object?](#1-what-is-class-and-object)
2. [Which class is the superclass of all objects in Java and why?](#2-which-class-is-the-superclass-of-all-objects-in-java-and-why)
3. [How can we say that a particular language is an object-oriented programming language?](#3-how-can-we-say-that-a-particular-language-is-an-object-oriented-programming-language)
4. [Difference between procedural programming language and object-oriented programming language.](#4-difference-between-procedural-programming-language-and-object-oriented-programming-language)
5. [What is encapsulation?](#5-what-is-encapsulation)
6. [What do you mean by tightly encapuslated?](#6-what-do-you-mean-by-tightly-encapuslated)
7. [What are varargs?](#7-what-are-varargs)
8. [What do you mean by the terms Composition and Aggregation?](#8-what-do-you-mean-by-the-terms-composition-and-aggregation)
9. [What are daemon threads? How are they different from non-daemon threads?](#9-what-are-daemon-threads-how-are-they-different-from-non-daemon-threads)
10. [What is serialization? Explain the use of the transient keyword.](#10-what-is-serialization-explain-the-use-of-the-transient-keyword)
11. [What is Reflection in Java?](#11-what-is-reflection-in-java)
12. [Explain the Iterable and Iterator interfaces.](#12-explain-the-iterable-and-iterator-interfaces)
13. [Explain the Comparable and Comparator interfaces.](#13-explain-the-comparable-and-comparator-interfaces)
14. [What if 2 interfaces have same default method signatures but different implementation and a class implements both the interfaces, how to know which interface's default implementation will be called?](#14-what-if-2-interfaces-have-same-default-method-signatures-but-different-implementation-and-a-class-implements-both-the-interfaces-how-to-know-which-interfaces-default-implementation-will-be-called)
15. [What is the need of a ConcurrentHashMap and how is it different from HashMap? Also, what are fail-fast and fail-safe iterators?](#15-what-is-the-need-of-a-concurrenthashmap-and-how-is-it-different-from-hashmap-also-what-are-fail-fast-and-fail-safe-iterators)

### 1. What is class and object?

#### **Class**

A class can be understood as a template or a blueprint, which contains some values, known as data members, and some set of rules, known as behaviors or methods.

#### **Objects**

An object is an instance of a class. It is a specific entity created from the class, and it represents a real-world concept.

In simpler terms, a **class defines the structure and behavior**, while an **object is an actual representation of that structure in memory**.

### 2. Which class is the superclass of all objects in Java and why?

`java.lang.Object` class is the root or superclass of the class hierarchy, which is present in `java.lang` package. All predefined classes and user-defined classes are the subclasses from `Object` class.

**Every object has common properties.**

To reduce the burden on the developer SUN developed a class called Object by implementing all these properties.

All these methods have generic logic common for all the subclasses, if this logic is not satisfying subclass requirement then subclass can override it. Some of the common ones are -

**Comparing two objects**

```java
public boolean equals(Object obj)
```

**Retrieving hashcode**

```java
public int hashcode()
```

**Retrieving the run time class object reference**

```java
public final Class getClass()
```

### 3. How can we say that a particular language is an object-oriented programming language?

A language is considered object-oriented if it supports the four fundamental principles of OOP:

- encapsulation
- inheritance
- polymorphism
- abstraction

### 4. Difference between procedural programming language and object-oriented programming language.

| Procedural Programming                                                                       | Object-Oriented Programming                                                                 |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| In procedural programming, the program is divided into small parts called **functions**.     | In object-oriented programming, the program is divided into small parts called **objects**. |
| Procedural programming follows a **top-down approach**.                                      | Object-oriented programming follows a **bottom-up approach**.                               |
| There is no access specifier in procedural programming.                                      | Object-oriented programming has access specifiers like private, public, protected, etc.     |
| In procedural programming, there is no concept of data hiding and inheritance.               | In object-oriented programming, the concept of data hiding and inheritance is used.         |
| Procedural programming does not have any proper way of hiding data so it is **less secure**. | Object-oriented programming provides data hiding so it is **more secure**.                  |

### 5. What is encapsulation?

Encapsulation is the bundling of data and methods that operate on that data into a single unit, i.e., a class. It helps in hiding the internal state of an object and restricting access to the internal details.

### 6. What do you mean by tightly encapuslated?

If each variable is declared as private in the class, it is called tightly encapsulated class in Java.

For a tightly encapsulated class, we are not required to check whether the class contains getter and setter method or not and whether these methods are declared as public or not. For example -

```java
// TightEncapsulationExample.java
package com.sthmishra.interview;

public class TightEncapsulationExample {
    private double balance;

    public double getBalance() {
        return balance;
    }
}
```

### 7. What are varargs?

In Java, varargs (variable-length arguments) is a feature introduced in Java 5 that allows a method to accept a variable number of arguments of the same type. This is particularly useful when the number of arguments that a method needs to accept is not known in advance.

The syntax for declaring a method with varargs is to specify the type followed by an ellipsis `...` after the parameter type. For example:

```java
public void methodName(Type... parameterName) {
    // Method body
}
```

You can pass any number of arguments of the specified type, including zero, to a varargs parameter. Inside the method, the varargs parameter is treated as an array of the specified type.

```java
public void printValues(String... values) {
    for (String value : values) {
        System.out.println(value);
    }
}
```

You can call this method with any number of String arguments:

```java
printValues("Hello", "World"); // Output: Hello\nWorld
printValues("Java", "is", "awesome"); // Output: Java\nis\nawesome
printValues(); // Output: (nothing printed)
```

**Varargs and other parameters**

A method can have other parameters in addition to the varargs parameter, but the varargs parameter must be the last parameter declared in the method signature.

```java
public void printDetails(String name, int... scores) {
    System.out.println("Name: " + name);
    System.out.print("Scores: ");
    for (int score : scores) {
        System.out.print(score + " ");
    }
    System.out.println();
}
```

You can call this method like this:

```java
printDetails("Alice", 80, 85, 90); // Output: Name: Alice\nScores: 80 85 90
```

**Zero or more arguments**

If a varargs parameter is not supplied with any arguments, it will behave as an empty array of the specified type inside the method.

### 8. What do you mean by the terms Composition and Aggregation?

**Composition**

In composition, one class owns the other class. The owned class cannot exist independently of the owning class. If the owning class is destroyed, the owned class is also destroyed.

In Java, composition is often implemented by including an instance of one class as a field in another class. For example:

```java
public class Car {
    private Engine engine;

    public Car() {
        this.engine = new Engine();
    }
    // Other methods and fields...
}
```

**Aggregation**

In aggregation, one class is associated with another class, but there is no ownership implied. The associated class can exist independently of the owning class.

Aggregation implies a weaker relationship compared to composition. Aggregation can also be implemented using fields, but the associated class can be provided externally or created independently:

```java
public class University {
    private List<Department> departments;

    public University(List<Department> departments) {
        this.departments = departments;
    }
    // Other methods and fields...
}
```

### 9. What are daemon threads? How are they different from non-daemon threads?

In Java, a daemon thread is a type of thread that runs in the background and does not prevent the Java Virtual Machine (JVM) from exiting when the program finishes execution.

Daemon threads are typically used for background tasks such as garbage collection, monitoring, or other non-critical tasks that can be terminated when the main program exits.

Daemon threads are considered non-essential threads because they do not prevent the JVM from shutting down. When all non-daemon threads (also known as user threads) have finished executing, the JVM exits, regardless of whether daemon threads are still running. They are not guaranteed to execute to completion.

You can create a daemon thread by calling the `setDaemon(true)` method on a `Thread` instance before starting it, or by subclassing `Thread` and overriding the `isDaemon()` method to return true.

```java
Thread daemonThread = new Thread(() -> {
    // Daemon thread task
});
daemonThread.setDaemon(true);
daemonThread.start();
```

**The main thread cannot be declared as a daemon thread.** It is a user (non-daemon) thread.

Daemon threads are useful for tasks that should not delay the termination of the JVM but need to perform some work in the background. However, since they can be abruptly terminated when the JVM exits, they should not be used for critical operations or tasks that require orderly cleanup.

### 10. What is serialization? Explain the use of the transient keyword.

Serialization in Java is the process of converting an object into a byte stream, which can then be saved to a file, sent over the network, or stored in a database. This byte stream can later be deserialized, or converted back into an object, allowing it to be reconstructed.

To enable serialization for an object in Java, the class of that object must implement the Serializable interface. It is a marker interface, i.e., it does not contain any method.

This interface acts as a marker, indicating that the objects of the class can be serialized.

```java
import java.io.Serializable;

public class MyClass implements Serializable {
    // Class definition
}
```

**Transient Keyword**

Fields in a serializable class can be marked as `transient` to exclude them from serialization. These fields will not be saved as part of the serialized object.

Serialization is commonly used for storing objects persistently, transferring objects between applications, and caching objects in memory. However, it's important to consider security concerns and versioning issues when designing serialized classes, as serialized data can be manipulated and evolve over time.

### 11. What is Reflection in Java?

Reflection in Java is a powerful feature that allows you to inspect and manipulate classes, interfaces, fields, methods, and constructors at runtime.

It provides a way to analyze the structure of a class and access its members dynamically, without knowing their names at compile time. Reflection is extensively used in frameworks like Spring, Hibernate, and JavaBeans, where classes are dynamically loaded and configured.

Reflection is provided through the `java.lang.reflect` package. Reflection allows you to inspect the structure of a class, including fields, methods, constructors, annotations, and interfaces implemented.

```java
Field[] fields = MyClass.class.getDeclaredFields();
Method[] methods = MyClass.class.getDeclaredMethods();
Constructor<?>[] constructors = MyClass.class.getDeclaredConstructors();
```

### 12. Explain the Iterable and Iterator interfaces.

**Iterable Interface**

The Iterable interface represents a collection of elements that can be iterated over. It provides a way to obtain an `Iterator` instance for traversing the elements in the collection.

`Iterator<T> iterator()`: Returns an iterator over elements of type `T`, allowing sequential access to the elements in the collection.

**Iterator Interface**

The `Iterator` interface provides methods for traversing a collection of elements one by one. It allows you to iterate over elements without exposing the underlying implementation of the collection.

`boolean hasNext()`: Returns true if the iteration has more elements, false otherwise.
`T next()`: Returns the next element in the iteration.
`void remove()`: Removes the last element returned by `next()` from the underlying collection. This method is optional and may not be supported by all iterators.

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> myList = new ArrayList<>();
        myList.add("Apple");
        myList.add("Banana");
        myList.add("Orange");

        // Using Iterable and Iterator
        for (String fruit : myList) {
            System.out.println(fruit);
        }

        // Equivalent usage using Iterator explicitly
        Iterator<String> iterator = myList.iterator();
        while (iterator.hasNext()) {
            String fruit = iterator.next();
            System.out.println(fruit);
        }
    }
}
```

### 13. Explain the Comparable and Comparator interfaces.

Both `Comparator` and `Comparable` are interfaces used for comparing objects, but they serve different purposes and are used in different contexts.

**Comparable Interface**

The `Comparable` interface is used to define the natural ordering of objects. When a class implements `Comparable`, it specifies how its instances should be compared to one another.

`int compareTo(T o)`: Compares this object with the specified object for order. It returns a negative integer, zero, or a positive integer if this object is less than, equal to, or greater than the specified object, respectively.

Implementing `Comparable` allows objects of a class to be automatically ordered in collections (e.g., `TreeSet`, `TreeMap`) and sorted using utility methods (e.g., `Arrays.sort()`).

**Comparator Interface**

The `Comparator` interface is used to define custom comparison logic for objects that do not have a natural ordering or when you want to override the default ordering provided by `Comparable`.

`int compare(T o1, T o2)`: Compares its two arguments for order. It returns a negative integer, zero, or a positive integer if the first argument is less than, equal to, or greater than the second argument, respectively.

```java
public class Person implements Comparable<Person> {
    private String name;
    private int age;

    // Getters and setters

    @Override
    public int compareTo(Person other) {
        return this.name.compareTo(other.name);
    }
}
```

```java
public class AgeComparator implements Comparator<Person> {
    @Override
    public int compare(Person p1, Person p2) {
        return Integer.compare(p1.getAge(), p2.getAge());
    }
}
```

```java
List<Person> people = new ArrayList<>();
// Add people to the list

Collections.sort(people, new AgeComparator());
```

### 14. What if 2 interfaces have same default method signatures but different implementation and a class implements both the interfaces, how to know which interface's default implementation will be called?

In Java, if a class implements two interfaces that both define a default method with the same signature but different implementations, the compiler will raise a compile-time error because of the ambiguity. This situation violates the interface's rules for default methods, which state that an implementing class should be able to determine which default method implementation to use.

To resolve this ambiguity, the implementing class must explicitly override the default method and provide its own implementation. This allows the class to specify which default method implementation to use.

```java
public interface InterfaceA {
    default void myMethod() {
        System.out.println("Default implementation of myMethod in InterfaceA");
    }
}

public interface InterfaceB {
    default void myMethod() {
        System.out.println("Default implementation of myMethod in InterfaceB");
    }
}

public class MyClass implements InterfaceA, InterfaceB {
    @Override
    public void myMethod() {
        InterfaceA.super.myMethod(); // Specify which default method to call
    }
}
```

### 15. What is the need of a ConcurrentHashMap and how is it different from HashMap? Also, what are fail-fast and fail-safe iterators?

`ConcurrentHashMap` is a specialized implementation of the `Map` interface in Java that is designed to support concurrent access by multiple threads without the need for external synchronization. It achieves this through internal mechanisms such as partitioning the map into segments and using fine-grained locking.

It was introduced in Java 5 to address the shortcomings of `HashMap` in concurrent multi-threaded environments.

However, `HashMap` incurs less memory overhead compared to `ConcurrentHashMap` because it does not need additional synchronization mechanisms.

**Fail-fast and Fail-safe iterator**

Iterators over `HashMap` are **fail-fast**, meaning they throw `ConcurrentModificationException` if the map is modified structurally while iterating (excluding through the iterator's own `remove` method).

Iterators over `ConcurrentHashMap` provide weakly consistent behavior. They may not reflect the most recent updates made to the map during iteration but do not throw `ConcurrentModificationException`.
