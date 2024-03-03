![image](https://github.com/Firasama29/my-blog/assets/67781796/869a3342-187b-41bb-96f2-a6b61e4e4d32)

# Basic Java Questions and Answers (Part 1) — Type-Casting

I’ve compiled a list of questions and answers about fundamental topics in Java that I believe every Java developer should be aware of. This is part 1, covering the concepts of ***type-casting***, ***upcasting*** and ***downcasting***.

## What is type-casting?
**Type-casting** refers to the process of converting from one data type to another.

## What are the conditions for type-casting?
To convert between data types:

- the data types must be compatible. We can convert an <pre>int</pre> to a <pre>float</pre> or vice versa, but we can’t convert between an <pre>int</pre> and a <pre>String</pre>. A compile error will be thrown in this case.
- the data type that we convert into must be larger than the original data type. Otherwise, Java will complain. However, this is still possible with a workaround, which we will discuss in the next section.

## What are the categories of type-casting?
There are two types of type-casting:

- ***Widening conversion (implicit casting)***: If we cast a smaller data type to a larger one, Java compiler will automatically perform the casting. For example, if we want to convert from <pre>int</pre> to a <pre>double</pre>, we only need to assign the <pre>int</pre> value to a <pre>double</pre> because integers are smaller (32 bits) than doubles (64 bits), so there is no risk of data loss after conversion. Here’s a code snippet to demonstrate this:
  ```java
    double number = 10;      //output = 10.0, which is a double
  ```
  We declared a <pre>double</pre> variable and assigned to it an integer value of 10. Since an integer is smaller than a double, the double will easily have more than enough room to store that value.

- ***Narrowing conversion (explicit casting)***: If we cast a larger data type to a smaller one, Java compiler will complain and will not perform the conversion. For instance, attempting to cast a <pre>double</pre> to an <pre>int</pre> will trigger a compile error. To solve this, we can explicitly cast the value to the smaller data type using the casting operator ():
  ```java
  int number = (int) 10.50;  //output = 10, which is an integer
  ```
  Contrary to the previous example, the double value of 10.50 is assigned to an integer. Without an explicit operator, a portion of data would be lost since it's larger than what an integer can hold. So we use the casting operator (int) next to the double value so that it gets converted and stored as an integer.

> Type-casting with primitive types vs reference types

> type-casting not only works works on primitive types, but on reference types as well, although in slightly different ways due to the inherent difference between primitive and reference type variables.

## What is Upcasting?
Upcasting is a process of implicitly casting a subclass to a superclass and is closely related to inheritance. Before we further discuss this, let’s look an example:
```java
public class Vehicle {
    private String name;

    public Vehicle() {}
}

public class Car extends Vehicle {
    private String model;

    public Car() {
        super();
    }

    public String getModel() {
        return model;
    }
}
```
As you can see, there are two classes, **Vehicle** and **Car**. The **Car** class extends or inherits **Vehicle**. In this scenario, when we create an object of type **Car**, we can either assign it to a reference of type **Car** class like so:
```java
Car vehicle = new Car();
```
Or assign it to a reference of type Vehicle, which is the superclass:
```java
Vehicle vehicle = new Car();
```
This is an example of upcasting where the compiler implicitly casts the subclass to the superclass.

Using upcasting, we can access all methods defined in the superclass from the subclass but we’re restricted from calling the methods in the sublcass itself. If we attempt to call a method in the subclass based on the last example, the compiler will complain:
```java
Vehicle vehicle = new Car();
```

## What is Downcasting?
Downcasting is the reverse of upcasting. It’s a process of converting from the superclass to the subclass.

Let’s modify the previous example:
```java
// Upcasting
Vehicle vehicle = new Car();

// Downcasting
if(vehicle instanceof Vehicle) {
    Car car = (Car) vehicle;
    car.driveCar();
}
```
We use <pre>instanceof<pre> to check if the vehicle reference is an instance of Vehicle class before explicitly downcasting using the <pre>(Car)</pre> operator. This is a way to prevent <pre>ClassCastException</pre> at runtime.

Downcasting is particularly useful in cases where we have an instance of a superclass but we need to use the fields and methods of a subclass. Since we can only access superclass fields and methods in this scenario, downcasting is an approach to solve this problem.

There you have it. This is part one of the series of Java questions and answers. I hope what we’ve discussed so far was helpful. Stay tuned for part two.

Thanks for reading.
