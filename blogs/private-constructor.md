![image](https://github.com/Firasama29/my-blog/assets/67781796/d38e763c-fdcc-4eb3-a574-9d4802082feb)

# When Should We Use A Private Constructor In Java

A constructor in Java is a special type of method that has the same name as the class and is used to initialize objects. It is automatically called when creating an object of a class using the keyword <pre>new</pre>.

There are two types of constructors: a ***default no-args*** constructor which takes no parameters and is provided by Java compiler in case one is not explicitly defined, and a ***parameterized constructor*** which accepts one or more parameters.

We can define a constructor with any access modifier like <pre>public</pre>, <pre>private</pre>, <pre>protected</pre> or <pre>package</pre> to limit the level of access to the constructor from outside the class.

Since the purpose of constructors is to instantiate a class, or in other words, to create objects, it makes sense to define a public constructor to allow any class to access it and create the desired object. On the other hand, it would seem that defining a private constructor would defeat the purpose as it would prevent it to be accessed from outside the class. So what exactly is the point of having one?

In this blog post, we’re going to discuss the use cases of private constructors and the rules for creating them.

Let’s see the example below. If we define a private constructor and attempt to call it in the main method, Java compiler will throw a compile error:
```java
  public MyObject{
      private int numberOfObjects;
      private String name;
      // private constructor
      private MyObject() {}
  }
  
  public class MainClass {
      public static void main(String[] args) {
          MyObject obj = new MyObject();   // compile error
      }
  }
```
So how can we make use of a private constructor if we can’t access it? And when should we use it?

In the next section, we’ll discuss the use cases and an example to demonstrate how to take advantage of a private constructor.

## Use Cases Of Private Constructors
There are some use cases where private constructors are applicable. For instance, they’re used to:

- ***implement singleton design pattern***: A singleton class is a class that limits the instantiation of a class to only one. Let’s look at an example. Below we have a singleton class that contains a private constructor and a static method <pre>getInstance()</pre>:
```java
  public class SingletonClass {
      private static SingletonClass INSTANCE;
  
      private SingletonClass() {}
  
      public static SingletonClass() {
          if(INSTANCE == null) {
              INSTANCE = new SingletonClass();
          }
          return INSTANCE;
      }
  }
```

  The private constructor ensures that the class can only be instantiated from within the class itself, whereas the role of the static method is to return an instance of the class if invoked from anywhere in case there’s no existing instance. So since the private constructor will not be directly approachable from outside the boundaries of its class, other classes will only be able to instantiate the class once by invoking SingletonClass.getInstance().

- ***in utility and constant-only classes*** where only static member methods or fields are used. Static methods and fields can be directly called without the need to create an object. In this case, using a private constructor prevents the instantiation of the class. Here’s a quick example:
```java
  public class MyUtils {
  
    // private constructor to prevent instantiation of the class
    private MyUtils() {}
  
    // static method
    public static int calculateSum(int num1, int num2) {
      return num1 + num2;
    }
  }

  public class MyConstants {
   
    private MyConstants() {}
    
   // static member variable
    public static final String RESULT = "result = ";
  }
  
  public class MyClass {
    public static void main(String[] args) {
  
      int result = MyUtils.calculateSum(20, 50);
      System.out.println(MyConstants.RESULT + result);
    }
  }
```
As you can see, we’ve defined a public static utility method to return the sum of two integers, and a static constant field in another class. To invoke both the method and field, there’s no need to create an instance of their classes since both are static. A simple MyUtils.calculateSum(20, 50) and <pre>MyConstants.RESULT</pre> will be enough.

## Rules Of A Private Constructor
There are some rules that we should consider when dealing with private constructors, such as:

- they must be defined using the private access modifier
- they cannot be accessed from outside the class in which it is defined
- they do not allow initializing an object from outside the class
- they do not allow a class to extend this class

You can find more details on this topic [here](https://stackoverflow.com/questions/17342815/whats-the-use-of-private-constructor-in-java) and [here](https://www.baeldung.com/java-private-constructors).
