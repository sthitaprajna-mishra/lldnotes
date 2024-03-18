# Design Patterns Notes - Facade - 7

### Facade Pattern

- A structural design pattern that provides a simplified interface to a complex system of classes, interfaces, or subsystems.

- It hides the complexities of the subsystem and provides a single interface to the client.

- This helps in decoupling the client from the subsystem, making the client code easier to understand and maintain.

```java
// Subsystem class 1
class CPU {
    public void freeze() {
        System.out.println("CPU is freezing");
    }

    public void jump(long position) {
        System.out.println("Jumping to position: " + position);
    }

    public void execute() {
        System.out.println("CPU is executing commands");
    }
}

// Subsystem class 2
class Memory {
    public void load(long position, byte[] data) {
        System.out.println("Loading data at position: " + position);
    }
}

// Subsystem class 3
class HardDrive {
    public byte[] read(long lba, int size) {
        System.out.println("Reading data from hard drive");
        return new byte[size];
    }
}

// Facade class
class ComputerFacade {
    private CPU cpu;
    private Memory memory;
    private HardDrive hardDrive;

    public ComputerFacade() {
        this.cpu = new CPU();
        this.memory = new Memory();
        this.hardDrive = new HardDrive();
    }

    public void start() {
        cpu.freeze();
        memory.load(0, hardDrive.read(0, 1024));
        cpu.jump(0);
        cpu.execute();
    }
}
```

#### Client code -

```java
public class Client {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.start();
    }
}
```
