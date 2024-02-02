# Guide to NullPointerException in Java And How to Avoid it

`NullPointerException` (or `NPE` for short) is one of those dreaded exceptions that every Java developer has to face in their career. We'll discuss the exception, why and when it exists and how to avoid it in detail later, but first, let's understand the concept of null in Java, which is the culprit behind `NullPointerException`.

## What is `null` in java?

- `null` is a special lateral that is used in Java to denote the absence of a value. It indicates that a reference variable does not reference any object in memory. It simply means the variable does not point to any object.

- null is case-sensitive, which means Java compiler will only recognize the word `null`, not `Null` or `NULL`.

- We can assign `null` to a reference type variable (Strings, Objects and arrays):

<pre>
String str = null;

Object obj = null;

int[] intArr = null;
</pre>

- Note that we can only assign null to a variable of reference type, not primitive type. Let's have a quick look at the difference between both in the next section.

## Primitive vs Reference Types

In Java, variables are simply pointers to something in memory. a Primitive points to the value itself while a non-Primitive or Reference type points to a reference of an object.

- Primitive types refer to data types like int, float, double, boolean, etc. When you declare a variable in Java, you must specify what type it is so that the Java compiler can reserve a block of memory to store the value of that type. The variable is simply a reference that points to that memory location. In simpler words, if you want to declare a variable that holds an integer value, then you need to use the type int like this:

<pre>int myInteger = 20;</pre>

- The above code declares the variable `myInteger` of type int and initializes it to the value of 20 . This tells the Java compiler to reserve enough memory to store an integer value.

- In the case of Reference types, when we declare a variable of a non-primitive type such as String, Class, Array, etc., Java creates an object that holds the value of that reference type, stores it on the heap and returns a reference of that object which is then stored in the variable we declared. Through that reference, we can access the object's properties and methods.

- So `null` can only be assigned to reference type variables and not primitives. But why?

- The answer is simple, a primitive type points directly to the value stored in memory, whereas a reference type holds a reference to an object. So for example, if we declare a variable of type String and assign null to it like so:

<pre>String str = null;</pre>

we're essentially saying that the above variable does not point to any object in memory. That's why the concept of null only works with reference types.

## What is `NullPointerException` in Java?

Now that we have some idea about `null` in Java. Let's dive deep into the main topic.

- `NullPointerException` or `NPE` is a common runtime exception that occurs when you attempt to access or perform an operation on an object with a `null` reference. It's a class that extends `java.lang.RuntimeException`, meaning it will be raised once you execute the code. Let's see a quick example:

<pre>
 String str = null
 System.out.println(str.length());
 </pre>

 In the above code, variable `str` is assigned a value of `null`. Then the `.length()` is called to get the length of the String variable, but since it's assigned to `null`, a `java.lang.NullPointerException` will be thrown.

 <pre>
 Exception in thread "main" java.lang.NullPointerException
 </pre>

 - There are many common scenarios where we may encounter this error. According to oracle documentation, here is a list of cases:
 1. Calling the instance method of a `null` object.

 <pre>
String str = null;
System.out.println(str.toUpperCase()); // throws NPE
 </pre>

 2. Accessing or modifying the field of a `null` object.

 <pre>
class MyClass {
    private String name;
    
    public void setName(String name) {
        this.name = name;
    }
    
    public String getName() {
        return this.name;
    }
}

public class Example {
    public static void main(String[] args) {
        Myclass myclass = null; // an object of MyClass assgined as null
        // if we attempt to modify the name
        myClass.setName("java");
        System.out.println(myClass); // throws NPE

        // if we attemp to access the name
        myClass = null;
        System.out.println(myClass.getName()); // throws NPE
    }
}
 </pre>

 3. Taking the length of `null` as if it were an array.

 <pre>
  int[] arr = null;
  System.out.println(arr.length()); // throws NPE
 </pre>

 4. Accessing or modifying the slots of `null` as if it were an array.
  <pre>
  String[] stringArr = null;
  stringArr[0] = "example"; // throws NPE
 </pre>

 5. Throwing null as if it were a **Throwable** value.
 <pre>
class MyClass {
    private String name;

    public String getName() {
        throw null;     
    }                                                
}
            
public class Example {
    public static void main(String[] args) {
        MyClass myClass = new MyClass();
        System.out.println(myClass.getName()); // throws NPE
    }
}
 </pre>


 ## Why is it important to avoid `NullPointerException`

 Null pointer exceptions will occur throughout the application's life unless we make sure to take the necessary precautions to prevent them beforehand as much as possible. This is an important step in the development of an application, but why? Well, because `NullPointerException` can cause some pretty annoying issues.

 - **It can cause the application to crash or behave unexpectedly** because NullPointerException is an unchecked runtime exception. In other words, it only occurs during runtime and causes the application to terminate abruptly. And that's not something you want in your application.

 - **It can be difficult to debug**, especially given the fact that it occurs at runtime. Imagine having to deal with this in complex applications with interdependent components.

 - **Prevention saves developers time and effort** instead of wasting time having to stare at the logs and track the buggy line of code.

 These are by no means the only reasons, but you get the idea. The more we catch errors by surprise, the more reliable and predictable our application would be, thus improving user experience and satisfaction.


 ## How to prevent NullPointerException

 There are various techniques that we can use to handle `NullPointerException`. Let's list down and discuss some of them:

 - **Using simple `null` checks:**
    One of the most basic techniques to prevent `NPE` is by adding a null check to ensure an object is null-safe before accessing it or using any of its methods. We can accomplish this in different ways:
        - with **if-else** statement:
        When comparing two objects, it's always recommended to have the non-null object on the lefthand side of the .equals() method. Otherwise, the code will produce `NullPointerException`. This is because the .equals() method is a member method of an object, so if you try to call a method of an object that is assigned as null then you already know the outcome of doing so. Look at the code below:
   
        <pre>
        String str1 = null;
        String str2 = "Not Null";
        // this will produce NullPointerException
        if(str1.equals(str2)) {
            // do something
        }
        // this will safely pass   
        if(str2.equals(str1)) {
            // do something
        }
   
        </pre>
        Let's see another example of null check on an array
        <pre>
   
        String[] strArr = null;

        if(strArr != null) {
            // do something
        } else {
            // do something        // throws NPE
        }
   
        </pre>

        - with **ternary operator**:
        <pre>
        String str = null;
        String result = str != null ? str : "Hello World!";
        System.out.println(result);
        </pre>
   
        Using this special syntax, if str is not null then return it, otherwise, print "Hello World!". The output of the above code will give us "Hello World!".
 
 - **java.util.Objects:**
    Objects class is a `java.util` class that provides several static utility methods to work with objects. We can use a variety of those methods to handle `NPE` . Let's take a look:
   
    1. `isNull(Object obj)`: returns true if the object is null, otherwise returns false.

        <pre>
        Objects.isNull(null);    // true
        </pre>

    3. `nonNull(Object obj)`: returns true if the object is non-null, otherwise returns false.
        <pre>
        Objects.nonNull(null);   // false
        </pre>

    4. `requireNonNullElse(Object obj, Object defaultObj)`: introduced in Java 9. It returns the first argument if it is non-null, otherwise, it returns the second argument. Keep in mind that if both arguments are null, a `NullPointerExceptionwill` be thrown.

        <pre>
        String value1 = null;
        String defaultValue = "default value";
        // returns defaultObj
        Objects.requireNonNullElse(value1, defaultValue);
        // if both arguments are null
        Objects.requireNonNullElse(null, null);    // NPE 
        </pre>

    6. `requireNonNullElseGet(Object obj, Supplier<? extends T> supplier)`: takes an object and supplier function as arguments. It returns the first argument if it's non-null, otherwise returns the value of Supplier.get() if it is non-null. If both the object and the supplier or value of Supplier.get() are null, we will be greeted by the familiar `NullPointerException`.

        <pre>
        String value1 = null;
        String defaultValue = "default value";
        // returns defaultValue
        Objects.requireNonNullElseGet(value1, () -> defaultValue);
        // if both arguments are null
        Objects.requireNonNullElseGet(null, () -> null);    // NPE
        </pre>

 - **Optional class:**
    - `Optional` is a container object and one of the many features introduced in Java 8 to safely handle `NPE` without the need to resort to null checks. To use it, we start by first wrapping a potentially nullable value in Optional object, then use of one its methods to check whether the value is present and retrieve it if it is.

        <pre>
        Optional<String> value = Optional.ofNullable("foo");
        if(value.isPresent()) {
            System.out.println(value.get());  // returns foo
        }
        </pre>

    - As you can see, we wrapped an `Optional` around a String value of foo and invoked `ofNullable()` static method that returns an Optional object containing that value if it's present or else just returns an empty `Optional`. Let's see more examples of Optional methods:
        
        - `ofNullable()`: returns an Optional containing the value if it is present, or an empty Optional if it is null.
           `Optional<String> myString = Optional.ofNullable(null);`
        
        - `empty()`: returns an empty Optional object in case a value is null.
            <pre>
            Optional<String> value = myString.isPresent() ? myString : Optional.empty();    
            System.out.println(value); // returns Optional.empty
            </pre>

        - `orElse(Object other)`: works similar to `ofNullable()`, but returns a default specified value if the value is not present.
            <pre>
            String defaultValue = myString.orElse("default");
            System.out.println(defaultValue);
            </pre>

        - `orElseGet(Supplier<? extends T> supplier)`: works slightly different from `orElse()`. If the Optional is empty, it returns a value returned by the specified supplier function.
            <pre>
             // method to be passed by the supplier function
             public static String getMessage() {
                 return "Hello World!";
             }
             String defVal = myString.orElseGet(() -> getMessage());
             System.out.println(defVal);
            </pre>

            There is another difference between orElse()and orElseGet():
            orElse() always evaluates the default value regardless of whether the Optional is empty or not.
            orElseGet() only executes the supplier function if the Optional is empty.
            The difference can be more significant in cases where the default value involves expensive computations, making orElseGet() more preferable since it avoids unnecessary operations if the Optional is present.

        - `orElseThrow(Supplier<? extends X> exceptionSupplier)`: if the Optional is empty, this method throws an exception returned by the specified Supplier function.
            <pre>
            String value = myString.orElseThrow(() -> new RuntimeException("the value is not present"));
            System.out.println(value);
            </pre>

        - `isPresent()`: returns true if the Optional contains a non-null value, or false otherwise.
            `System.out.println(myString.isPresent());`

        - `ifPresent(Consumer<? super T> consumer)`: takes a Consumer function as an argument. It uses a lambda expression or method reference to execute a specific action if the value contained within the Optional object is present, otherwise, it does nothing.
            <pre>
            // using lambda expression
            myString.ifPresent(str -> System.out.println(str));
            // method reference
            myString.ifPresent(System.out::println);
            </pre>

 - **Apache Commons StringUtils:**

   - Apache Commons Lang is a third-party library that provides utility classes and methods to deal with Java objects. One of these classes is StringUtils, which contains static methods that work with Strings and can be utilized to prevent NPE. Let's look at some of them:

        - `isEmpty(CharSequence cs)`: returns true if a String is null or empty
            <pre>
                StringUtils.isEmpty(null);    //true
                StringUtils.isEmpty("");      //true
                StringUtils.isEmpty(" ");     //false
            </pre>    

        - `isNotEmpty(CharSequence cs)`: returns false if a String is null or empty

            <pre>
            StringUtils.isNotEmpty(null);    //false
            StringUtils.isNotEmpty("");      //false
            StringUtils.isNotEmpty(" ");     //true
            </pre>

        - `defaultIfEmpty(String str, String defaultStr)`: returns the first argument if it's non-null or not empty. Otherwise, it returns the second argument

            <pre>
            StringUtils.defaultIfEmpty(null, "foo");    // foo
            StringUtils.defaultIfEmpty("", "foo");      // foo
            StringUtils.defaultIfEmpty(" ", "foo");     // whitespace
            </pre>    

        - `isBlank(CharSequence cs)`: returns true if a String is null, empty or contains only whitespace characters

            <pre>
            StringUtils.isBlank(null);    //true
            StringUtils.isBlank("");      //true
            StringUtils.isBlank(" ");     //true
            </pre>

        - `isNotBlank(CharSequence cs)`: returns false if a String is null, empty or contains only whitespace characters

            <pre>
            StringUtils.isNotBlank(null);    //false
            StringUtils.isNotBlank("");      //false
            StringUtils.isNotBlank(" ");     //false
            </pre>

        - `defaultIfBlank(String str, String defaultStr)`: returns the first argument if non-null, not empty or contains whitespace. Otherwise, it returns the second argument. If both arguments are null, it just returns null.

            <pre>
            StringUtils.defaultIfBlank(null, "foo");    // foo
            StringUtils.defaultIfBlank("", "foo");      // foo
            StringUtils.defaultIfBlank(" ", "foo");     // foo
            </pre>


In summary, NullPointerException occurs due to the existence of null concept in Java. It is important to avoid this exception to maintain a better user experience. This is made easier by a combination of Java features well as third-party libraries and the choice of which to use depends on the requirements of an application.
