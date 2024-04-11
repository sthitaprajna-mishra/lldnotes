# Design Patterns Notes - Facade - 7

### Facade Pattern

- Structural Design Pattern

- Provides a simplified interface to a complex system of classes, interfaces, or subsystems.

- It hides the complexities of the subsystem and provides a single interface to the client.

- This helps in decoupling the client from the subsystem, making the client code easier to understand and maintain.

```java
// Subsystem - AccountManagement
class AccountManagement {
    public void createAccount(String accountType) {
        System.out.println("Creating a new " + accountType + " account");
        // Implementation details...
    }
}

// Subsystem - TransactionProcessing
class TransactionProcessing {
    public void deposit(int accountId, double amount) {
        System.out.println("Depositing $" + amount + " to account ID " + accountId);
        // Implementation details...
    }

    public void withdraw(int accountId, double amount) {
        System.out.println("Withdrawing $" + amount + " from account ID " + accountId);
        // Implementation details...
    }
}

// Subsystem - CustomerService
class CustomerService {
    public void updateAddress(int customerId, String newAddress) {
        System.out.println("Updating address for customer ID " + customerId + " to " + newAddress);
        // Implementation details...
    }
}

// Facade
class BankFacade {
    private AccountManagement accountManagement;
    private TransactionProcessing transactionProcessing;
    private CustomerService customerService;

    public BankFacade() {
        this.accountManagement = new AccountManagement();
        this.transactionProcessing = new TransactionProcessing();
        this.customerService = new CustomerService();
    }

    public void openAccount(String accountType) {
        accountManagement.createAccount(accountType);
    }

    public void deposit(int accountId, double amount) {
        transactionProcessing.deposit(accountId, amount);
    }

    public void withdraw(int accountId, double amount) {
        transactionProcessing.withdraw(accountId, amount);
    }

    public void updateAddress(int customerId, String newAddress) {
        customerService.updateAddress(customerId, newAddress);
    }
}
```

#### Client code -

```java
public class Main {
    public static void main(String[] args) {
        BankFacade bankFacade = new BankFacade();

        // Using facade to perform operations
        bankFacade.openAccount("Savings");
        bankFacade.deposit(123456, 1000);
        bankFacade.withdraw(123456, 500);
        bankFacade.updateAddress(987654, "123 Main Street");
    }
}
```
