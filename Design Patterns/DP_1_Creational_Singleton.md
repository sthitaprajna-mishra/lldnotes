# Design Patterns Notes - Singleton - 2

### Singleton Pattern

- Creational Design Pattern

- This ensures that a class has only one instance, and provides a global point of access to it.

### Naive Singleton

```java
public class Singleton {
    private static Singleton uniqueInstance;

    private Singleton() {}

    public static Singleton getInstance() {
        if(uniqueInstance == null) {
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
    }
}
```

### Need for improvement

A naive or simple implementation of the Singleton pattern may not work correctly in a multithreaded environment due to potential race conditions.

In a multithreaded environment, consider the following scenario:

- Thread 1 checks if instance is null and finds it to be true.
- Before Thread 1 creates the instance, Thread 2 also checks if instance is null and finds it to be true.
- Thread 1 creates an instance and sets instance to the newly created instance.
- Thread 2 also creates an instance and sets instance to a new instance, thus overriding the instance created by Thread 1.

This scenario leads to the violation of the Singleton pattern because there are now multiple instances of the Singleton class, which is not the intended behavior.

### What exactly is a race condition?

A race condition is a type of concurrency bug that occurs in a multithreaded environment when the outcome/correctness of a program depends on the relative timing or interleaving of operations performed by multiple threads.

Race conditions occur when two or more threads access shared resources (such as variables, data structures, or I/O devices) concurrently, and the final outcome of the program becomes unpredictable or incorrect due to the non-deterministic nature of thread scheduling.

### Thread-safe Singleton (using Double-Checked Locking)

```java
public class Singleton {
    private volatile static Singleton uniqueInstance;

    private Singleton() {}

    public static Singleton getInstance() {
        if(uniqueInstance == null) {
            synchronized(Singleton.class) {
                if(uniqueInstance == null) {
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```
