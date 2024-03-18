# Basic Java Questions and Answers (Part 3) — Instance vs Static
![image](https://github.com/Firasama29/my-blog/assets/67781796/af318c56-907b-491b-9f9e-4d99eb675a6a)

I’ve compiled a list of questions and answers about fundamental topics in Java that I believe every Java developer should be aware of. This is part 3, covering the concepts of instance vs static variables and methods and the difference between them.

## What is the difference between instance and static methods and fields?
- Instance methods are regular methods that are dependent on individual instances of a class and can be used to perform operations specific to each object. They are a common aspect of Object-Oriented Programming languages like Java. However, there are situations where we may need to define a field or method inside a class that can function independently, regardless of the class object. These are called static methods.
- Static methods belong to the class itself, while instance methods are associated with a class object.
- Static methods are created using the keyword `static`:

    ```java
    public class StaticExample {
        public static void calculateTotalPrice() {
            System.out.println(10 * 12.50);
        }
    }
    ```

- We can now invoke this method using the class name itself:

  `StaticExample.calculateTotalPrice();`

- On the other hand, instance methods are created using a reference of a class instance:
  ```java
    public class Example {
     private double price;
     private int quantity;
     // constructor
     public Example(double price, int quantity) {
         this.price = price;
         this.quantity = quantity;
     }

     public void calculatePrice() {
         System.out.println(price * quantity);
     }
  }

  class MainClass {
      public static void main(String[] args) {
          Example example = new Example();
          // calling instance method using an Object reference
          example.calculatePrice();
      }
  }
  ```

- We created a class called Example which has two fields and a method. Then once we instantiated an object of Example class inside the main method, we were able to use its reference to invoke the `calculatePrice()` method. Unlike static methods, without an object, we cannot access that instance method.

## What happens if you try to access an instance field or method within a static method?

This scenario triggers a compile error. Let’s look at an example:
  ```java
  public class Item {
      private String category;
      private double price;
  
      public void displayCategory() {
          System.out.println(category);
      }
  
      public static void displayPrice() {
          System.out.println(price);  //compile error
      }
  }
```

We tried to reference the price variable inside the static method `displayPrice()`. If you hover over price, you'll notice this error:

`Non-static field 'price' cannot be referenced from a static context`

Java compiler throws an error because we’re trying to call a non-static field within a static method.

**But why is it allowed to call an instance field inside an instance method but not inside a static method?**

This is due to the difference between static vs instance fields and methods. As we mentioned before, instance fields and methods are associated with an instance of the class, while static ones are associated directly with the class. Static methods are restricted from accessing non-static data as they are only allowed to operate on the class as a whole, not on a particular object.

## What are the advantages and drawbacks of instance methods and static ones?
### Instance methods:
**Advantages:**

- Access to instance variables: instance methods have direct access to instance data, allowing them to operate and modify the state of the object.
- Encapsulation: instance methods play a role in Object-Oriented Programming by bundling the data and methods that operate on that data into a single unit.
- Polymorphism: using the concept of instance methods, subclasses can override methods of their superclasses.

**Drawbacks:**

### Static methods:
**Advantages:**

- No dependency on objects: static methods do not require an object to be instantiated since they belong to the class itself.
- Global accessibility: they can be invoked globally within the scope of the class.

**Drawbacks:**

- Access restriction to instance-specific data: static methods can only work on static data and are not allowed to access instance variables and methods.
- Not suitable for Polymorphism: unlike their counterpart, static methods do not work well with Polymorphism as they cannot be overriden by subclasses.

The most common static method in Java is none other than the “main” method, which serves as the entry point in any Java program.

The “main” method is static because it needs to be called before any object is instantiated.

There you have it. This is part three of the series of Java questions and answers. I hope what we’ve discussed so far was helpful. Stay tuned for the next one.
