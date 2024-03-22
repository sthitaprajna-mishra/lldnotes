# Function

- The Function interface is a functional interface that represents a function that accepts one argument and produces a result.

- Function is commonly used when you need to apply a transformation or perform some computation on an object.

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```

- `apply(T t):` This method takes an argument of type T and returns a result of type R. It represents the operation or transformation that the function performs on the input object t to produce the result.

Let's discuss the additional methods provided by the Function interface:

1. `andThen(Function<? super R, ? extends V> after)`:

This method returns a composed function that first applies the current function to its input, and then applies the after function to the result.
It allows you to chain multiple functions together, where the output of one function becomes the input of the next.

Example:

```java
Function<Integer, Integer> multiplyBy2 = num -> num * 2;
Function<Integer, Integer> add3 = num -> num + 3;

Function<Integer, Integer> multiplyAndAdd = multiplyBy2.andThen(add3);
System.out.println(multiplyAndAdd.apply(5)); // Output: 13 (5 * 2 + 3)
```

2. `compose(Function<? super V, ? extends T> before)`:

This method returns a composed function that first applies the before function to its input, and then applies the current function to the result.
It allows you to apply a function before the current function is applied.

Example:

```java
Function<Integer, Integer> multiplyBy2 = num -> num * 2;
Function<Integer, Integer> subtract1 = num -> num - 1;

Function<Integer, Integer> subtractAndMultiply = multiplyBy2.compose(subtract1);
System.out.println(subtractAndMultiply.apply(5)); // Output: 8 ((5 - 1) * 2)
```

3. `identity()`:

This method returns a function that always returns its input argument.
It serves as a placeholder when you need a function that does nothing but return its input.

Example:

```java
Function<Integer, Integer> identityFunction = Function.identity();
System.out.println(identityFunction.apply(5)); // Output: 5
```
