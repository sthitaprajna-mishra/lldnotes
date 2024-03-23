# Supplier

- The Supplier interface is a functional interface that represents a supplier of results.

- It doesn't accept any input arguments but produces a result of a specified type.

```java
@FunctionalInterface
public interface Supplier<T> {
    T get();
}
```

- `get()`: This method takes no arguments and returns a result of type `T`. It represents the operation of supplying or generating a value.

```java
import java.util.function.Supplier;

public class Main {
    public static void main(String[] args) {
        // Defining a supplier to generate a random integer
        Supplier<Integer> randomNumberSupplier = () -> (int) (Math.random() * 100);

        // Getting a random number
        int randomNumber = randomNumberSupplier.get();
        System.out.println("Random number: " + randomNumber);
    }
}
```
