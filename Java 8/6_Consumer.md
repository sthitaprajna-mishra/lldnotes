# Consumer

- The Consumer interface is a functional interface that represents an operation that accepts a single input argument and returns no result.

- Consumer is commonly used when you need to perform some action or operation on an object without returning any result.

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```

- `accept(T t)`: This method takes an argument of type T and performs some operation on it. It represents the action or operation that the consumer performs on the input object t.

- Consumer is often used in scenarios where you need to process or operate on elements in a collection, perform side effects, or execute some action on an object.

Here's an example demonstrating the use of Consumer:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;

public class Main {
    public static void main(String[] args) {
        // Creating a list of strings
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        // Defining a consumer to print each element of the list
        Consumer<String> printConsumer = name -> System.out.println("Hello, " + name);

        // Iterating through the list and applying the consumer to each element
        System.out.println("Printing names:");
        names.forEach(printConsumer);

        // Defining a consumer to uppercase each element of the list
        Consumer<String> uppercaseConsumer = name -> System.out.println(name.toUpperCase());

        // Applying the uppercase consumer to each element of the list
        System.out.println("Uppercase names:");
        names.forEach(uppercaseConsumer);
    }
}
```
