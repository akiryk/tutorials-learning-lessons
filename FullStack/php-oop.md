# PHP - Object Oriented Programming

There are four principles to OOP
1. Encapsulation: Bundle like with like. For example, shapes have area, number of degrees, etc, so perhaps we have class Shape.
2. Inheritance: 
3. Polymorphism: Children of Shape might include Rect, Circle, Triange, each with its own implementation of getArea()
4. Abstraction: We hide the implementation details with exposed methods such as getArea(). We don't need to worry about exactly how it works.

## Static and Const
Const properties are accessed with the `self` keyword.

Static properties and methods use `static` or `self` or `parent` depending on what you are trying to do. Use `static` to be more explicit. 
