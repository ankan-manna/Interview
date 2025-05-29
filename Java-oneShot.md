# Classes and Objects

## Definition:
A class is a blueprint or template for creating objects.

An object is an instance of a class that contains state (fields) and behavior (methods).

## Characteristics:
- Classes define attributes (fields) and methods.
- Objects are runtime entities that occupy memory.
- Objects can interact with each other through methods.

## Example:
```java
// Class definition
class Dog {
    // Fields (state)
    String breed;
    int age;
    String color;
    
    // Methods (behavior)
    void barking() {
        System.out.println("Woof! Woof!");
    }
    
    void hungry() {
        System.out.println("The dog is hungry");
    }
}

public class Main {
    public static void main(String[] args) {
        // Creating objects
        Dog myDog = new Dog();
        myDog.breed = "Labrador";
        myDog.age = 3;
        myDog.color = "Golden";
        
        myDog.barking();
        myDog.hungry();
    }
}
```

# 2. Constructors

## Definition:
Special methods used to initialize objects when they are created.

## Characteristics:
- Same name as the class.
- No return type.
- Can be overloaded.
- If not defined, Java provides a default constructor.

## Example:
```java
class Student {
    String name;
    int age;
    
    // Default constructor
    Student() {
        name = "Unknown";
        age = 0;
    }
    
    // Parameterized constructor
    Student(String n, int a) {
        name = n;
        age = a;
    }
    
    void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student(); // Uses default constructor
        Student s2 = new Student("Alice", 20); // Uses parameterized constructor
        
        s1.display();
        s2.display();
    }
}
```

# 3. this Keyword

## Definition:
Reference variable that refers to the current object.

## Use cases:
- Differentiate instance variables from local variables.
- Invoke current class constructor.
- Pass as argument in method/constructor call.
- Return the current class instance.

## Example:
```java
class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name; // Using 'this' to distinguish instance variable
        this.age = age;
    }
    
    void compareAge(Person p) {
        if(this.age > p.age) {
            System.out.println(this.name + " is older");
        } else {
            System.out.println(p.name + " is older");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("John", 25);
        Person p2 = new Person("Sarah", 30);
        
        p1.compareAge(p2);
    }
}
```

# 4. Inheritance (IS-A Relationship)

## Definition:
Mechanism where one class acquires properties and behaviors of another class.

## Characteristics:
- Superclass (parent) - Subclass (child) relationship.
- Supports code reusability.
- Types: Single, Multilevel, Hierarchical (Java doesn't support multiple inheritance with classes).

## Example:
```java
// Superclass
class Animal {
    void eat() {
        System.out.println("Eating...");
    }
}

// Subclass
class Dog extends Animal {
    void bark() {
        System.out.println("Barking...");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat(); // Inherited from Animal
        d.bark(); // Own method
    }
}
```

# 5. Aggregation and Composition (HAS-A Relationship)

## Aggregation:
- Weak association (independent existence).
- Example: Department and Professor (department can exist without professor).

## Composition:
- Strong association (dependent existence).
- Example: House and Room (room can't exist without house).

## Example:
```java
// Aggregation example
class Professor {
    String name;
    Professor(String name) { this.name = name; }
}

class Department {
    String name;
    Professor prof; // Aggregation
    
    Department(String name, Professor prof) {
        this.name = name;
        this.prof = prof;
    }
}

// Composition example
class Engine {
    void start() { System.out.println("Engine started"); }
}

class Car {
    private final Engine engine; // Composition
    
    Car() {
        engine = new Engine(); // Engine created when Car is created
    }
    
    void startCar() {
        engine.start();
        System.out.println("Car started");
    }
}

public class Main {
    public static void main(String[] args) {
        // Aggregation
        Professor p = new Professor("Dr. Smith");
        Department dept = new Department("Computer Science", p);
        
        // Composition
        Car myCar = new Car();
        myCar.startCar();
    }
}
```

# 6. Method Overloading & Overriding

## Method Overloading:
- Same method name, different parameters.
- Compile-time polymorphism.
- Within same class.

## Method Overriding:
- Same method signature as in parent class.
- Runtime polymorphism.
- In inheritance hierarchy.

## Example:
```java
class Calculator {
    // Method overloading
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
    
    int add(int a, int b, int c) {
        return a + b + c;
    }
}

class Animal {
    void makeSound() {
        System.out.println("Animal sound");
    }
}

class Cat extends Animal {
    // Method overriding
    @Override
    void makeSound() {
        System.out.println("Meow");
    }
}

public class Main {
    public static void main(String[] args) {
        // Overloading
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 3));
        System.out.println(calc.add(4.5, 2.3));
        System.out.println(calc.add(1, 2, 3));
        
        // Overriding
        Animal a = new Cat();
        a.makeSound(); // Calls Cat's version
    }
}
```

# 7. super Keyword

## Definition:
Reference variable used to refer immediate parent class object.

## Use cases:
- Access parent class fields.
- Call parent class methods.
- Invoke parent class constructor.

## Example:
```java
class Animal {
    String color = "white";
    
    Animal() {
        System.out.println("Animal constructor");
    }
    
    void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {
    String color = "black";
    
    Dog() {
        super(); // Calls Animal constructor
        System.out.println("Dog constructor");
    }
    
    void displayColor() {
        System.out.println("Dog color: " + color);
        System.out.println("Animal color: " + super.color);
    }
    
    void eat() {
        System.out.println("Eating dog food...");
        super.eat(); // Calls Animal's eat()
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.displayColor();
        d.eat();
    }
}
```

# 8. final, static, abstract Keywords

## final:
- Variable: constant value.
- Method: cannot be overridden.
- Class: cannot be extended.

## static:
- Belongs to class rather than instance.
- Shared among all instances.

## abstract:
- Class: cannot be instantiated.
- Method: no implementation, must be overridden.

## Example:
```java
final class FinalClass { // Cannot be extended
    final int MAX_VALUE = 100; // Constant
    
    final void display() { // Cannot be overridden
        System.out.println("This is final method");
    }
}

class StaticExample {
    static int count = 0; // Class variable
    
    StaticExample() {
        count++;
    }
    
    static void showCount() { // Class method
        System.out.println("Count: " + count);
    }
}

abstract class Shape { // Abstract class
    abstract void draw(); // Abstract method
    
    void display() {
        System.out.println("Displaying shape");
    }
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing circle");
    }
}

public class Main {
    public static void main(String[] args) {
        // final
        FinalClass f = new FinalClass();
        System.out.println(f.MAX_VALUE);
        f.display();
        
        // static
        new StaticExample();
        new StaticExample();
        StaticExample.showCount();
        
        // abstract
        Shape s = new Circle();
        s.draw();
        s.display();
    }
}
```

# 9. Polymorphism

## Compile-time Polymorphism:
- Method overloading.
- Determined at compile time.

## Runtime Polymorphism:
- Method overriding.
- Determined at runtime.

## Example:
```java
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    // Compile-time polymorphism
    static int add(int a, int b) {
        return a + b;
    }
    
    static double add(double a, double b) {
        return a + b;
    }
    
    public static void main(String[] args) {
        // Compile-time
        System.out.println(add(5, 3));
        System.out.println(add(4.5, 2.3));
        
        // Runtime
        Animal a;
        a = new Dog();
        a.sound(); // Dog's sound()
        
        a = new Cat();
        a.sound(); // Cat's sound()
    }
}
```

# 10. Encapsulation

## Definition:
Wrapping data and methods together as a single unit and restricting access to some components.

## Characteristics:
- Data hiding using private access modifier.
- Public getter/setter methods.
- Increases security and maintainability.

## Example:
```java
class Employee {
    private String name;
    private int age;
    private double salary;
    
    // Getter methods
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public double getSalary() {
        return salary;
    }
    
    // Setter methods
    public void setName(String name) {
        this.name = name;
    }
    
    public void setAge(int age) {
        if(age > 0) {
            this.age = age;
        }
    }
    
    public void setSalary(double salary) {
        if(salary > 0) {
            this.salary = salary;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee();
        emp.setName("John Doe");
        emp.setAge(30);
        emp.setSalary(50000);
        
        System.out.println("Name: " + emp.getName());
        System.out.println("Age: " + emp.getAge());
        System.out.println("Salary: " + emp.getSalary());
    }
}
```

# 11. Abstraction

## Definition:
Hiding implementation details and showing only functionality.

## Characteristics:
- Achieved through abstract classes and interfaces.
- Focuses on what an object does rather than how.
- Reduces complexity.

## Example:
```java
abstract class Vehicle {
    abstract void start(); // Abstract method
    
    void stop() { // Concrete method
        System.out.println("Vehicle stopped");
    }
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car started with key");
    }
}

class Bike extends Vehicle {
    @Override
    void start() {
        System.out.println("Bike started with kick");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle v1 = new Car();
        Vehicle v2 = new Bike();
        
        v1.start();
        v1.stop();
        
        v2.start();
        v2.stop();
    }
}
```

# 12. Interfaces

## Definition:
Blueprint of a class that contains static constants and abstract methods.

## Characteristics:
- 100% abstraction (Java 8+ allows default/static methods).
- Supports multiple inheritance.
- Used to achieve loose coupling.

## Example:
```java
interface Drawable {
    void draw(); // Abstract method
    
    default void print() { // Default method (Java 8+)
        System.out.println("Printing...");
    }
}

interface Clickable {
    void onClick();
}

class Button implements Drawable, Clickable { // Multiple inheritance
    @Override
    public void draw() {
        System.out.println("Drawing button");
    }
    
    @Override
    public void onClick() {
        System.out.println("Button clicked");
    }
}

public class Main {
    public static void main(String[] args) {
        Button btn = new Button();
        btn.draw();
        btn.onClick();
        btn.print();
    }
}
```

# 13. Packages and Access Modifiers

## Packages:
- Namespace for organizing classes.
- Prevent naming conflicts.
- Built-in (java.lang, java.util etc.) and user-defined.

## Access Modifiers:
- public: accessible everywhere.
- private: only within class.
- protected: within package and subclasses.
- default: within package only.

## Example:
```java
// File: com/example/MyClass.java
package com.example;

public class MyClass {
    public int publicVar = 1;
    protected int protectedVar = 2;
    int defaultVar = 3; // default
    private int privateVar = 4;
    
    public void display() {
        System.out.println("Public: " + publicVar);
        System.out.println("Protected: " + protectedVar);
        System.out.println("Default: " + defaultVar);
        System.out.println("Private: " + privateVar);
    }
}

// File: com/test/TestClass.java
package com.test;

import com.example.MyClass;

class SubClass extends MyClass {
    void show() {
        System.out.println("Public: " + publicVar);
        System.out.println("Protected: " + protectedVar);
        // System.out.println("Default: " + defaultVar); // Error - not accessible
        // System.out.println("Private: " + privateVar); // Error - not accessible
    }
}

public class TestClass {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        System.out.println("Public: " + obj.publicVar);
        // Other variables not accessible here
        obj.display();
    }
}
```

# 14. Exception Handling

## Definition:
Mechanism to handle runtime errors to maintain normal flow.

## Keywords:
- try: block with exception-prone code.
- catch: handles exception.
- finally: always executes.
- throw: explicitly throw exception.
- throws: declares exception.

## Example:
```java
import java.io.*;

class CustomException extends Exception {
    CustomException(String message) {
        super(message);
    }
}

public class Main {
    static void validateAge(int age) throws CustomException {
        if(age < 18) {
            throw new CustomException("Age must be 18+");
        }
        System.out.println("Valid age");
    }
    
    public static void main(String[] args) {
        // try-catch-finally
        try {
            int[] numbers = {1, 2, 3};
            System.out.println(numbers[5]); // ArrayIndexOutOfBoundsException
        } catch(ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index out of bounds");
        } finally {
            System.out.println("This always executes");
        }
        
        // Checked exception
        try {
            FileReader file = new FileReader("nonexistent.txt");
        } catch(FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
        
        // Custom exception
        try {
            validateAge(15);
        } catch(CustomException e) {
            System.out.println("Caught custom exception: " + e.getMessage());
        }
    }
}
```

# 15. Multithreading

## Definition:
Concurrent execution of two or more threads for maximum CPU utilization.

## Thread Creation:
- Extending Thread class.
- Implementing Runnable interface.

## Example:
```java
class MyThread extends Thread {
    public void run() {
        for(int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(500);
            } catch(InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}

class MyRunnable implements Runnable {
    public void run() {
        for(int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(500);
            } catch(InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // Extending Thread
        MyThread t1 = new MyThread();
        t1.setName("Thread-1");
        MyThread t2 = new MyThread();
        t2.setName("Thread-2");
        
        t1.start();
        t2.start();
        
        // Implementing Runnable
        Thread t3 = new Thread(new MyRunnable(), "Thread-3");
        Thread t4 = new Thread(new MyRunnable(), "Thread-4");
        
        t3.start();
        t4.start();
        
        // Synchronization example
        SharedResource resource = new SharedResource();
        
        Thread t5 = new Thread(() -> resource.printNumbers(5), "Thread-5");
        Thread t6 = new Thread(() -> resource.printNumbers(5), "Thread-6");
        
        t5.start();
        t6.start();
    }
}

class SharedResource {
    synchronized void printNumbers(int n) { // Synchronized method
        for(int i = 1; i <= n; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(500);
            } catch(InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}
```

# 16. Thread Lifecycle

## States:
- New: thread created but not started.
- Runnable: thread ready to run.
- Running: thread is executing.
- Blocked/Waiting: thread is inactive.
- Terminated: thread exits.

## Example:
```java
public class ThreadStates {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(() -> {
            try {
                Thread.sleep(1000);
                synchronized(ThreadStates.class) {
                    ThreadStates.class.wait(500);
                }
            } catch(InterruptedException e) {
                e.printStackTrace();
            }
        });
        
        System.out.println("State after creation: " + t.getState()); // NEW
        
        t.start();
        System.out.println("State after start: " + t.getState()); // RUNNABLE
        
        Thread.sleep(100);
        System.out.println("State during sleep: " + t.getState()); // TIMED_WAITING
        
        synchronized(ThreadStates.class) {
            Thread.sleep(1000);
            System.out.println("State during wait: " + t.getState()); // WAITING
        }
        
        t.join();
        System.out.println("State after completion: " + t.getState()); // TERMINATED
    }
}
```

# 17. Inter-thread Communication

## Methods:
- wait(): releases lock and waits.
- notify(): wakes one waiting thread.
- notifyAll(): wakes all waiting threads.

## Example:
```java
class Message {
    private String msg;
    
    public Message(String str) {
        this.msg = str;
    }
    
    public String getMsg() {
        return msg;
    }
    
    public void setMsg(String str) {
        this.msg = str;
    }
}

class Waiter implements Runnable {
    private Message msg;
    
    public Waiter(Message m) {
        this.msg = m;
    }
    
    public void run() {
        String name = Thread.currentThread().getName();
        synchronized(msg) {
            try {
                System.out.println(name + " waiting to get notified");
                msg.wait();
            } catch(InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(name + " got notified at: " + System.currentTimeMillis());
            System.out.println(name + " processed: " + msg.getMsg());
        }
    }
}

class Notifier implements Runnable {
    private Message msg;
    
    public Notifier(Message m) {
        this.msg = m;
    }
    
    public void run() {
        String name = Thread.currentThread().getName();
        System.out.println(name + " started");
        try {
            Thread.sleep(1000);
            synchronized(msg) {
                msg.setMsg(name + " Notifier work done");
                msg.notify();
                // msg.notifyAll();
            }
        } catch(InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Message msg = new Message("process it");
        
        Waiter waiter1 = new Waiter(msg);
        Thread t1 = new Thread(waiter1, "Waiter1");
        t1.start();
        
        Waiter waiter2 = new Waiter(msg);
        Thread t2 = new Thread(waiter2, "Waiter2");
        t2.start();
        
        Notifier notifier = new Notifier(msg);
        Thread t3 = new Thread(notifier, "Notifier");
        t3.start();
    }
}
```

# 18. Deadlock

## Definition:
When two or more threads are blocked forever waiting for each other.

## Example:
```java
public class DeadlockDemo {
    static final String resource1 = "Resource 1";
    static final String resource2 = "Resource 2";
    
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            synchronized(resource1) {
                System.out.println("Thread 1: locked resource 1");
                try {
                    Thread.sleep(100);
                } catch(InterruptedException e) {}
                
                synchronized(resource2) {
                    System.out.println("Thread 1: locked resource 2");
                }
            }
        });
        
        Thread t2 = new Thread(() -> {
            synchronized(resource2) {
                System.out.println("Thread 2: locked resource 2");
                try {
                    Thread.sleep(100);
                } catch(InterruptedException e) {}
                
                synchronized(resource1) {
                    System.out.println("Thread 2: locked resource 1");
                }
            }
        });
        
        t1.start();
        t2.start();
    }
}
```

# 19. Daemon Threads

## Definition:
Low priority threads that run in background to perform tasks like garbage collection.

## Characteristics:
- Doesn't prevent JVM from exiting.
- Automatically terminated when all user threads finish.
- Created using setDaemon(true) before start().

## Example:
```java
public class DaemonThreadDemo {
    public static void main(String[] args) {
        Thread userThread = new Thread(() -> {
            System.out.println("User thread started");
            try {
                Thread.sleep(2000);
            } catch(InterruptedException e) {}
            System.out.println("User thread completed");
        });
        
        Thread daemonThread = new Thread(() -> {
            while(true) {
                System.out.println("Daemon thread running");
                try {
                    Thread.sleep(500);
                } catch(InterruptedException e) {}
            }
        });
        
        daemonThread.setDaemon(true); // Must be before start()
        
        userThread.start();
        daemonThread.start();
        
        // JVM will exit after userThread completes, even if daemonThread is running
    }
}
```
# Collection & Framwork

          Iterable
              ↑
          Collection
         /    |     \
      List   Set    Queue
              |        |
           SortedSet   Deque
              |
         NavigableSet


| Interface      | Key Implementations                                                     | Characteristics            |
| -------------- | ----------------------------------------------------------------------- | -------------------------- |
| `List`         | `ArrayList`, `LinkedList`, `Vector`, `Stack`                            | Ordered, allows duplicates |
| `Set`          | `HashSet`, `LinkedHashSet`, `TreeSet`                                   | No duplicates              |
| `Queue`        | `PriorityQueue`, `ArrayDeque`, `LinkedList`                             | FIFO                       |
| `Deque`        | `ArrayDeque`, `LinkedList`                                              | Double-ended queue         |
| `Map`          | `HashMap`, `LinkedHashMap`, `TreeMap`, `Hashtable`, `ConcurrentHashMap` | Key-value pairs            |
| `SortedSet`    | `TreeSet`                                                               | Sorted, no duplicates      |
| `NavigableSet` | `TreeSet`                                                               | Sorted with navigation     |
| `SortedMap`    | `TreeMap`                                                               | Sorted by keys             |
| `NavigableMap` | `TreeMap`                                                               | Sorted with navigation     |


            Iterable<T>
                |
            Collection<T>
      ________/   |     \________
     /            |               \
List<T>         Set<T>         Queue<T>
 |               |                |
 |            SortedSet<T>      Deque<T>
 |               |
 |         NavigableSet<T>
 |
ArrayList,     HashSet,       PriorityQueue,
LinkedList,    LinkedHashSet, ArrayDeque
Vector         TreeSet

Map<K, V> (not part of Collection)
 |
 |--- SortedMap<K, V>
       |
     NavigableMap<K, V>

HashMap, TreeMap, LinkedHashMap, Hashtable


| Component | Interface  | Examples                      | Notes               |
| --------- | ---------- | ----------------------------- | ------------------- |
| List      | `List<T>`  | `ArrayList`, `LinkedList`     | Ordered, duplicates |
| Set       | `Set<T>`   | `HashSet`, `TreeSet`          | No duplicates       |
| Queue     | `Queue<T>` | `LinkedList`, `PriorityQueue` | FIFO                |
| Deque     | `Deque<T>` | `ArrayDeque`                  | Double-ended queue  |
| Map       | `Map<K,V>` | `HashMap`, `TreeMap`          | Key-value pairs     |

# ✅ What is Generics in Java?
Generics allow you to write code that works with any data type, providing type safety, code reusability, and compile-time checks.

Introduced in Java 5, Generics are widely used in the Collections Framework, custom classes, and methods.

## 🚀 Why Use Generics?
### Without Generics:

```java

List names = new ArrayList(); // raw type
names.add("Alice");
names.add(10); // Compiles, but may fail at runtime

String name = (String) names.get(1); // ClassCastException
```
### With Generics:

```java

List<String> names = new ArrayList<>();
names.add("Alice");
// names.add(10); // Compile-time error

String name = names.get(0); // Safe, no cast needed
```
## ✅ Common Use Cases of Generics in Java (with code)
### Generic Classes
```java

class Box<T> {
    private T value;
    
    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}

// Usage
Box<Integer> intBox = new Box<>();
intBox.set(123);

Box<String> strBox = new Box<>();
strBox.set("Hello");
```
### Generic Methods
```java

class Utils {
    public static <T> void printArray(T[] array) {
        for (T item : array) {
            System.out.println(item);
        }
    }
}

// Usage
String[] names = {"Alice", "Bob"};
Integer[] nums = {1, 2, 3};

Utils.printArray(names);
Utils.printArray(nums);
```
### Bounded Type Parameters
```java

class MathUtils {
    public static <T extends Number> double square(T num) {
        return num.doubleValue() * num.doubleValue();
    }
}

// Usage
double result = MathUtils.square(5);        // int
double result2 = MathUtils.square(3.14);    // double
```
### Multiple Type Parameters
```java

class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() { return key; }
    public V getValue() { return value; }
}

// Usage
Pair<String, Integer> entry = new Pair<>("Age", 30);
```
## Wildcards in Generics
### Unbounded Wildcard: <?>
```java

public static void printList(List<?> list) {
    for (Object item : list) {
        System.out.println(item);
    }
}
```
### Upper Bounded Wildcard: <? extends Number>
```java

public static double sum(List<? extends Number> list) {
    double total = 0;
    for (Number n : list) {
        total += n.doubleValue();
    }
    return total;
}
```
### Lower Bounded Wildcard: <? super Integer>
```java

public static void addNumbers(List<? super Integer> list) {
    list.add(10); // OK
    list.add(20); // OK
}
```
### Generic Interface
```java

interface Transformer<T> {
    T transform(T input);
}

class UpperCaseTransformer implements Transformer<String> {
    public String transform(String input) {
        return input.toUpperCase();
    }
}
```

| Concept              | Syntax                  | Use Case                       |
| -------------------- | ----------------------- | ------------------------------ |
| Generic Class        | `class Box<T> {}`       | Container-type data structures |
| Generic Method       | `<T> T method(T input)` | Reusable utility methods       |
| Bounded Type         | `<T extends Number>`    | Limit generic types            |
| Multiple Type Params | `<K, V>`                | Key-value pairs, tuples        |
| Wildcards            | `<?>`, `<? extends T>`  | Flexible input types           |
