# Should we use primitive data types or Wrapper classes in Java?

This question occurred to me while I was immersed in some research on Wrapper Classes. This is one of the most fundamental topics in Core Java that I find interesting and essential to study deeply.

Wrapper classes are an integral part of Java. They are classes that encapsulate their corresponding primitive data types: **Integer** corresponds to **int** data type, **Double** corresponds to **double**, **Float** to **float**, **Boolean** to **boolean** and so on.

Wrapper classes are useful in situations where you need to work with objects. For example: collections like **Lists**, **Sets**, **Maps** can only work with objects.

**So aside from the above use case, which one should we be using? Primitive data types of Wrappers?**

To answer this question, let’s discuss the following use cases:

### Storage:
Primitive types are assigned to the actual data, which are stored in the stack memory.
Wrapper objects store references that point to the data. The references are stored in the heap memory.
```
int a = 10;

Integer obj = Integer.valueOf(20);
```

In the above example, the variable a directly holds the value **10** , while **obj** of type **Integer** holds the address of the value **20**.

### Default values:
Primitive types are assigned with default values. For example, the default value for **int** is **0**, **boolean** is **false**, **float** and **double** is **0.0**.
Wrappers are null by default since they are objects, which may cause **NullPointerException** if not handled with care.

### Efficiency:
Because primitive data types hold the actual data, they are more efficient in terms of memory usage. On the other hand, using wrappers requires additional memory overhead since they are objects and they require auto-boxing or unboxing behind the scene. Let’s look at the example below:

```
double d = 12.5; 

Double dObj = Double.valueOf(12.5);
```

In the above example, the output for **d** and **dObj** will be the same. But behind the scenes, two additional steps are executed: An instance of **Integer** is created and auto-boxing converts the **int** into **Integer**. Additionally, extra processing is required to store the created object in the heap memory.

### Features:
Wrapper classes offer additional functionalities and utility methods to work with data and perform various object-related operations. There are methods for parsing, comparison, and other data manipulation uses.

## When can we use primitive types and wrapper classes interchangeably?
There are various cases where we can switch between primitives and their counterparts thanks to autoboxing and unboxing:

In method arguments:
```java
public void printNumber(Integer a) { 
   // your code here 
}

// when invoking the method
int num = 5;
printNumber(num);    // valid statement
```

Let’s see another example:
```java
List<Double> doubleList = new ArrayList<>(); 

doubleList.add(21.01); 
doubleList.add(2.12);  

// doubleList = [21.01, 2.12]
```

With return types:
```java
public Integer printNumber(Integer a) {
   return a;
}

// when invoking the method
int num = printNumber();    // valid statement
```

When performing operations:
```java
int a = 12;
Integer b = Integer.valueOf(6);

// below statements are valid
int c = a * b;             // 72
Integer d = a + (c * b);   // 444
```

Remember to always assign a value to the wrapper class object before using it to avoid causing **NullPointerException**.

So in short, we can conclude that using primitive data types requires less memory consumption, making them much faster and more efficient compared to their Wrapper counterparts. Therefore primitives should be used unless Wrapper classes are applicable in an object-related context such as when dealing with collections.


Thanks for reading.
