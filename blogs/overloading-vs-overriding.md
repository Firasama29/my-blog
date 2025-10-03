# Guide to Method Overloading vs. Overriding
![img.png](../images/img.png)

Method overloading and overriding are two forms of Polymorphism in Java. In this article we’re going to discuss each concept, their characteristics and key rules when working on them.

## What is Method Overloading?
Method overloading is a way to have two or more methods with the same name defined in the same class. It’s used to enhance code readability and making code clean by reusing the same method name.

Let’s create a class called Shape and declare two methods: One to calculate the area of a circle and the other to calculate the area of a triangle:

```java
  public class Shape {
  
    //area of a circle
    public double calculateArea(double radius) {
        return 3.14 * radius * radius;
    }
    
    //area of a triangle
    public double calculateArea(double base, double height) {
        return 0.5 * base * height;
    }
  }
```

The above code is valid and we can invoke the methods and print the output. But here’s a question: _how does Java compiler distinguish which method is being invoked?_

The distinguishing factor here is the number of arguments. Java compiler examines the method signature: the method name, number and types of parameters and determines which method is the target. If method signatures are identical, an error will be thrown. Here’s how the methods are called:
```java
  Shape shape = new Shape();
  
  System.out.println(shape.calculateArea(3.5));
  System.out.println(shape.calculateArea(2.0, 3.0));
```

In other cases, it can also differentiate the methods according to the type and order of the arguments.

```java
  public class Person {
  
      public static String getIdentity(String name, int age, String nationality) {
        return name + " is " + age + " years old and he's from " + nationality;
      }
  
      public static String getIdentity(String name, String nationality, int age) {
        return name + " is from " + nationality + " and he's " + age + " years old.";
      }
  }
```
Both methods have the same number of arguments, but in a different order. In both cases, based on the input arguments, Java will decide at runtime which method version to invoke and print the output accordingly.

Now another question: _What’s the point of overloading? Why can’t we just declare a method of any name?_

Let’s answer this question with a simple example. Say you declare a simple method that calculates the square of two integers:

```java
  public int getSquareOfTwoNumbers(int num1, int num2) {
    return num1 * num2;
  }
```
At some point later, you decide you want to reuse this method to get the square of two variables of type double. You might be tempted to call the above method and pass two arguments of type double, but this will obviously trigger a compile error because the method is expecting two int arguments, not double.

In this case, you might simply declare another method of any name, for instance, `getSquareOfTwoDoubles()`. This will work just fine, but you can also leverage method overloading to simplify your code and make it more elegant and readable. You wouldn’t need to worry about naming conflict because as we discussed earlier, Java compiler is smart enough to figure out they’re not entirely identical.

#### Overloading rules:

- number and order of parameters must be different.
- it’s performed in the same class.

### What is Method Overriding?
Method overriding is similar to overloading, except that it is specifically used to provide specific implementation in subclasses of the method that is already defined in the superclass. This is where subclasses can redefine the behavior of the superclass by overriding its methods.

Let’s rewrite the earlier code to demonstrate this:

```java
  public class Shape {
  
      //this is method of the superclass
      public double calculateArea() {
          return 0.0;
      }
  }

  public class Circle extends Shape {
    private double radius = 12.5;

    //we override the parent mathod
    @Override
    public double calculateArea() {
        return 3.14 * radius * radius;
    }
  }
  
  
  public class Triangle extends Shape {
    private double base = 6.7;
    private double height = 1.0;
  
    //we override the parent method
    @Override
    public double calculateArea() {
        return 0.5d * base * height;
    }
  }
```
The overridden method in each subclass has the same name and return type as that of the parent class with the only difference is the implementation in the method body.

Now, when it comes to method overriding, we create an instance of each subclass that inherits the superclass, then using each instance, we call their respective version of the `calculateArea()` method. The choice of the version of method to be called is determined based on the object type. Check this out:

```java
  public static void main(String[] args) {
    Shape circle = new Circle();      //object of type Cirlce
    Shape triangle = new Triangle();  //object of type Triangle
    
    System.out.println(circle.calculateArea()); //area of a circle = 490.625
    
    System.out.println(triangle.calculateArea()); //area of a triangle = 3.35
  }
```

Method `circle.calculateArea()` is of type `Car`, while `triangle.calculateArea()` is of type `Triangle`. Using method overriding, both objects called the same method but produced different output.

### Overriding rules:
- methods must have the same name and return type.
- methods must have the same type and order of arguments.
- methods are annotated with `@Override`.
- you cannot override `static` or `final` methods.


### Conclusion
To recap, method overloading allows us to declare any number of methods of the same name in the same class provided they have different parameters.
Method overriding, on the other hand, enables subclasses to implement any method in the superclass and define their own implementation.

Thanks for reading!