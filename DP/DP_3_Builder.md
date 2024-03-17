# Design Patterns Notes - Builder - 3

### Builder Pattern

A creational design pattern that allows us to create a complex object on a step by step basis.

For a complex object, the initialization of its many fields is buried under a monstrou constructor.

If an object has many parameters, then every time we need to create an object and don't need some of the parameters, then we would either need to pass in NULL or have multiple overloaded constructors.

In this pattern, we extract the task of object creation to its own class and move it to separat bjects called builders.

```java

public class Student {
    int id;
    String name;
    double percentage;
    int gradYear;

    public Student(Builder builder) {
        this.id = builder.id;
        this.name = builder.name;
        this.percentage = builder.percentage;
        this.gradYear = builder.gradYear;
    }

    public static Builder getBuilder() {
        return new Builder();
    }

    public static class Builder {
        int id;
        String name;
        double percentage;
        int gradYear;

        public Builder setId(int id) {
            this.id = id;
            return this;
        }

        public Builder setName(String name) {
            this.name = name;
            return this;
        }

        public Builder setPercentage(String percentage) {
            this.percentage = percentage;
            return this;
        }

         public Builder setGradYear(int gradYear) {
            this.gradYear = gradYear;
            return this;
        }

        public Student build() {
            return new Student(this);
        }
    }

}

```
