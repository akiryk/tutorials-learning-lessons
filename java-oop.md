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
  // double, int, boolean, String, etc
  double height;
  
  Tree(double height, double width, TreeType type) {
    this.height = height;
    // type is an Enum
    this.type = type;
  }
}
```

### The main function
Every Java application must have a main function, which starts everything going. It can be in any class you'd like, but we can also just use a Main class:
```java
public class Main {
    // the main function takes String[] as arts; this is required-->
    public static void main(String[] args) {
        // The main function...
    }
}
```
