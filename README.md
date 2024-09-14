
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
