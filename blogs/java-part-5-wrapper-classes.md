# Basic Java Questions and Answers (Part 5) — Wrapper Classes
![image](https://github.com/Firasama29/my-blog/assets/67781796/05a1aea5-e0c2-48c8-a226-058d4474a86d)

I’ve compiled a list of questions and answers about fundamental topics in Java that I believe every Java developer should be aware of. This is part 5 of the series, covering the topic of Wrapper Classes.

## What are Wrapper Classes?
Java provides classes that correspond to primitive types:

`Byte` corresponds to `byte`,

`Boolean` corresponds to `boolean`,

`Character` to `char`,

`Integer` to `int`,

`Float` to `float`,

`Double` to `double`,

`Short` to `short`,

and `Long` to `long`.

Wrapper classes (`Integer`, `Float`, `Double`, `Short`, `Long`) extend the abstract class Number. They’re called ***Wrappers*** or Wrapper classes because they essentially wrap the respective primitive data types and turn them into objects.

## How to convert primitive types into Wrapper classes?

There are two ways to do the conversion:

- **autoboxing**: when you assign a primitive type to a wrapper class object, Java automatically performs the conversion:
  ```java
  int a = 20;

  Integer aObj = a;     //autoboxing
  ```
- **using a constructor**:
  ```java
  Integer aObj = new Integer(5);
  ```
- **using valueOf() method**: Every wrapper class provides a static .valueOf() method:
  ```java
  Integer aObj = Integer.valueOf(62);
  ```

  >> autoboxing and explicit valueOf() method are generally more preferable than using the constructor. This is because the constructor approach creates a new instance of the Wrapper class, whereas when using autoboxing and valueOf(), Java runtime re-uses pre-existing data within the range of -157 to 158 thanks to the ‘Integer Cache’ mechanism.

  >> How does the caching work?

  >> When valueOf() is called for the first time while the integer passed is within the range mentioned earlier, the integer is cached and subsequent calls of the method utilize the cache instead of creating a new object. This is useful because it optimizes memory use. For more details, checkout [this article](https://medium.com/javarevisited/why-is-1-1-is-true-but-1000-1000-is-false-when-dealing-with-wrapper-classes-in-java-53c5a45ed687).
  >>

## How to convert Wrapper classes into primitive types?
There are two ways to achieve this:
- **unboxing**: Java compiler can automatically convert wrapper classes into their corresponding primitive types.
  ```java
  Integer aObj = 5;
  int a = aObj;
  
  Double bObj = 30.6;
  double b = bObj;
  ```
**using intValue() method**: This is a method provided by the wrapper class:
  ```java
  Integer aObj = 5;
  int a = aObj.intValue();

  Double bObj = 30.6;
  double b = bObj.doubleValue();
  ```

## What’s the point of Wrapper Classes?
Wrapper classes extend the usability of primitive types by providing additional object-related capabilities to be used in situations where primitives do not work. They essentially allow you to treat primitives as objects.

There are use cases where we need to use wrapper classes instead of primitive types. For example, when dealing with collections such as Lists, Sets, and Maps, we’re only able to work with objects, not primitive types. This is where wrapper classes come in handy. Let’s look at an example:

```java
List<Integer> numbers = new ArrayList<>();

numbers.add(7);
numbers.add(9);
numbers.add(12);
```
As you can see, we declared an ArrayList of type Integer and added some elements to it.

> Notice that we’re passing a primitive type int where the ArrayList is of type Integer. This works fine due to autoboxing where Java automatically converts the int to its wrapper class before adding it to the ArrayList.

The same goes to other data types.

## Pitfalls of overusing Wrapper Classes

While they are useful in many situations, it’s important to avoid the unnecessary use of Wrapper classes. Wrapper classes are slower and less efficient than primitive types due to the additional processing of autoboxing and creating a Wrapper object. Opting for primitives reduces memory consumption.

That’s it. We briefly covered the topic of Wrapper classes, autoboxing and unboxing. If you have any question or feedback, don’t hesitate to reach out.

Thanks for reading.
