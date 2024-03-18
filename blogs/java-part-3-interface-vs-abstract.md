# Basic Java Questions & Answers (Part 4) — Interface & Abstract Class
![image](https://github.com/Firasama29/my-blog/assets/67781796/b5f6366d-b269-4502-a54e-6015524b876c)
I’ve compiled a list of questions and answers about fundamental topics in Java that I believe every Java developer should be aware of. This is part 4, covering the topic of Interface and Abstract class.

## What are the differences between an interface and an abstract class?

**Definition:**

- An abstract class is a class that is declared using the keyword ‘abstract’ and contains at least one abstract method (a method with no body). It can also have any number of non-abstract methods.

![image](https://github.com/Firasama29/my-blog/assets/67781796/caaa73a6-ae2f-4379-b5ac-aaf454d024e3)

- An interface is declared with the keyword ‘ interface’ and it contains abstract methods.
- Starting from Java 8, interfaces can contain default methods.

![image](https://github.com/Firasama29/my-blog/assets/67781796/33f8f05c-d4c0-42a1-8a64-801e208edd9c)

**Inheritance and Implementation**
- A class can extend an abstract class using the keyword ‘extends’ and it must provide an implementation for all abstract methods in the abstract class. If you do not implement the abstract classes, Java compiler will throw an error.

![image](https://github.com/Firasama29/my-blog/assets/67781796/a73799f9-fcac-4c73-a9bb-b6410d7fe6c5)

- A class can implement an interface using the keyword ‘ implements’ and it must implement all the methods of the interface.
- A class can implement an interface, but an interface cannot extend an abstract class.
- A class can extend only one abstract class and implement multiple interfaces, whereas an interface can extend multiple interfaces.

**Variables:**
- Variables in interfaces are implicitly set as public, static and final. They are treated as constants and cannot be reassigned.
- Abstract classes can have final, non-final, static and non-static variables.

**Abstraction:**
- Abstract classes achieve Abstraction by declaring abstract methods that have no implementation. We can also declare non-public variables and methods in abstract classes.
- Interfaces support Abstraction since they only allow the declaration of abstract methods. Additionally, variables are by default final.

**Polymorphism:**
- Abstract classes can achieve Polymorphism using inheritance and method overriding. Multiple classes can inherit an abstract class and each have to override its method and provide their own implementation:

  ![image](https://github.com/Firasama29/my-blog/assets/67781796/6fa32933-b7a6-46ed-bed9-ddae089cb7ac)

  ```java
  output:
  I am driving a car
  I am driving a truck
  ```
- Interfaces can also achieve Polymorphism using implementation and method overriding. The code will look similar to the above example, except that classes have to implement the interface.

**Instantiation:**
- Neither interfaces nor abstract classes can be instantiated. Meaning you cannot create objects of either of them.

## When to use abstract classes vs interfaces?
The Oracle Java docs examine a list of situations where you need to either use abstract classes or interfaces:
**Use abstract classes when:**
- you have a group of related classes and you want to share common code among them. This promotes code re-usability and avoids duplication.
- you want to declare non-static or non-final fields.

**Use interfaces when:**
- unrelated classes implement the interface.
- you want to take advantage of multiple inheritance. Interfaces support multiple inheritance, which means a class can inherit more than one interface. This allows a class to inherit behaviors from multiple sources, which promotes code re-usability.

- There you have it. This is part four of the series of Java questions and answers. I hope what we’ve discussed so far was helpful. Stay tuned for the next one.
