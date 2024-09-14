
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
