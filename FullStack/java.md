# Java

## Basic Course
https://github.com/LinkedInLearning/learning-java-2825378

### Get started in IntelliJ

Create a new project and then go to `src` and create new class named `Main`.
Add some code.
To run, hover over the Main class in sidebar and choose `Run main.main()`

## Numerical types in Java

Whole numbers: int, short, long
Decimals: double, float
Float is more performant, but gives a smaller range.

When we say a language represents `int` values with 32 bits, we mean that every <code>int</code> will have 32 1s and 0s. For example:
<code>00000000000000000000000000000011</code> represents 3. In Java, a double is 64 bits.

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

