# Design Patterns Notes - Decorator - 8

## Decorator Pattern

- Lets you attach new behaviours to an object by placing them inside a special wrapper that contains these behaviours.

- It's useful when you want to add new functionality to objects without subclassing.

```java
// Component Interface
public interface Pizza {
    String getDescription();
    double getCost();
}

// Concrete Component
public class PlainPizza implements Pizza {
    @Override
    public void getDescription() {
        return "Plain pizza";
    }

    @Override
    public double getCost() {
        return 100.00;
    }
}

// Decorator
public abstract class PizzaDecorator implements Pizza {
    Pizza decoratedPizza;

    public PizzaDecorator(Pizza pizza) {
        this.decoratedPizza = pizza;
    }

    public String getDescription() {
        return this.decoratedPizza.getDescription();
    }
    public double getCost() {
        return this.decoratedPizza.getCost();
    }
}

// Concrete decorator
public class Cheese extends PizzaDecorator {
    public Cheese(Pizza pizza) {
        super(pizza);
    }

    @Override
    public String getDescription() {
        return super.getDescription() + "+ Cheese";
    }

    @Override
    public double getCost() {
        return super.getCost() + 20.00;
    }
}

// Concrete decorator
public class Olives extends PizzaDecorator {
    public Olives(Pizza pizza) {
        super(pizza);
    }

    @Override
    public String getDescription() {
        return super.getDescription() + "+ Olives";
    }

    @Override
    public double getCost() {
        return super.getCost() + 10.00;
    }
}

// Concrete decorator
public class Paneer extends PizzaDecorator {
    public Paneer(Pizza pizza) {
        super(pizza);
    }

    @Override
    public String getDescription() {
        return super.getDescription() + "+ Paneer";
    }

    @Override
    public double getCost() {
        return super.getCost() + 25.00;
    }
}
```

#### Client code -

```java
public class Client {
    public static void main(String[] args) {
        // Creating a plain pizza
        Pizza plainPizza = new PlainPizza();
        System.out.println("Description: " + plainPizza.getDescription());
        System.out.println("Cost: $" + plainPizza.getCost());

        // Adding cheese to the plain pizza
        Pizza cheesePizza = new Cheese(plainPizza);
        System.out.println("Description: " + cheesePizza.getDescription());
        System.out.println("Cost: $" + cheesePizza.getCost());

        // Adding olives to the cheese pizza
        Pizza olivesAndCheesePizza = new Olives(cheesePizza);
        System.out.println("Description: " + olivesAndCheesePizza.getDescription());
        System.out.println("Cost: $" + olivesAndCheesePizza.getCost());

         // Adding paneer to the olives+cheese pizza
        Pizza paneerOlivesAndCheesePizza = new Paneer(olivesAndCheesePizza);
        System.out.println("Description: " + paneerOlivesAndCheesePizza.getDescription());
        System.out.println("Cost: $" + paneerOlivesAndCheesePizza.getCost());
    }
}
```
