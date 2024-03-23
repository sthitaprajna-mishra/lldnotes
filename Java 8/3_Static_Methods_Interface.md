# Static Methods in Interface

- Interfaces were enhanced to support the declaration of static methods.

- Static methods in interfaces provide a way to define utility methods that are related to the interface's functionality but do not depend on any specific implementation.

- The implementation class cannot override the interface's static methods because the interface's static methods are just not visible to the implementation class.

**NOTE:**

- We can now write the main method `public static void main(String[] args)` inside an interface and run it as a Java application too.
