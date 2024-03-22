# Lambdas

- Lambda expressions in Java are a concise way to represent anonymous functions. They do not need a name, hence, anonymous.

- Example:

```
    (x, y) -> x + y
```

- They are different from anonymous inner classes.

- They can use local variables which are final or effectively final only. That means, even if we alter the state of the local variable after the lambda expression, we cannot use it inside the lambda.

```java
public class Client {
    public static void main(String[] args) {
        int a = 100;
        IEmployee emp = () -> {
            System.out.println("a: " + a); // THIS WILL GIVE ERROR
          return 100.0;
        };
        a = 20; // BECAUSE OF THIS

        System.out.println(emp.getSalary());
    }
}
```

#### Anonymous Inner Classes

```java
public interface IEmployee {
    double getSalary();
    String getDesignation();
}

public class Client {
    public static void main(String[] args) {
        IEmployee emp = new IEmployee() {
            @Override
            public double getSalary() {
                return 100.0;
            }

            @Override
            public String getDesignation() {
                return "SDE-2";
            }
        };

        System.out.println(emp.getDesignation());
        System.out.println(emp.getSalary());
    }
}
```
