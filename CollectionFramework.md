### **Java Collection Framework - Detailed Notes**

The Java Collection Framework provides a set of interfaces and classes to handle groups of objects as a single unit (collections). This framework is found in the `java.util` package and is a fundamental aspect of the Java programming language, offering essential data structures and algorithms.

---

## **1. Overview of Collection Framework**

### **1.1 Key Interfaces in Collection Framework**

1. **Collection Interface**:  
   - The root interface in the collection hierarchy.
   - Defines the most common methods such as `add()`, `remove()`, `size()`, and `iterator()`.
   
2. **List Interface**:  
   - Extends `Collection`. Represents an ordered collection (also known as a sequence). Allows duplicates.
   - Classes implementing `List`: `ArrayList`, `LinkedList`, `Vector`, `Stack`.
   
3. **Set Interface**:  
   - Extends `Collection`. Represents a collection that cannot contain duplicate elements.
   - Classes implementing `Set`: `HashSet`, `LinkedHashSet`, `TreeSet`.
   
4. **Queue Interface**:  
   - Extends `Collection`. Represents a collection designed for holding elements prior to processing. Typically follows the FIFO order (First-In-First-Out).
   - Classes implementing `Queue`: `PriorityQueue`, `LinkedList` (acts as both List and Queue).
   
5. **Map Interface**:  
   - Represents a collection of key-value pairs. Maps cannot contain duplicate keys; each key maps to exactly one value.
   - Classes implementing `Map`: `HashMap`, `LinkedHashMap`, `TreeMap`, `Hashtable`.

---

## **2. List Interface and Its Implementations**

### **2.1 ArrayList**
- **Characteristics**:
  - A **resizable array** implementation of the `List` interface.
  - Provides fast random access (O(1) complexity for retrieving elements).
  - Slower when inserting/removing elements, especially in the middle of the list (O(n) complexity).
- **Use Case**:  
  When frequent reads are needed, but inserts and deletions are rare.
  
- **Example**:
```java
List<String> arrayList = new ArrayList<>();
arrayList.add("Apple");
arrayList.add("Banana");
arrayList.remove("Apple");
```

### **2.2 LinkedList**
- **Characteristics**:
  - A **doubly linked list** implementation of the `List` and `Deque` interfaces.
  - Efficient for insertions and deletions (O(1) for head/tail operations).
  - Slower for random access compared to `ArrayList` (O(n)).
- **Use Case**:  
  When frequent insertions and deletions at both ends are needed.

- **Example**:
```java
List<String> linkedList = new LinkedList<>();
linkedList.add("Car");
linkedList.addFirst("Bike");
linkedList.removeLast();
```

### **2.3 Vector**
- **Characteristics**:
  - Similar to `ArrayList`, but synchronized (thread-safe).
  - Slower than `ArrayList` due to overhead in synchronization.
- **Use Case**:  
  When a thread-safe dynamic array is required.

- **Example**:
```java
Vector<Integer> vector = new Vector<>();
vector.add(1);
vector.add(2);
vector.remove(1);
```

### **2.4 Stack**
- **Characteristics**:
  - Extends `Vector` and implements LIFO (Last-In-First-Out) principle.
- **Use Case**:  
  For scenarios like reversing a word, backtracking, etc.
  
- **Example**:
```java
Stack<String> stack = new Stack<>();
stack.push("A");
stack.push("B");
stack.pop();  // Removes "B"
```

---

## **3. Set Interface and Its Implementations**

### **3.1 HashSet**
- **Characteristics**:
  - Implements the `Set` interface and uses a **hash table** for storing elements.
  - **No ordering** of elements.
  - **No duplicates allowed**.
  - O(1) time complexity for basic operations like add, remove, and contains.
- **Use Case**:  
  When unique elements are required and ordering is not important.
  
- **Example**:
```java
Set<String> hashSet = new HashSet<>();
hashSet.add("One");
hashSet.add("Two");
hashSet.add("One");  // Will not add a duplicate
```

### **3.2 LinkedHashSet**
- **Characteristics**:
  - Extends `HashSet` and maintains a **linked list of entries**.
  - Preserves insertion order.
- **Use Case**:  
  When unique elements are required with predictable iteration order.
  
- **Example**:
```java
Set<String> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add("A");
linkedHashSet.add("B");
```

### **3.3 TreeSet**
- **Characteristics**:
  - Implements the `NavigableSet` interface, which extends `SortedSet`.
  - Stores elements in **ascending order** (natural ordering).
  - Uses a **Red-Black tree** for storage (balanced tree).
  - Time complexity for operations: O(log n).
- **Use Case**:  
  When sorted elements are required.
  
- **Example**:
```java
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(10);
treeSet.add(5);
treeSet.add(20);  // Output: [5, 10, 20] (sorted order)
```

---

## **4. Queue Interface and Its Implementations**

### **4.1 PriorityQueue**
- **Characteristics**:
  - Implements the `Queue` interface.
  - Elements are ordered by their **natural ordering** or by a `Comparator` provided at queue construction time.
  - Does not allow null elements.
- **Use Case**:  
  When priority-based processing is needed, e.g., in scheduling tasks.
  
- **Example**:
```java
Queue<Integer> priorityQueue = new PriorityQueue<>();
priorityQueue.add(15);
priorityQueue.add(10);
priorityQueue.add(25);  // Output: [10, 15, 25] (natural ordering)
```

### **4.2 LinkedList (as Queue)**
- **Characteristics**:
  - Implements both `List` and `Queue`.
  - Supports **FIFO** behavior when used as a queue.
- **Use Case**:  
  Simple queue with dequeuing at the front and enqueuing at the rear.
  
- **Example**:
```java
Queue<String> linkedListQueue = new LinkedList<>();
linkedListQueue.offer("A");
linkedListQueue.offer("B");
linkedListQueue.poll();  // Removes "A"
```

---

## **5. Map Interface and Its Implementations**

### **5.1 HashMap**
- **Characteristics**:
  - Implements the `Map` interface, storing data as key-value pairs.
  - **No ordering** of keys.
  - Allows null keys and values.
  - Time complexity: O(1) for basic operations (on average).
- **Use Case**:  
  General-purpose map with fast retrieval and insertion.
  
- **Example**:
```java
Map<Integer, String> hashMap = new HashMap<>();
hashMap.put(1, "One");
hashMap.put(2, "Two");
```

### **5.2 LinkedHashMap**
- **Characteristics**:
  - Extends `HashMap` and maintains a **doubly linked list** of its entries.
  - Preserves **insertion order**.
- **Use Case**:  
  When predictable iteration order is required.
  
- **Example**:
```java
Map<Integer, String> linkedHashMap = new LinkedHashMap<>();
linkedHashMap.put(1, "One");
linkedHashMap.put(2, "Two");  // Output: [1=One, 2=Two] (preserves insertion order)
```

### **5.3 TreeMap**
- **Characteristics**:
  - Implements the `NavigableMap` interface, storing entries in **sorted order** by keys.
  - Uses a **Red-Black tree** internally.
  - Time complexity: O(log n).
- **Use Case**:  
  When sorted mapping by keys is required.
  
- **Example**:
```java
Map<Integer, String> treeMap = new TreeMap<>();
treeMap.put(3, "Three");
treeMap.put(1, "One");
treeMap.put(2, "Two");  // Output: [1=One, 2=Two, 3=Three] (sorted by keys)
```

---

## **6. Important Collection Framework Methods**

### **6.1 Common Methods for Collection**
1. `add(E e)`: Adds the specified element to the collection.
2. `remove(Object o)`: Removes the specified element.
3. `clear()`: Removes all elements.
4. `contains(Object o)`: Returns `true` if the collection contains the element.
5. `size()`: Returns the number of elements.
6. `iterator()`: Returns an iterator to traverse the collection.

### **6.2 Common Methods for Map**
1. `put(K key, V value)`: Adds a key-value pair to the map.
2. `get(Object key)`: Retrieves the value associated with the key.
3. `remove(Object key)`: Removes the key-value pair.
4. `keySet()`: Returns a set of all keys.
5. `values()`: Returns a collection of all values.

---

## **7. Differences Between Important Collections**

### **7.1 ArrayList vs LinkedList**
- **Array

List**: Better for random access, slow for insertions/deletions.
- **LinkedList**: Efficient for insertions/deletions, slower for random access.

### **7.2 HashSet vs TreeSet**
- **HashSet**: No ordering of elements, fast lookups (O(1)).
- **TreeSet**: Elements sorted, slower operations (O(log n)).

### **7.3 HashMap vs TreeMap**
- **HashMap**: No ordering of keys, faster (O(1)).
- **TreeMap**: Sorted by keys, slower (O(log n)).

---

### **8. Conclusion**
The Java Collection Framework is a comprehensive toolset for managing data collections efficiently. Choosing the correct implementation depends on the use case, performance requirements, and whether order or uniqueness is important.
