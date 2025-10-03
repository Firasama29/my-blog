# How Java Resolves Overridden Methods at Runtime
![img_1.png](../images/img_1.png)
<p style="text-align: center;">Photo by Stefan Heinemann on Unsplash</p>

One of the most prominent features in Java that we’re familiar with as Java developers is method overriding, which is a way to achieve run-time Polymorphism. When a class extends a another, it overrides all methods in the extended class, providing its own implementation of each method. Upon running the program, the overridden version of the method in the subclass is called. How is it that the subclass method and not the original method that is executed?

In this short article, we’re going to dive into the simple yet important concept of Dynamic Method Dispatch which is closely related to run-time polymorphism as well as inheritence.

## Run-time (Dynamic) Polymorphism
Polymorphism is closely tied to Inheritance where subclasses override methods from a superclass or implement methods from an interface with their own behavior. This allows objects of subclass types to reuse the same method but with different behavior. So polymorphism makes code more flexible, reusable and easier to maintain.

There are two types of Polymorphism: compile-time and run-time Polymorphism. We’re going to discuss the latter since it’s the topic of our article. Here’s an example of a class called Vehicle:

```java
  public class Vehicle {

    public void move(String model, double speed) {
      System.out.println("this is a vehicle's model: " + model);
      System.out.println("this is a vehicle's speed: " + speed);
    }
  }

  public class Car extends Vehicle {
    private String type;
  
    // no-args constructor which initializes the type variable with a default value
    public Car() {
      this.type = "Hatchback";
    }
  
    @Override
    public void move(String model, double speed) {
      System.out.println(model + " is a " + type + " with a maximum speed of " + speed + "km/h");
    }
  }
```

In the subclass, we extended the `Vehicle` class and overrode its method. Inside this method, we provided a new implementation. Now we can create an instance like this:

```java
  public static void main(String[] args) {
    Vehicle car = new Car();
    car.move("Honda Civic", 220);
  }

```
When we call the `move()` method, which version will be executed?

Here’s where Dynamic Method Dispatch and run-time Polymorphism comes into the picture. _**Dynamic Method Dispatch**_ (also referred to as dynamic or late-binding) is essentially a process used in parent-child class relationship, in which Java resolves the call to an overridden method at run-time based on the type of object which the reference points to.

Look at the main method above. The reference variable `car` is of type `Vehicle` (superclass) but it references an object of type `Car` (subclass).
So based on the rule of late-binding, the method version that is executed is the one belonging to the subclass. The output will print:

`Honda Civic is a sedan with a maximum speed 220.0km/h`

This is true regardless of how many subclasses inherit the superclass.

## Benefits of Method Overriding
Method Overriding is used extensively in Java due to many benefits, including:

- **Code Reusability**: method overriding allows developers to modify the existing methods from the parent class and create new implementations. This reduces code redundancy.
- **Extensibility**: with method overriding, you can modify or extend the behavior of the parent class methods without directly affecting them, making the code more extensible and adaptable to requirements.
- **Flexibility**: objects of different subclasses can invoke the same method but with specialized behavior depending on the object type. This makes the code more flexible when dealing with changing requirements.
- **Maintainability**: The code becomes easier to maintain and update over time.

In summary, when a superclass-type reference points to an instance of a subclass, Java ensures that the version of the inherited method in the subclass gets executed.

Thanks for reading!