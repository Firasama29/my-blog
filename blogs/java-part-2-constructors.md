# Basic Java Questions and Answers (Part 2) — Constructors

I’ve compiled a list of questions and answers about fundamental topics in Java that I believe every Java developer should be aware of. This is part 2, covering the topic of **Constructors**.

## What is a Java constructor?
- It’s a special type of method that has the same name as the class it contains.
- It’s used to initialize an instance of a class.

## How is a constructor used to initialize an object of a class?
![image](https://github.com/Firasama29/my-blog/assets/67781796/1857a0c8-915a-4a86-a0a5-946ae5774498)

We created an object of `Person` class using the `new` keyword followed by the constructor `Person()`

## What are the types of constructors in Java?
1. ***No-args constructor (default)***
- Can be explicitly defined or else a default one will be provided by Java compiler
- Does not take any parameters. Hence called ‘no-args’
- The syntax is ClassName() {}
- Can be used to create objects and initialize instance variables of a class with their default values:
  ![image](https://github.com/Firasama29/my-blog/assets/67781796/c76cf80f-45ca-4e3d-b504-0b4930808b2a)

2. Parameterized Constructor
- Must be defined with one or more parameters
- Used to create objects and initialize instance variables with customized values. Let’s modify the above example to demonstrate how to create and use a parameterized constructor:
- ![image](https://github.com/Firasama29/my-blog/assets/67781796/66d66a7d-d98b-4bf3-8825-5ba3bb347bb0)

## What are the rules for creating a Java constructor?
There are some rules such as:

- Must have the same name as the class it’s defined in
- Must not have a return type, not even `void`
- If not explicitly defined, a default no-args constructor is provided by Java compiler
- Can have any access modifier like `public`, `private`, `protected` or `package` that determines the level of access to the constructor from another class
- Can call another constructor using the keyword `this()`
- Can call a superclass constructor from the subclass using keyword `super()` provided that the call must be the first statement in the constructor.

## What’s the difference between a constructor and a method?
**Constructor**:

- Used to initialize objects
- Must have the same name as the class
- Does not have a return type
- A default constructor is provided by Java compiler if not explicitly defined

**Method**:

- Used to perform a specific operation
- Can be named anything
- Always has a return type, including `void`
- No method is provided in any case

## What is Constructor chaining?
This concept refers to the process of invoking a constructor from another constructor within the same class or subclass. It’s performed using the keyword `this` in the same class or `super` from the subclass, while making sure the call is the first statement inside the constructor. This is useful in reducing code duplication by reusing the initialization code that's already defined in one constructor. Let’s look at the code below:
![image](https://github.com/Firasama29/my-blog/assets/67781796/105d005e-da72-4b8b-8bf7-a3a0a7f1c73c)

As you can see, we demonstrated two ways to perform constructor chaining:
- `MyClass` has three constructors: a no-arg constructor, a constructor with a single parameter that invokes another 3-parameter constructor and passes a default value in place of the type parameter.
- `MySubClass` class extends `MyClass` and defines a 3-args constructor which invokes a constructor from the subclass.

There you have it. This is part two of the series of Java questions and answers. I hope what we’ve discussed so far was helpful. Stay tuned for the next one.

Thanks for reading.
