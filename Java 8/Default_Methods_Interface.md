# Default Methods in Interface

- Allows interfaces to provide method implementations by adding the keyword `default` before the return type.

- This feature enables the addition of new methods to existing interfaces without breaking backward compatibility with implementing classes.

- Classes that implement the interface can choose to override the default method if they want to provide a different implementation.

### Ambiguity Issue

Suppose there are 2 interfaces A and B, and both of them have the same default method defined in their bodies with the exact same method signature.

If a class implements both these interfaces, which method does it take after - A or B?

```java

interface A {
    default void testMethod() {
        System.out.println("A says hello!");
    }
}

interface B {
    default void testMethod() {
        System.out.println("A says hello!");
    }
}
```

#### This code will not compile:

```java
// ERROR
class C implements A, B {
    public static void main(String[] args) {
        C objC = new C();
        C.testMethod();
    }
}
```

#### **Solution:** Override the default method in the class and either call super for any one parent interface or write its own definition.

#### Option 1

```java
class C implements A, B {
    public static void main(String[] args) {
        C objC = new C();
        C.testMethod();
    }

    @Override
    public void testMethod() {
        A.super.testMethod();
    }
}
```

#### Option 2

```java
class C implements A, B {
    public static void main(String[] args) {
        C objC = new C();
        C.testMethod();
    }

    @Override
    public void testMethod() {
        System.out.println("Child class says hello!");
    }
}
```
