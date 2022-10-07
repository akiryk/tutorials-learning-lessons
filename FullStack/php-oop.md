# PHP - Object Oriented Programming

There are four principles to OOP
1. Encapsulation: Bundle like with like. For example, shapes have area, number of degrees, etc, so perhaps we have class Shape.
2. Inheritance: 
3. Polymorphism: Children of Shape might include Rect, Circle, Triange, each with its own implementation of getArea()
4. Abstraction: We hide the implementation details with exposed methods such as getArea(). We don't need to worry about exactly how it works.

## Static and Const
Const properties are accessed with the `self` keyword.

Static properties and methods use `static` or `self` or `parent` depending on what you are trying to do. Use `static` to be more explicit. 

### Multiple Constructors
To reference the parent from a child, use scope resolution operator: `Parent::__construct($myArg);`

### Destructors
Run when object is deleted. It can go anywhere but cannot take any parameters. The destructor is triggered when garbage collection happens once the class ends.
```php
function __destruct() {
  // perhaps update a database or log something
}
```

### Final keyword
Useful for design reasons to prevent a method from being over-ridden, e.g. for security reasons. 

## Interfaces
A tool for letting developers know they need to implement certain methods for the class to be complete. 

Interface methods must be public and must not have any implementation. 

Implementers must implement all of the interface's methods. 

## Abstract 
Very much like an interface, but you are allowed to define implementation details for 1 or more methods. E.g., you can have an abstract class, `ElecticalAppliance` that has an abstract method, `voltage()`, that will differ by implementation **and** it can also have a non-abstract method that will be shared by all children, `powerOn()`. 

If even one property in a class is of type `abstract`, the entire class must be `abstract` as well. Then we use `extends` keyword for any classes that use that abstract class. 

```php
abstract class Appliance {
  public function powerOn() {
    $this->on = true;
  }
  
  abstract function voltage();
}

class Television extends Appliance {
  public function voltage() {
    //
  }
}
```
