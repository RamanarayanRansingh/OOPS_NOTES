
### **Classes and Objects in Java**

- **Class**: A class is a template or blueprint for an object. It defines a new data type that can be used to create objects.
- **Object**: An object is an instance of a class and represents physical reality (occupies space in memory).
  
#### **Key Properties of Objects**
1. **State**: Represents the data (attributes) of the object.
2. **Identity**: Uniquely distinguishes one object from another (usually where it's stored in memory).
3. **Behavior**: Describes what operations (methods) can be performed on the object.

---

### **Declaration and Instantiation**

- **Declaration**:  
  ```java
  Box mybox; // Declare reference to object
  ```
  Here, `mybox` is a reference to an object of type `Box`. It does not yet refer to an actual object.
  
- **Instantiation**:  
  ```java
  mybox = new Box(); // Allocate a Box object
  ```
  This line allocates memory for a `Box` object using the `new` keyword and assigns a reference to `mybox`.

#### **Memory Allocation with `new`**
- The **new** keyword allocates memory dynamically (at runtime) for an object and returns a reference to it.
- The reference is stored in a variable (in this case, `mybox`), which holds the memory address of the object.
  
  ```java
  classname class-var = new classname();
  ```
  - **class-var**: A variable of the class type being created.
  - **classname()**: Constructor of the class, invoked when an object is instantiated.

---

### **Primitive Types vs Objects**
- **Primitive Types**: Such as `int` and `char` are not objects in Java. They are implemented as normal variables for efficiency and do not require `new` for instantiation.
  
---

### **Object References and Assignment**

- Example:
  ```java
  Box b1 = new Box();
  Box b2 = b1;
  ```
  - **b1** and **b2** both refer to the **same object**. No new memory is allocated for `b2`, and changes made through `b2` will affect the object referred to by `b1`.

---

### **Method Parameters**
- **Parameter**: A variable defined in a method that receives a value during method invocation.
  
  Example:
  ```java
  int square(int i) {
      return i * i;
  }
  ```
  - **i** is a parameter in the `square(int i)` method.

- **Argument**: The actual value passed when invoking the method. In `square(100)`, `100` is the argument.

---

### **Note on Object Creation**
- When creating an object:
  ```java
  Bus bus = new Bus();
  ```
  - **LHS (Left-hand side)**: `bus` (the reference) is checked by the **compiler**.
  - **RHS (Right-hand side)**: `new Bus()` (the object creation) is handled by the **JVM**.

--- 

This structure captures the essential concepts of classes, objects, memory allocation, and method parameters in Java.

---

### **The `this` Keyword**

- **Definition**: 
  - The `this` keyword is used within a method or constructor to refer to the current object, i.e., the object on which the method or constructor was invoked.

  - Example:
    ```java
    class Box {
        int width, height;

        Box(int width, int height) {
            this.width = width;  // Refers to the instance variable
            this.height = height; // Refers to the instance variable
        }

        void displayDimensions() {
            System.out.println("Width: " + this.width + ", Height: " + this.height);
        }
    }
    ```

---

### **The `final` Keyword**

- **Purpose**: 
  - Used to declare constants in Java. A field declared as `final` cannot be modified after it is initialized.

- **Usage Example**:
  ```java
  final int FILE_OPEN = 2;  // Constant field with all uppercase naming convention
  ```

- **Immutability for Primitive vs Reference Types**:
  - For **primitive types**: The value cannot be changed once initialized.
  - For **reference types**: The reference to the object cannot be changed, but the object’s internal state can still be modified.

  - Example for reference type:
    ```java
    final Box box = new Box(5, 10);  // The reference 'box' cannot point to another Box
    box.width = 20;  // But you can modify the internal state of the Box object
    ```

---

### **The `finalize()` Method**

- **Purpose**: 
  - The `finalize()` method is used to perform cleanup actions before an object is reclaimed by the garbage collector.

- **Example**:
  ```java
  protected void finalize() {
      System.out.println("Object is being garbage collected");
  }
  ```

- **Note**: This method is rarely used in modern Java programs due to improvements in garbage collection and better alternatives for resource management like `try-with-resources`.

---

### **Constructors in Java**

- **Definition**: 
  - A **constructor** is a special method that is automatically called when an object is created. It has no return type and is used to initialize objects.

- **Example**:
  ```java
  class Box {
      int width, height;

      // Constructor
      Box() {
          width = 10;
          height = 20;
          System.out.println("Box Constructor Called");
      }
  }

  public class Main {
      public static void main(String[] args) {
          Box mybox = new Box();  // Calls the Box() constructor
      }
  }
  ```

---

### **Inheritance and Constructors in Java**

- **Key Points**:
  - In Java, the constructor of a base class (superclass) is automatically called when an object of the derived class (subclass) is created.
  - If the base class has no argument constructor, it gets invoked by default.
  - If the base class has a **parameterized constructor**, the derived class must explicitly call it.

- **Example**:

  ```java
  class Base {
      Base() {
          System.out.println("Base Class Constructor Called");
      }
  }

  class Derived extends Base {
      Derived() {
          // Automatically calls the Base() constructor
          System.out.println("Derived Class Constructor Called");
      }
  }

  public class Main {
      public static void main(String[] args) {
          Derived d = new Derived();  // Creates an instance of Derived, calls both constructors
      }
  }
  ```

  **Output**:
  ```
  Base Class Constructor Called
  Derived Class Constructor Called
  ```

- **Parameterized Constructor in Base Class**:

  ```java
  class Base {
      int value;

      // Parameterized constructor
      Base(int value) {
          this.value = value;
          System.out.println("Base Class Constructor Called with value: " + value);
      }
  }

  class Derived extends Base {
      // Must explicitly call the Base class parameterized constructor
      Derived(int value) {
          super(value);  // Call to Base class constructor
          System.out.println("Derived Class Constructor Called");
      }
  }

  public class Main {
      public static void main(String[] args) {
          Derived d = new Derived(100);  // Calls parameterized constructor of Base
      }
  }
  ```

  **Output**:
  ```
  Base Class Constructor Called with value: 100
  Derived Class Constructor Called
  ```

---

This structure provides a comprehensive overview of the `this`, `final`, `finalize()` methods, and the role of constructors and inheritance in Java with code examples to clarify the concepts.

Here's a detailed and structured note on Java packages, including examples and important details:

---

### **Java Packages**

- **Definition**:
  - Packages are containers for classes that help in compartmentalizing the class namespace. They prevent name collisions and organize related classes into hierarchical structures.

- **Purpose**:
  - **Naming**: Avoids naming conflicts by allowing multiple classes with the same name in different packages.
  - **Visibility Control**: Determines which classes and members are accessible from other classes.

- **Creating a Package**:
  - To create a package, include the `package` statement at the beginning of your Java source file.

  ```java
  package MyPackage; // Declares that the class belongs to MyPackage
  ```

- **File System Structure**:
  - Java uses directories to represent packages. The directory structure must mirror the package hierarchy.
  - For example, a class in the `java.awt.image` package must be stored in `java/awt/image` directory.

- **Directory Naming**:
  - The directory name must exactly match the package name, including case sensitivity.

- **Finding Packages**:
  - **Default Behavior**: The Java runtime system starts searching for packages in the current working directory.
  - **Classpath**: You can specify additional directories or JAR files using the `CLASSPATH` environment variable.
  - **Command Line**: Use the `-classpath` (or `-cp`) option with `java` and `javac` commands to specify paths to your classes.

- **Importing Packages**:
  - When importing a package, only the public members of the classes within that package are accessible. Non-public members are not accessible outside their package.

  - **Example**:
    ```java
    // In MyPackage/Person.java
    package MyPackage;

    public class Person {
        public String name;
        private int age;

        public Person(String name, int age) {
            this.name = name;
            this.age = age;
        }

        public void display() {
            System.out.println("Name: " + name + ", Age: " + age);
        }
    }
    ```

    ```java
    // In another package or directory
    import MyPackage.Person;

    public class TestPerson {
        public static void main(String[] args) {
            Person p = new Person("Alice", 30);
            p.display();  // Accessible as display() is public
            // p.age; // Not accessible, as age is private
        }
    }
    ```

- **Classpath Example**:
  - **Setting CLASSPATH** (environment variable): Add the directory where your `.class` files are located.

  - **Using Command Line**:
    ```bash
    javac -classpath /path/to/classes MyPackage/Person.java
    java -classpath /path/to/classes TestPerson
    ```

---

This note captures the essential aspects of Java packages, including their purpose, file system structure, and how to manage and import them, along with practical examples.


Here's a detailed and well-organized note on the `static` keyword in Java, including explanations and code examples:

---

### **Understanding `static` in Java**

- **Definition**:
  - The `static` keyword in Java is used for creating class-level methods and variables. Static members belong to the class rather than to instances of the class.

- **Characteristics of Static Members**:
  - **Access**: Static members can be accessed before any objects of the class are created and without reference to any specific object.
  - **Static Methods**:
    - Belong to the class, not to any instance.
    - Can only access other static methods and static variables directly.
    - Cannot access instance variables or methods.
    - Cannot use `this` or `super` keywords.
    - Can be accessed using the class name directly.

- **Example of Static Methods**:

  ```java
  public class Human {
      String message = "Hello World";

      public static void display(Human human) {
          System.out.println(human.message); // Accessing non-static variable through object reference
      }

      public static void main(String[] args) {
          Human kunal = new Human();
          kunal.message = "Kunal's message";
          Human.display(kunal);
      }
  }
  ```

- **Static Variables**:
  - Shared among all instances of a class.
  - Initialized when the class is first loaded.

- **Static Blocks**:
  - Used for static initialization. Executes once when the class is first loaded.

  ```java
  class UseStatic {
      static int a = 3;
      static int b;

      static void meth(int x) {
          System.out.println("x = " + x);
          System.out.println("a = " + a);
          System.out.println("b = " + b);
      }

      static {
          System.out.println("Static block initialized.");
          b = a * 4;
      }

      public static void main(String args[]) {
          meth(42);
      }
  }
  ```

  - **Output**:
    ```
    Static block initialized.
    x = 42
    a = 3
    b = 12
    ```

- **Static Inner Classes**:
  - Only nested classes can be static.
  - Static nested classes do not have access to instance variables of the outer class.

  ```java
  public class Static {
      static class Test {
          String name;

          public Test(String name) {
              this.name = name;
          }
      }

      public static void main(String[] args) {
          Test a = new Test("Kunal");
          Test b = new Test("Rahul");

          System.out.println(a.name); // Kunal
          System.out.println(b.name); // Rahul
      }
  }
  ```

- **Key Points**:
  - Static methods cannot be overridden because method resolution is done at compile-time for static methods.
  - Static interface methods are not inherited by implementing classes or sub-interfaces.
  - Static inner classes are not associated with an instance of the outer class and do not have access to its instance members.

- **Note on Static Classes**:
  - Only nested classes can be static. Static nested classes can have static variables and methods.

  ```java
  public class StaticDemo {
      // Static inner class
      static class InnerStatic {
          static int staticVar = 10;

          static void staticMethod() {
              System.out.println("Static Method in InnerStatic");
          }
      }

      public static void main(String[] args) {
          InnerStatic.staticMethod(); // Access static method directly
          System.out.println("Static Variable: " + InnerStatic.staticVar); // Access static variable directly
      }
  }
  ```

---

This note provides a comprehensive overview of static members in Java, including how they function, examples, and specific rules regarding their usage.


### **Singleton Design Pattern in Java**

The Singleton design pattern ensures that a class has only one instance and provides a global point of access to that instance. Here's a detailed breakdown of how the Singleton pattern is implemented in Java, using the provided code as an example:

---

#### **Singleton Class Implementation**

```java
package com.kunal.singleton;

import com.kunal.access.A;

public class Singleton {
    // Private constructor to prevent instantiation from outside
    private Singleton() {
    }

    // Private static variable to hold the single instance
    private static Singleton instance;

    // Public static method to provide access to the instance
    public static Singleton getInstance() {
        // Create the instance only if it does not exist
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

#### **Key Components**

1. **Private Constructor**:
   - The constructor `private Singleton()` ensures that the class cannot be instantiated from outside. This is crucial for maintaining a single instance of the class.

2. **Private Static Variable**:
   - `private static Singleton instance;` is a static variable that holds the single instance of the class. This variable is private to prevent direct access from outside the class.

3. **Public Static Method**:
   - `public static Singleton getInstance()` is a static method that provides the global access point to the single instance of the class. 
   - Inside this method, a check is performed to see if the instance is `null`. If it is `null`, a new instance is created and assigned to the `instance` variable.
   - If the instance already exists, the existing instance is returned.

#### **Usage**

- **Accessing the Singleton Instance**:
  - To get the single instance of the `Singleton` class, you call `Singleton.getInstance()`.
  - This method ensures that only one instance of the class is created and reused throughout the application.

#### **Advantages**

- **Controlled Access**: Ensures controlled access to the single instance of the class.
- **Reduced Memory Usage**: Since only one instance is created, it helps in reducing memory consumption.
- **Global Access Point**: Provides a global point of access to the instance.

#### **Considerations**

- **Thread Safety**: The given implementation is not thread-safe. In a multi-threaded environment, multiple threads might simultaneously pass the `null` check and create multiple instances. To make it thread-safe, consider using synchronization or the double-checked locking principle.

  ```java
  public static Singleton getInstance() {
      if (instance == null) {
          synchronized (Singleton.class) {
              if (instance == null) {
                  instance = new Singleton();
              }
          }
      }
      return instance;
  }
  ```

- **Lazy Initialization**: The instance is created only when `getInstance()` is called for the first time, which is known as lazy initialization.

#### **Real-World Example**

- **Configuration Manager**: Often used in applications where a single configuration manager is needed to handle configuration settings.

#### **Note**

- **Package Import**: The `import com.kunal.access.A;` statement indicates that this class might be using or extending functionality from another class or package. Ensure that `A` is appropriately defined if needed.

---

This note provides a clear explanation of the Singleton design pattern and how it is implemented in Java, along with the provided code example.


### **Inheritance in Java**

Inheritance is a fundamental concept in Java that allows one class to inherit the properties and behaviors (fields and methods) of another class. Here's a breakdown of key concepts related to inheritance, including the use of `extends`, `super`, and `final`.

---

#### **Basic Inheritance Syntax**
In Java, inheritance is achieved using the `extends` keyword:

```java
class Subclass extends Superclass {
    // body of class
}
```

- **Subclass**: The class that inherits from another class.
- **Superclass**: The class being inherited from.
- A subclass can inherit only one superclass (Java does not support multiple inheritance directly).

#### **Superclasses and Subclass Access**
- While a subclass inherits all the fields and methods of a superclass, it **cannot access private members** of the superclass directly.
- **Superclass Reference to Subclass Object**: You can assign a subclass object to a superclass reference, but the reference can only access methods and fields defined in the superclass.

  ```java
  Superclass ref = new Subclass(); // ref can only access superclass methods.
  ```

#### **Using `super` Keyword**

`super` is used to:
1. Call the **superclass constructor**.
2. Access a **superclass method** or field that is hidden by the subclass.

- **Calling a Superclass Constructor**: If a subclass needs to initialize fields from the superclass, it can call the superclass constructor using `super`.

  ```java
  class BoxWeight extends Box {
      double weight;

      BoxWeight(double w, double h, double d, double m) {
          super(w, h, d); // Call superclass constructor
          weight = m;
      }
  }
  ```

- **Accessing Superclass Methods or Fields**: When a subclass hides a superclass member with the same name, you can use `super` to refer to the superclass version.

  ```java
  super.member; // Access the superclass method or field.
  ```

#### **Multilevel Hierarchy**
In a multilevel class hierarchy, `super()` always refers to the constructor of the immediate superclass. Each constructor in the chain must call the constructor of its superclass.

```java
class Box {
    private double width, height, depth;

    Box(double w, double h, double d) {
        width = w;
        height = h;
        depth = d;
    }
}

class BoxWeight extends Box {
    double weight;

    BoxWeight(double w, double h, double d, double m) {
        super(w, h, d); // Call Box constructor
        weight = m;
    }
}
```

#### **Key Points About `super()`**
- **super()** must be the first statement in the subclass constructor if used.
- If a superclass constructor requires parameters, the subclass must pass them via `super()`.

#### **`final` Keyword**

The `final` keyword can be used with methods and classes to prevent further inheritance or modification.

1. **Prevent Overriding**: Marking a method as `final` prevents subclasses from overriding it.

   ```java
   final void show() {
       // cannot be overridden
   }
   ```

2. **Prevent Inheritance**: Marking a class as `final` prevents it from being extended.

   ```java
   final class MyClass {
       // no other class can extend MyClass
   }
   ```

3. **Performance**: Declaring methods as `final` allows for **early binding** (method calls resolved at compile time), improving performance through inlining.

4. **Note on Static Methods**: Static methods are class-level and are not subject to overriding. Thus, polymorphism does not apply to static methods.

#### **Important Notes**

- **Polymorphism**: In Java, polymorphism applies to methods, not fields. Thus, instance variables are not subject to polymorphism.
- **Default Constructor**: If `super()` is not used, the default or parameterless constructor of each superclass is called automatically.

#### **Example**

```java
class Box {
    private double width, height, depth;

    Box(Box ob) { // Constructor with object parameter
        width = ob.width;
        height = ob.height;
        depth = ob.depth;
    }
}

class BoxWeight extends Box {
    double weight;

    BoxWeight(BoxWeight ob) {
        super(ob); // Call superclass constructor
        weight = ob.weight;
    }
}
```

In the above code, `super(ob)` calls the `Box` constructor, passing a `BoxWeight` object, which invokes the constructor of the superclass.

---

By understanding these core concepts, you can effectively utilize inheritance, `super`, and `final` in Java to build efficient and scalable object-oriented programs.


### **Method Overloading in Java**

Method overloading allows multiple methods in the same class to have the same name but different parameter lists. Here's a detailed explanation:

---

#### **Key Concepts of Method Overloading**:
1. **Same Method Name, Different Parameters**: You can define multiple methods with the same name in a class as long as their parameters (number, types, or order) differ.
   
2. **Different Return Types**: While overloaded methods can have different return types, the return type alone does not distinguish overloaded methods.

3. **Method Resolution**: When a method is called, Java determines which method to invoke based on the argument list provided. It selects the best match according to the method's parameter types.

4. **Automatic Type Conversion**: If no exact match is found, Java will attempt to convert the arguments using its automatic type conversion rules (e.g., `int` to `double`).

---

#### **Example: Automatic Type Conversion in Overloading**

In this example, the method `test(double)` is invoked even though `test(int)` is not defined. This happens because Java automatically converts the `int` argument to `double`.

```java
class OverloadDemo {
    void test(double a) {
        System.out.println("Inside test(double) a: " + a);
    }
}

class Overload {
    public static void main(String args[]) {
        OverloadDemo ob = new OverloadDemo();
        int i = 88;

        // Automatic type conversion from int to double
        ob.test(i);        // Calls test(double) with i converted to double
        ob.test(123.2);    // Calls test(double) with a double argument
    }
}
```

**Explanation**:
- The `test(int)` method is not defined in `OverloadDemo`.
- When `ob.test(i)` is called with an `int` argument, Java automatically converts `i` to a `double` and calls `test(double)`.

---

### **Returning Objects from Methods**

In Java, a method can return an object. This is useful when you want a method to return complex data or objects with multiple fields.

---

#### **Key Concepts of Returning Objects**:
1. **Returning Object References**: When a method returns an object, it returns a reference to the object created within the method.
   
2. **Dynamic Object Allocation**: Since objects are dynamically allocated using `new`, they remain in memory as long as there are references to them, even after the method terminates.

3. **Garbage Collection**: Once there are no references to an object, it becomes eligible for garbage collection, meaning the memory is freed.

---

#### **Example: Method Returning an Object**

In the following example, the `incrByTen()` method returns a new `Test` object with its `a` field incremented by 10:

```java
class Test {
    int a;

    // Constructor to initialize the 'a' field
    Test(int i) {
        a = i;
    }

    // Method that creates and returns a new object with 'a' incremented by 10
    Test incrByTen() {
        Test temp = new Test(a + 10);
        return temp;  // Return the new object
    }
}

class RetOb {
    public static void main(String args[]) {
        Test ob1 = new Test(2);  // Create a new object with 'a' initialized to 2
        Test ob2;

        // Call incrByTen() which returns a new Test object
        ob2 = ob1.incrByTen();

        System.out.println("ob1.a: " + ob1.a);  // Output: 2
        System.out.println("ob2.a: " + ob2.a);  // Output: 12
    }
}
```

**Explanation**:
- **Object Creation**: The `incrByTen()` method creates a new `Test` object with `a` incremented by 10.
- **Returning the Object**: The method returns the reference to the newly created object. This reference is assigned to `ob2`.
- **Output**:
  - `ob1.a` remains 2 because `ob1` is unchanged.
  - `ob2.a` becomes 12 as it references the new object with `a` incremented.

---

### **Key Points**:
- **Automatic Type Conversion**: If no exact match is found during method overloading, Java attempts to convert the argument type (e.g., `int` to `double`).
- **Returning Objects**: When an object is returned from a method, it continues to exist as long as there is a reference to it, even after the method terminates.
- **Garbage Collection**: When no references to an object remain, it is eligible for garbage collection, and its memory is freed.

These concepts are crucial for writing efficient, flexible, and reusable code in Java.
