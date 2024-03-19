# Design Patterns Notes - Strategy - 10

## Strategy Pattern

- The Strategy design pattern is a behavioral design pattern that defines a family of algorithms and makes them interchangeable.
- This pattern is especially useful when you have a family of algorithms, and you want to be able to switch between them at runtime.

```java
// Context
class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(double amount) {
        paymentStrategy.pay(amount);
    }
}

// Strategy interface
interface PaymentStrategy {
    void pay(double amount);
}

// Concrete strategy 1
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;
    private String expiryDate;
    private String cvv;

    public CreditCardPayment(String cardNumber, String expiryDate, String cvv) {
        this.cardNumber = cardNumber;
        this.expiryDate = expiryDate;
        this.cvv = cvv;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " via credit card.");
    }
}

// Concrete strategy 2
class PayPalPayment implements PaymentStrategy {
    private String email;
    private String password;

    public PayPalPayment(String email, String password) {
        this.email = email;
        this.password = password;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " via PayPal.");
    }
}
```

#### Client code -

```java
// Client code
public class Main {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        // Use credit card payment strategy
        cart.setPaymentStrategy(new CreditCardPayment("1234 5678 9012 3456", "12/25", "123"));
        cart.checkout(100.0);

        // Use PayPal payment strategy
        cart.setPaymentStrategy(new PayPalPayment("example@example.com", "password123"));
        cart.checkout(200.0);
    }
}
```
