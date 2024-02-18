# Why is 1 == 1 is true but 1000 == 1000 is false When dealing with Wrapper Classes in Java?

That’s a loaded title.

In this article, we’re going to discuss a behavior that occurs when we use the ‘==’ operator to compare Wrapper classes.

Wrapper classes are used to wrap the corresponding primitive data types so they can be used as objects in a context that requires only objects like collections (Lists, Sets and Maps). For example, the Integer class corresponds to int data type, Double corresponds to double and so on.

For the purpose of this article, we’re only going to work with the Integer class.

Let’s look at the example below:

```
Integer a = Integer.valueOf(10);
Integer b = 10;
```

This is a simple example. We created two Integer objects: one using the valueOf() method provided by the Integer class and the other using autoboxing feature.

```System.out.println((a == b));          // true
System.out.println(a.equals(b));       // true
```

In the code above, we compared between the two objects using both the ‘==’ operator and equals() method. The output in both cases is true.

However, things take a different turn when we use a different value:
```
Integer a = Integer.valueOf(350);
Integer b = 350;

```System.out.println((a == b));          // false
System.out.println(a.equals(b));       // true
```

**Why is the output different?**
First of all, the ‘==’ operator checks for reference equality, while the equals() method compares the actual values.

The reason for the difference in output is that the JVM uses a caching mechanism referred to as ‘Integer cache’ to improve performance and reduce memory consumption.

**How does this Integer cache work?**
The caching range is set between -128 to 127. When you call the Integer.valueOf() method the first time, it caches the value only if it is within the range and any subsequent calls will return the cached Integer rather than creating a new one. Meaning both references will point to the same object, which is why the comparison returns true.

This is why the comparison of Integer 10 returns true while that of a value not within the range returns false.

Integer Cache mechanism only works with auto-boxing or the Integer.valueOf()method. It is not applicable when creating a wrapper object using the constructor:

```
Integer a = new Integer(12);
Integer b = new Integer(12);

System.out.println((a == b));          // false
System.out.println(a.equals(b));       // true
```

As you can see, the first comparison will always return false regardless of the value.

That’s it for this article. Thanks for reading.
