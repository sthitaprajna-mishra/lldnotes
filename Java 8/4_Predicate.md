# Predicate

- The Predicate interface is a functional interface that represents a boolean-valued function of one argument.

- `test(T t):` This method takes an argument of type T and returns a boolean value. It evaluates some condition on the input object t and returns true if the condition is satisfied, otherwise, it returns false.

```java
public class Client {
    public static void main(String[] args) {
        Predicate<Integer> isEven = x -> x%2 == 0;
        System.out.println(isEven.test(12));

        Predicate<Integer> greaterThan10 = x -> x > 10;
        System.out.println(greaterThan10.test(20));

        // OR
        System.out.println(isEven.or(greaterThan10).test(6));

        // AND
        System.out.println(isEven.and(greaterThan10).test(6));

        // NEGATE
        System.out.println(isEven.negate().test(2));

        // ISEQUAL
        System.out.println(Predicate.isEqual(2).test(6));
    }
}
```
