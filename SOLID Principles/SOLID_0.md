# SOLID Principles Notes

### What are SOLID Principles?

SOLID Principles are a set of 5 rules and best practices that developers follow while working on designing class structures. They serve the same purpose - to create

- understandable
- readable
- testable
- extensible
- maintainable

code for developers to collborate on.

Following the SOLID acronym they are -

- **S**ingle Responsibility Principle
- **O**pen-Closed Principle
- **L**iskov Substitution Principle
- **I**nterface Segregation Principle
- **D**ependency Inversion Principle

### Single Responsibility Principle

A class should do only one thing and thus, it should have only one reason to change.

### Open-Closed Principle

Classes should be open to extension but closed to modification.

### Liskov Substitution Principle

Subclasses should be substitutable for their base classes.

Child class should expand the behaviour of their parent class, not narrow it down.

Eg: Given class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.

### Interface Segregation Principle

It is better to have multiple client-specific interfaces than have one general purpose interface.

Clients should not be forced to implement a function they do not need.

### Dependency Inversion Principle

Classes should depend on interfaces and abstract classes instead of concrete classes.

High level modules should not depend on low level modules directly but on abstractions.
