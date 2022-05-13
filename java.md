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
- helps us reduce complexity
- helps us write more reusable code
