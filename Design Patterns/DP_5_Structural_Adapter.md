# Design Patterns Notes - Adapter - 6

### Adapter Pattern

- Structural Design Pattern

- Allows incompatiable objects to work together by providing a wrapper that converts the interface of one class into another interface.

```java
public class PhonePe {
    public BankAPIAdapter bankAPI;

    public PhonePe(BankAPIAdapter bankAPI) {
        this.bankAPI = bankAPI;
    }

    public void fetchTotalFunds(String accNumber) {
        double totalFunds = bankAPI.getFunds(accNumber);
        System.out.println("You have " + totalFunds + " money in your account.");
    }
}

public class YesBankAPI {
    public double getTotalBalance(String accNumber) {
        // business logic
    }

    public boolean sendMoney(String accNumber, double money) {
        // business logic
    }
}

public class ICICIBankAPI {
    public double checkBalance(String accNumber) {
        // business logic
    }

    public boolean transferMoney(String accNumber, double money) {
        // business logic
    }
}

public interface BankAPIAdapter {
    public double getFunds(String accNumber);
    public boolean sendFunds(String accNumber, double funds);
}

public class YesBankAPI implements BankAPIAdapter {
    // implement the methods of the interface
}

public class ICICIBankAPI implements BankAPIAdapter {
    // implement the methods of the interface
}
```

#### Client code -

```java
public class Client {
    public static void main(String[] args) {
        BankAPIAdapter adapter = new YesBankAPIAdapter();
        PhonePe app = new PhonePe(adapter);
        app.fetchTotalFunds();
    }
}
```
