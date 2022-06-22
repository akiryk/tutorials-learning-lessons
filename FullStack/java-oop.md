# Notes for Java OOP

[LinkedIn Learning Class](https://www.linkedin.com/learning/java-object-oriented-programming-2/)

## Key Attributes

The goal of these pillars is to reduce complexity and enable code reusability.

- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

## Basics

### Create a class

Types of Java Classes

- Class
- Enum
- interface


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

**The main function**
Every Java application must have a main function, which starts everything going. It can be in any class you'd like, but we can also just use a Main class:
```java
public class Main {
    // the main function takes String[] as arts; this is required-->
    public static void main(String[] args) {
        // The main function...
    }
}
```


## Encapsulation
Binding an object's state and behavior into one unit. AKA, "bundling of data, along with the methods that operate on that data, into a single unit" — i.e. the `Class`.

Java provides 3 access modifiers to manage encapsulation:
- public
- private
- protected

In Java, getters and setters don't _need_ to use the `this` keywords.

## Polymorphism
An object or function can take many forms — an object can use functionality from different classes depending on the context. For example, a Baker class inherits from a Worker class. `Baker.getWage()` will use a function on `Worker`, but `Baker.measureFlour()` will use `Baker`.

- Polymorphism helps us reduce complexity
- helps us write more reusable code

_Runtime_ vs _Compile-time_ polymorphism 
RunTime is when the specific implementation is determined at runtime. Say you have OddList that extends ArrayList. If you call `.add()` for an instance of OddList and `.add()` for an instance of ArrayList, they both are considered ArrayList -- but the implementation is different. 

Compile Time polymorphism enables you to **overload** a constructor. You can have one that takes, e.g., an array of numbers and another that takes a list of numbers. Java will determin at compile time which constructor to use based on the arguments.

### Override a class method
Duplicate the method exactly. If it takes an element of type `Integer`, you need your method to accept an element of type `Integer`. If it returns boolean, you need to return boolean.


## Abstraction
There are two ways to use abstraction:
- `abstract` classes and class methods
- `Interface`

Neither can be instantiated; both must be extended. Implement an interface as a way to enforce a contract: if you extend the `EventInterface`, you must have certain methods and properties. Implement and abstract class if you want to inherit certain methods or properties but for children to implement certain methods. 

A Java class can only extend one `abstract` class, but it can implement as many interfaces as it wants. 

For an interface, use the `implement` keyword:
```java
public class MyClass implements SomeInterface {
```

Example:
```java
// an interface defines methods that implementers must use
public interface Event {
    Long getTimeStamp();
    void process();
}

// this implementer is an abstract class
public abstract class AbstractEvent implements Event {
    protected final Long createdTimestamp;
    protected final String id;
    AbstractEvent(String id) {
        this.id = id;
        this.createdTimestamp = new Timestamp(System.currentTimeMillis()).getTime();
    }

    // It implements getTimeStampe
    @Override
    public Long getTimeStamp() { return this.createdTimestamp; };
    
    // but it uses abstract for process, which must be implemented by the abstract class's implementors
    public abstract void process();
}



