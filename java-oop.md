# Notes for Java OOP

[LinkedIn Learning Class](https://www.linkedin.com/learning/java-object-oriented-programming-2/)

## Intro

### Key Attributes

- Abstraction
- Inheritance
- Encapsulation
- Polymorphism

The goal of these pillars is to reduce complexity and enable code reusability.

### Types of Java Classes

- Class
- Enum
- interface

### Create a Class

When you create a class, make a constructor using the name of the class.

```java
public class Tree {
  Tree(double height, double width, TreeType type) {
    this.height = height;
    this.width = width;
    // type is an Enum
    this.type = type;
  }
}
```
