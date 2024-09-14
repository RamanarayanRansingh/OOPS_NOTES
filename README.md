
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
