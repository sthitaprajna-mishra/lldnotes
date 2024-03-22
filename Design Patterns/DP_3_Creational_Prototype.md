# Design Patterns Notes - Prototype - 4

### Prototype and Registry Pattern

- Creational Design Pattern

- Lets you copy existing objects without making your code dependent on their classes.

- This pattern delegates the cloning process to the actual objects that are being cloned.

### Prototype - Interface

```java
public interface Prototype {
    public Car clone();
}

public class Car implements Prototype {
    private String brand;
    private String color;
    private String model;
    private int topSpeed;

    public Car() {}

    public Car(Car otherCar) {
        this.brand = otherCar.brand;
        this.color = otherCar.color;
        this.model = otherCar.model;
        this.topSpeed = otherCar.topSpeed;
    }

    @Override
    public Car clone() {
        return new Car(this);
    }
}
```

### Prototype - Abstract class

```java
public abstract class Vehicle {
    private String brand;
    private String color;
    private String model;

    public Vehile(Vehicle vehicle) {
        this.brand = vehicle.brand;
        this.color = vehicle.color;
        this.model = vehicle.model;
    }

    public abstract Vehicle clone();
}

public class Car extends Vehicle {
    private int topSpeed;

    public Car() {}

    public Car(Car otherCar) {
        super(otherCar);
        this.topSpeed = otherCar.topSpeed;
    }

    @Override
    public Car clone() {
        return new Car(this);
    }
}

public class Bus extends Vehicle {
    private int doors;

    public Bus() {}

    public Bus(Bus otherBus) {
        super(otherBus);
        this.doors = otherBus.doors;
    }

    @Override
    public Bus clone() {
        return new Bus(this);
    }
}
```

### Shallow Copy vs Deep Copy in Prototype Pattern

```java
public class Car extends Vehicle {
    private int topSpeed;
    public GSPSystem gpsSystem;

    public Car() {}

    public Car(Car otherCar) {
        super(otherCar);
        this.topSpeed = otherCar.topSpeed;
        // this.gpsSystem = new GpsSystem(); // -> This is shallow copy
        this.gpsSystem = other.gpsSystem.clone(); // --> This is deep copy
    }

    @Override
    public Car clone() {
        return new Car(this);
    }
}
```

### Prototype with Registry

```java
public class VehicleCache {
    private Map<string, Vehicle> vehicleCache = new HashMap<>();

    public VehicleCache() {
        Car car = new Car();
        car.brand("...");
        ...

        Bus bus = new Bus();
        bus.brand("...");
        ...

        cache.put("Buggati Chiron", car);
        cache.put("Mercedes Setra", bus);
    }

    public Vehicle get(String key) {
        return this.vehicleCache.get(key).clone();
    }
}
```
