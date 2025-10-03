# Difference between A Setter Method and Constructor When Setting a Variable’s Value

Java provides different ways to set a value of an instance variable of a class. Among them are two common approaches: using the constructor and using the setter method. In this article we’re going to address the difference between both.

## Setting a Value Using the Setter Method
Setter methods are widely used in Java applications along with the getter methods to work with instance variables of classes. They provide a way to safely modify the values of private variables after creating an instance of a class:

```java
  public class Item {
    private String category;
  
    public void setCategory(String newCategory) {
      this.category = newCategory;
    }
    
    public String getCategory() {
      return category;
    }
  }
```

Here we created a class called Item with one member variable category and a setter method setCategory which accepts an argument newCategory.This method is used to update the value of original category. Let’s call this method to further illustrate this:

```java
  public static void main(String[] args) {
      Item item = new Item();
      item.setCategory("electronics");
  }
```

As you can see, we called the setter method and passed a String. Now if we call the getter to retrieve the variable, the output should give us electronics .

```java
    String category = item.getCategory();
    System.out.println(category);
```

## Setting a Value Using A Constructor
Constructors are a special type of methods used to initialize objects. They’re called when we create objects of a class. Another use of constructors is to set initial values of instance variables:

```java
    public class User {
      private Long id;
      private String name;
      private String password;
    
      public User(Long id, String name, String password) {
        this.id = id;
        this.name = name;
        this.password = password;
      }
    }
```

In the above example, we created the class User with a set of private variables and a parameterized constructor. What this constructor does is initialize the id, name and password of the User. Using this constructor when we create a user object, we ensure that the initial values of id, name and password are set at the time of the object creation:

```java
public static void main(String[] args) {
    User user = new User(1L, "user1", "user_password");
}
```

In this case, if we retrieve any of the instance variables, we should expect the same data we passed inside the constructor.

## Setters Vs. Constructors
Here are some of the key points for both the setter and constructor that should be considered when contemplating which of the two to use:

**Setter:**

- Use this when the value of a variable may change over time.
- Use this when you want to add additional validation before setting the value

```java
  public void setPrice(double price) {
    if(price > 0.0) {
        this.price = price;
    } else {
        throw new IllegalArgumentException("Price cannot be negative");
    }
  }
```

- Setter methods cannot set the value of a final variable.

**Constructor:**

- Use this when you want to set initial values when you create an object.
- It allows you to declare final variables, so they’re useful when you want to ensure they cannot be changed after initialization.

## Conclusion

We’ve discussed the use of setters and constructors in setting values of instance variables. Understanding the difference between setter methods and constructors is essential to making informed decisions on when to use them.

Thanks for reading!