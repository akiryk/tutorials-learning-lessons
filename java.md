# Java

## Basic Course
https://github.com/LinkedInLearning/learning-java-2825378

### Get started in IntelliJ

Create a new project and then go to `src` and create new class named `Main`.
Add some code.
To run, hover over the Main class in sidebar and choose `Run main.main()`

## Extending Classes
Java uses generic types just like TypeScript. 
```Java
// Create a new class that extends from ArrayList and takes any type
// `D` is arbitrary; it could instead be <AnyType> or something else
public class ModArraylist<D> extends Arraylist<D> {

  // later, you can set D as your type in a function
  public void addElement(D element) {}  
  
// in another class, we can reference the ModArrayList with whatever type we'd like
// <String> says it must be an array of strings;
// The diamond, <>, says it should infer the type.
ModArrayList myArray<String> = new ModArrayList<>();
```

## Polymorphism
An object or function can take many forms — an object can use functionality from different classes depending on the context. For example, a Baker class inherits from a Worker class. `Baker.getWage()` will use a function on `Worker`, but `Baker.measureFlour()` will use `Baker`.

- Polymorphism helps us reduce complexity
- helps us write more reusable code

_Runtime_ vs _Compile-time_ polymorphism 
RunTime is when the specific implementation is determined at runtime. Say you have OddList that extends ArrayList. If you call `.add()` for an instance of OddList and `.add()` for an instance of ArrayList, they both are considered ArrayList -- but the implementation is different. 

Compile Time polymorphism enables you to **overload** a constructor. You can have one that takes, e.g., an array of numbers and another that takes a list of numbers. Java will determin at compile time which constructor to use based on the arguments.

### Override a class method
Duplicate the method exactly. If it takes an element of type `Integer`, you need your method to accept an element of type `Integer`. If it returns boolean, you need to return boolean.
