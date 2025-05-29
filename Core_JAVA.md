# Core Java Topics - Fundamentals of Java

## 1. Basics of Java

### History and Features of Java
**Definition:**  
Java is a high-level, class-based, object-oriented programming language designed to have as few implementation dependencies as possible. It was developed by James Gosling at Sun Microsystems and released in 1995. Java enables developers to write code once and run it anywhere, thanks to its platform independence. It is widely used for building enterprise-scale applications, mobile applications (especially Android), web applications, and more.

**Characteristics:**  
- **Platform Independent:** Java programs are compiled into bytecode, which can run on any device equipped with a Java Virtual Machine (JVM). This "write once, run anywhere" capability makes Java highly portable across different operating systems and hardware architectures.  
- **Object-Oriented:** Supports core principles such as encapsulation, inheritance, and polymorphism, enabling modular, reusable, and maintainable code.  
- **Robust:** Provides strong memory management through automatic garbage collection, exception handling mechanisms, and strict compile-time and runtime type checking to minimize errors and enhance reliability.  
- **Secure:** Offers a secure execution environment through runtime checking, bytecode verification, sandboxing, and security APIs, making it suitable for networked and distributed environments.  
- **Multithreaded:** Supports concurrent execution of multiple threads, allowing efficient use of CPU resources and enabling the development of responsive and high-performance applications.  
- **High Performance:** Utilizes Just-In-Time (JIT) compiler to convert bytecode into native machine code at runtime, improving execution speed significantly compared to interpreted languages.  
- **Distributed:** Includes networking capabilities and APIs to support distributed computing, enabling applications to communicate over networks seamlessly.

**Example:**  
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### JVM, JRE, and JDK
**Definition:**  
- **JVM (Java Virtual Machine):** An abstract computing machine that enables a computer to run Java programs by converting compiled Java bytecode into machine-specific code. It provides platform independence by abstracting the underlying hardware and operating system.  
- **JRE (Java Runtime Environment):** A package that includes the JVM and the standard Java class libraries required to run Java applications. It does not include development tools.  
- **JDK (Java Development Kit):** A full-featured software development kit that includes the JRE, JVM, and development tools such as the Java compiler (`javac`), debugger, and other utilities necessary for Java application development.

**Characteristics:**  
- JVM is platform-dependent, meaning there are different JVM implementations for different operating systems, but it executes platform-independent Java bytecode.  
- JRE is required to run Java programs but does not provide tools for development.  
- JDK is required for Java development and includes tools for compiling, debugging, and monitoring Java applications.

### Data Types and Variables
**Definition:**  
Java supports two main categories of data types: primitive data types and reference types. Variables are named storage locations in memory used to hold data values of a specific type.

**Characteristics:**  
- **Primitive types:** Include `byte`, `short`, `int`, `long` for integer values; `float`, `double` for floating-point numbers; `char` for single characters; and `boolean` for true/false values. These types store actual values and have fixed sizes.  
- **Reference types:** Include objects and arrays, which store references (memory addresses) to the actual data. Reference types support methods and can be null.  
- Variables must be declared with a specific type before use, and Java is statically typed, meaning type checking is done at compile time.

**Example:**  
```java
int age = 25;
double price = 19.99;
char grade = 'A';
boolean isJavaFun = true;
String name = "Java";
```

### Operators and Expressions
**Definition:**  
Operators are special symbols or keywords that perform operations on variables and values. Expressions are combinations of variables, operators, and method calls that evaluate to a single value.

**Characteristics:**  
- **Arithmetic operators:** Perform mathematical calculations such as addition (`+`), subtraction (`-`), multiplication (`*`), division (`/`), and modulus (`%`).  
- **Relational operators:** Compare two values and return a boolean result, including greater than (`>`), less than (`<`), greater than or equal to (`>=`), less than or equal to (`<=`), equal to (`==`), and not equal to (`!=`).  
- **Logical operators:** Combine boolean expressions using AND (`&&`), OR (`||`), and NOT (`!`).  
- **Assignment operators:** Assign values to variables, including simple assignment (`=`) and compound assignments like `+=`, `-=`, `*=`, `/=` which combine arithmetic and assignment.

**Example:**  
```java
int a = 10, b = 20;
int sum = a + b;
boolean isGreater = a > b;
boolean result = (a > 5) && (b < 30);
```

### Control Statements
**Definition:**  
Control statements manage the flow of execution in a program by making decisions, repeating actions, or transferring control.

**Characteristics:**  
- **Conditional statements:** Include `if`, `if-else`, and `switch` statements to execute code blocks based on boolean conditions.  
- **Looping statements:** Include `for`, `while`, and `do-while` loops to repeat code blocks multiple times.  
- **Control transfer statements:** Include `break` to exit loops or switch cases, `continue` to skip the current iteration, and `return` to exit from a method.

**Example:**  
```java
if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}

for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

## 2. Object-Oriented Programming (OOP)
- ***OOPS stands for Object-Oriented Programming System. It's a programming paradigm that organizes software design around objects, which encapsulate both data and the code that operates on that data.***
- **Modularity**: Code is divided into classes, making it easier to maintain.

- **Reusability**: Inheritance lets you reuse logic across multiple classes.

- **Scalability**: Easy to scale applications by adding new classes.

- **Maintainability**: Encapsulation and abstraction help isolate bugs and updates.

Real-world Mapping: Maps real-world entities (like User, Car, BankAccount) easily.
### Classes and Objects
**Definition:**  
- **Class:** A blueprint or template for creating objects, defining properties (fields) and behaviors (methods) that the objects will have.  
- **Object:** An instance of a class that contains state (data stored in fields) and behavior (functions or methods).

**Characteristics:**  
- Classes encapsulate data and methods, promoting modularity and code reuse.  
- Objects are created at runtime and occupy memory.  
- Supports encapsulation by bundling data and methods together, hiding internal details from outside access.

**Example:**  
```java
// Class definition
class Car {
    // Fields (state)
    String color;
    int maxSpeed;
    
    // Method (behavior)
    void drive() {
        System.out.println("Car is driving at max speed of " + maxSpeed);
    }
}

public class Main {
    public static void main(String[] args) {
        // Creating an object
        Car myCar = new Car();
        myCar.color = "Red";
        myCar.maxSpeed = 180;
        myCar.drive(); // Output: Car is driving at max speed of 180
    }
}
```

### Constructors
**Definition:**  
Special methods used to initialize new objects when they are created. They set initial values for object fields.

**Characteristics:**  
- Have the same name as the class.  
- Do not have a return type, not even `void`.  
- Can be overloaded to provide multiple ways to initialize objects with different parameters.  
- If no constructor is defined, Java provides a default no-argument constructor.

**Example:**  
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
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student(); // Uses default constructor
        Student s2 = new Student("Alice", 20); // Uses parameterized constructor
    }
}
```

### this Keyword
**Definition:**  
A reference variable that refers to the current object within an instance method or constructor.

**Characteristics:**  
- Used to differentiate instance variables from local variables or parameters with the same name.  
- Can be used to call one constructor from another within the same class (constructor chaining).  
- Can be passed as an argument to methods or returned from methods.

**Example:**  
```java
class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name; // this refers to current object's name
        this.age = age;
    }
    
    void display() {
        System.out.println("Name: " + this.name + ", Age: " + this.age);
    }
}
```

### Inheritance (IS-A)
**Definition:**  
A mechanism where one class (subclass or child class) inherits properties and behaviors (fields and methods) from another class (superclass or parent class).

**Characteristics:**  
- Uses the `extends` keyword to establish inheritance.  
- Supports code reusability by allowing subclasses to reuse code from superclasses.  
- Java supports single inheritance, meaning a class can extend only one class.  
- Forms a hierarchy representing "is-a" relationships.

**Example:**  
```java
class Animal { // Superclass
    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal { // Subclass
    void bark() {
        System.out.println("Dog is barking");
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

### Aggregation and Composition (HAS-A)
**Definition:**  
- **Aggregation:** A weak "has-a" relationship where the child object can exist independently of the parent.  
- **Composition:** A strong "has-a" relationship where the child object cannot exist without the parent.

**Characteristics:**  
- Aggregation represents a "whole-part" relationship where parts can exist independently.  
- Composition represents a lifecycle dependency where the part's lifecycle is bound to the whole.  
- Both are implemented using instance variables referencing other objects.

**Example:**  
```java
// Aggregation example
class Address {
    String city, state;
    Address(String city, String state) {
        this.city = city;
        this.state = state;
    }
}

class Employee {
    Address address; // Employee HAS-A Address (aggregation)
    String name;
    
    Employee(String name, Address address) {
        this.name = name;
        this.address = address;
    }
}

// Composition example
class Engine {
    void start() {
        System.out.println("Engine started");
    }
}

class Car {
    private final Engine engine; // Car HAS-A Engine (composition)
    
    Car() {
        engine = new Engine(); // Engine created when Car is created
    }
    
    void startCar() {
        engine.start();
    }
}
```

### Method Overloading & Overriding
**Method Overloading:**  
- Defining multiple methods with the same name but different parameter lists within the same class.  
- Enables compile-time polymorphism (static binding).  
- Improves code readability by using the same method name for similar actions with different inputs.

**Method Overriding:**  
- Defining a method in a subclass with the same signature (name and parameters) as a method in the superclass.  
- Enables runtime polymorphism (dynamic binding).  
- Allows a subclass to provide a specific implementation of a method already defined in its superclass.

**Example:**  
```java
class Calculator {
    // Method overloading
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
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
```

### super Keyword
**Definition:**  
Used to refer to the immediate parent class object.

**Characteristics:**  
- Access parent class fields and methods that are hidden by subclass members.  
- Call parent class constructors from subclass constructors.  
- Must be the first statement in a constructor if used.

**Example:**  
```java
class Vehicle {
    int speed = 50;
    
    Vehicle() {
        System.out.println("Vehicle constructor");
    }
}

class Bike extends Vehicle {
    int speed = 100;
    
    Bike() {
        super(); // Calls Vehicle constructor
        System.out.println("Bike constructor");
    }
    
    void display() {
        System.out.println(super.speed); // 50 (parent class speed)
        System.out.println(speed); // 100 (current class speed)
    }
}
```

### final, static, abstract Keywords
- **final:**  
  - Variable: Declares a constant whose value cannot be changed once initialized.  
  - Method: Prevents method overriding in subclasses.  
  - Class: Prevents the class from being subclassed.

- **static:**  
  - Belongs to the class rather than any instance.  
  - Shared among all instances of the class.  
  - Can be used for variables, methods, blocks, and nested classes.

- **abstract:**  
  - Class: Cannot be instantiated directly and may contain abstract methods.  
  - Method: Declared without implementation and must be overridden in subclasses.

**Example:**  
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

abstract class AbstractClass {
    abstract void abstractMethod(); // No implementation
    
    void concreteMethod() {
        System.out.println("This is concrete method");
    }
}
```

### Polymorphism (Compile-time & Runtime)
**Definition:**  
The ability of an object to take many forms, allowing methods to behave differently based on the object invoking them.

- **Compile-time (Method Overloading):**  
  Determined at compile time based on method signatures and parameter types.

- **Runtime (Method Overriding):**  
  Determined at runtime based on the actual object type, enabling dynamic method dispatch.

**Example:**  
```java
// Compile-time polymorphism
class MathOperations {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

// Runtime polymorphism
class Animal {
    void sound() { System.out.println("Animal sound"); }
}

class Dog extends Animal {
    @Override
    void sound() { System.out.println("Bark"); }
}

public class Main {
    public static void main(String[] args) {
        // Runtime polymorphism
        Animal myAnimal = new Dog(); // Upcasting
        myAnimal.sound(); // Output: Bark (depends on runtime object)
    }
}
```

### Encapsulation
**Definition:**  
The process of wrapping data (variables) and code (methods) together as a single unit, restricting direct access to some of the object's components.

**Characteristics:**  
- Achieved using access modifiers like `private` to hide data.  
- Provides public getter and setter methods to access and update private data safely.  
- Enhances security, maintainability, and flexibility of code.

**Example:**  
```java
class BankAccount {
    private double balance; // Private field
    
    // Public getter
    public double getBalance() {
        return balance;
    }
    
    // Public setter with validation
    public void deposit(double amount) {
        if(amount > 0) {
            balance += amount;
        }
    }
}
```

### Abstraction
**Definition:**  
The concept of hiding complex implementation details and showing only the essential features of an object.

**Characteristics:**  
- Achieved through abstract classes and interfaces.  
- Focuses on "what" an object does rather than "how" it does it.  
- Helps reduce complexity and increase reusability.

**Example:**  
```java
abstract class Shape {
    abstract void draw(); // Abstract method (no implementation)
    
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
```

### Interfaces
**Definition:**  
A reference type in Java, similar to a class, that can contain only constants, method signatures, default methods, static methods, and nested types. Interfaces specify what a class must do, but not how.

**Characteristics:**  
- All methods are implicitly `public` and abstract (except default and static methods).  
- All fields are implicitly `public`, `static`, and `final`.  
- A class can implement multiple interfaces, supporting multiple inheritance of type.  
- Java 8 introduced default and static methods in interfaces.

**Example:**  
```java
interface Drawable {
    void draw(); // Abstract method
    
    default void print() { // Default method (Java 8+)
        System.out.println("Printing...");
    }
}

class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing rectangle");
    }
}

public class Main {
    public static void main(String[] args) {
        Drawable d = new Rectangle();
        d.draw();
        d.print();
    }
}
```

## 3. Packages and Access Modifiers

### Built-in Packages
Java provides several built-in packages that contain useful classes and interfaces:

- `java.lang` (automatically imported): Fundamental classes such as `String`, `Math`, `System`.  
- `java.util`: Utility classes including collections framework, date/time API, and more.  
- `java.io`: Input/output classes for reading and writing data.  
- `java.net`: Networking classes for communication over networks.  
- `java.sql`: Classes for database access and manipulation.

### import Statement
**Example:**  
```java
import java.util.ArrayList; // Import a single class
import java.util.*; // Import all classes from a package
```

### Creating Custom Packages
**Example:**  
```java
// File: com/example/MyClass.java
package com.example; // Package declaration

public class MyClass {
    public void display() {
        System.out.println("Inside my package");
    }
}

// In another file
import com.example.MyClass;

public class Main {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.display();
    }
}
```

### Access Modifiers
Access modifiers control the visibility and accessibility of classes, methods, and variables:

- **public:** Accessible from any other class.  
- **private:** Accessible only within the same class.  
- **protected:** Accessible within the same package and subclasses.  
- **default (no modifier):** Accessible only within the same package.

**Example:**  
```java
package com.example;

public class AccessExample {
    public int publicVar = 1;
    protected int protectedVar = 2;
    int defaultVar = 3; // default access
    private int privateVar = 4;
    
    public void show() {
        System.out.println(privateVar); // Accessible within class
    }
}
```

## 4. Exception Handling

### try, catch, throw, throws, finally
**Example:**  
```java
public class ExceptionHandling {
    static void validate(int age) throws ArithmeticException { // throws declares exception
        if(age < 18) {
            throw new ArithmeticException("Not eligible"); // throw an exception
        }
    }
    
    public static void main(String[] args) {
        try {
            validate(15);
        } 
        catch(ArithmeticException e) { // catch exception
            System.out.println("Exception: " + e.getMessage());
        } 
        finally { // always executes
            System.out.println("This always executes");
        }
    }
}
```

### Checked vs Unchecked Exceptions
- **Checked Exceptions:**  
  - Checked at compile-time.  
  - Must be either caught or declared in the method signature.  
  - Examples: `IOException`, `SQLException`.

- **Unchecked Exceptions:**  
  - Checked at runtime.  
  - Not required to be caught or declared.  
  - Examples: `NullPointerException`, `ArrayIndexOutOfBoundsException`.

### Custom Exceptions
**Example:**  
```java
class InvalidAgeException extends Exception {
    InvalidAgeException(String message) {
        super(message);
    }
}

public class Main {
    static void validate(int age) throws InvalidAgeException {
        if(age < 18) {
            throw new InvalidAgeException("Age must be 18+");
        }
    }
    
    public static void main(String[] args) {
        try {
            validate(15);
        } catch(InvalidAgeException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

## 5. String Handling

### String, StringBuilder, StringBuffer
- **String:** Immutable sequence of characters. Once created, its value cannot be changed.  
- **StringBuilder:** Mutable sequence of characters, not synchronized, faster for single-threaded use.  
- **StringBuffer:** Mutable sequence of characters, synchronized, thread-safe but slower.

**Example:**  
```java
public class StringExample {
    public static void main(String[] args) {
        String str = "Hello";
        str.concat(" World"); // New string created, original unchanged
        
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World"); // Original modified
        
        StringBuffer sbf = new StringBuffer("Hello");
        sbf.append(" World"); // Original modified
        
        System.out.println(str); // Hello
        System.out.println(sb); // Hello World
        System.out.println(sbf); // Hello World
    }
}
```

### Common String Methods
```java
String s = "Java Programming";
s.length(); // 16
s.charAt(2); // 'v'
s.substring(5); // "Programming"
s.substring(5, 9); // "Prog"
s.indexOf('P'); // 5
s.toUpperCase(); // "JAVA PROGRAMMING"
s.toLowerCase(); // "java programming"
s.trim(); // removes leading and trailing whitespace
s.replace('a', 'x'); // "Jxvx Progrxmming"
s.split(" "); // ["Java", "Programming"]
```

### String Pool and Interning
Java maintains a pool of string literals to optimize memory usage.

**Example:**  
```java
String s1 = "Java"; // String literal in pool
String s2 = "Java"; // Reuses from pool
String s3 = new String("Java"); // New object in heap

System.out.println(s1 == s2); // true (same reference)
System.out.println(s1 == s3); // false (different references)
System.out.println(s1.equals(s3)); // true (same content)

String s4 = s3.intern(); // Returns pooled version
System.out.println(s1 == s4); // true
```

## 6. Arrays and Multidimensional Arrays

### One-dimensional and Two-dimensional Arrays
**Example:**  
```java
// 1D array
int[] numbers = new int[3];
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;

// Shorthand initialization
int[] nums = {10, 20, 30};

// 2D array
int[][] matrix = new int[2][3];
matrix[0][0] = 1;
matrix[0][1] = 2;

// Shorthand
int[][] mat = {{1,2,3}, {4,5,6}};
```

### Array Class and Utility Methods
```java
import java.util.Arrays;

int[] arr = {5, 2, 8, 1};

Arrays.sort(arr); // [1, 2, 5, 8]
int index = Arrays.binarySearch(arr, 5); // 2
int[] copy = Arrays.copyOf(arr, 3); // [1, 2, 5]
boolean equal = Arrays.equals(arr, copy); // false
Arrays.fill(arr, 10); // [10, 10, 10, 10]
String str = Arrays.toString(arr); // "[10, 10, 10, 10]"
```

## 7. Wrapper Classes

### Autoboxing and Unboxing
- **Autoboxing:** Automatic conversion of primitive types to their corresponding wrapper classes.  
- **Unboxing:** Automatic conversion of wrapper class objects back to primitive types.

**Example:**  
```java
// Autoboxing
Integer num = 10; // int to Integer
Double d = 3.14; // double to Double

// Unboxing
int n = num; // Integer to int
double val = d; // Double to double

// Collections require wrapper classes
List<Integer> numbers = new ArrayList<>();
numbers.add(5); // Autoboxing
int x = numbers.get(0); // Unboxing
```

## 8. Java I/O Streams

### FileInputStream/FileOutputStream
**Example:**  
```java
import java.io.*;

public class FileIO {
    public static void main(String[] args) {
        // Writing to file
        try(FileOutputStream fos = new FileOutputStream("test.txt")) {
            String str = "Hello File IO";
            fos.write(str.getBytes());
        } catch(IOException e) {
            e.printStackTrace();
        }
        
        // Reading from file
        try(FileInputStream fis = new FileInputStream("test.txt")) {
            int content;
            while((content = fis.read()) != -1) {
                System.out.print((char)content);
            }
        } catch(IOException e) {
            e.printStackTrace();
        }
    }
}
```

### BufferedReader/BufferedWriter
**Example:**  
```java
import java.io.*;

public class BufferedIO {
    public static void main(String[] args) {
        // Writing
        try(BufferedWriter bw = new BufferedWriter(new FileWriter("buffered.txt"))) {
            bw.write("First line");
            bw.newLine();
            bw.write("Second line");
        } catch(IOException e) {
            e.printStackTrace();
        }
        
        // Reading
        try(BufferedReader br = new BufferedReader(new FileReader("buffered.txt"))) {
            String line;
            while((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch(IOException e) {
            e.printStackTrace();
        }
    }
}
```

### ObjectInputStream/ObjectOutputStream
**Example:**  
```java
import java.io.*;

class Person implements Serializable {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class ObjectIO {
    public static void main(String[] args) {
        // Serialization
        try(ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"))) {
            Person p = new Person("Alice", 25);
            oos.writeObject(p);
        } catch(IOException e) {
            e.printStackTrace();
        }
        
        // Deserialization
        try(ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {
            Person p = (Person)ois.readObject();
            System.out.println(p.name + " " + p.age);
        } catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 9. Multithreading

### Creating Threads (Thread, Runnable)
**Example:**  
```java
// Extending Thread class
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}

// Implementing Runnable
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable is running");
    }
}

public class ThreadDemo {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();
        
        Thread t2 = new Thread(new MyRunnable());
        t2.start();
        
        // Using lambda
        Thread t3 = new Thread(() -> System.out.println("Lambda thread"));
        t3.start();
    }
}
```

### Thread Lifecycle
- **New:** Thread is created but not started.  
- **Runnable:** Thread is ready to run and waiting for CPU time.  
- **Running:** Thread is executing.  
- **Blocked/Waiting:** Thread is waiting for a resource or condition.  
- **Terminated:** Thread has completed execution.

### Synchronization
**Example:**  
```java
class Counter {
    private int count = 0;
    
    public synchronized void increment() { // Synchronized method
        count++;
    }
    
    public void decrement() {
        synchronized(this) { // Synchronized block
            count--;
        }
    }
    
    public int getCount() {
        return count;
    }
}

public class SyncDemo {
    public static void main(String[] args) throws InterruptedException {
        Counter c = new Counter();
        
        Thread t1 = new Thread(() -> {
            for(int i=0; i<1000; i++) c.increment();
        });
        
        Thread t2 = new Thread(() -> {
            for(int i=0; i<1000; i++) c.decrement();
        });
        
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        
        System.out.println("Final count: " + c.getCount()); // Should be 0
    }
}
```

### Inter-thread Communication
**Example:**  
```java
class Shared {
    synchronized void method1() {
        System.out.println("Method1 started");
        try {
            wait(); // Releases lock and waits
        } catch(InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Method1 resumed");
    }
    
    synchronized void method2() {
        System.out.println("Method2 started");
        notify(); // Wakes up one waiting thread
        // notifyAll() wakes up all waiting threads
        System.out.println("Method2 completed");
    }
}

public class WaitNotifyDemo {
    public static void main(String[] args) {
        Shared s = new Shared();
        
        new Thread(() -> s.method1()).start();
        new Thread(() -> s.method2()).start();
    }
}
```

### Deadlock
**Example:**  
```java
class Resource {
    synchronized void method1(Resource r2) {
        System.out.println("Method1 started");
        try { Thread.sleep(100); } catch(Exception e) {}
        r2.method2();
    }
    
    synchronized void method2() {
        System.out.println("Method2 started");
    }
}

public class DeadlockDemo {
    public static void main(String[] args) {
        final Resource r1 = new Resource();
        final Resource r2 = new Resource();
        
        new Thread(() -> r1.method1(r2)).start();
        new Thread(() -> r2.method1(r1)).start();
    }
}
```

### Daemon Threads
**Example:**  
```java
public class DaemonDemo {
    public static void main(String[] args) {
        Thread daemon = new Thread(() -> {
            while(true) {
                System.out.println("Daemon working...");
                try { Thread.sleep(500); } catch(Exception e) {}
            }
        });
        
        daemon.setDaemon(true); // Must be before start()
        daemon.start();
        
        System.out.println("Main thread ending");
        // JVM exits when only daemon threads remain
    }
}
```

## 10. Collections Framework

### List, Set, Map Interfaces
- **List:** Ordered collection that allows duplicates.  
- **Set:** Collection that does not allow duplicates.  
- **Map:** Collection of key-value pairs.

### ArrayList, LinkedList, HashSet, TreeSet
**Example:**  
```java
import java.util.*;

public class CollectionsDemo {
    public static void main(String[] args) {
        // List examples
        List<String> arrayList = new ArrayList<>();
        arrayList.add("Apple");
        arrayList.add("Banana");
        arrayList.add(1, "Orange"); // Insert at index 1
        
        List<String> linkedList = new LinkedList<>();
        linkedList.addAll(arrayList);
        
        // Set examples
        Set<String> hashSet = new HashSet<>();
        hashSet.add("Apple");
        hashSet.add("Apple"); // Duplicate ignored
        hashSet.add("Banana");
        
        Set<String> treeSet = new TreeSet<>();
        treeSet.addAll(hashSet); // Sorted order
    }
}
```

### HashMap, TreeMap, LinkedHashMap
**Example:**  
```java
import java.util.*;

public class MapDemo {
    public static void main(String[] args) {
        // HashMap - no order
        Map<Integer, String> hashMap = new HashMap<>();
        hashMap.put(3, "Three");
        hashMap.put(1, "One");
        hashMap.put(2, "Two");
        
        // TreeMap - sorted by keys
        Map<Integer, String> treeMap = new TreeMap<>();
        treeMap.putAll(hashMap);
        
        // LinkedHashMap - insertion order
        Map<Integer, String> linkedHashMap = new LinkedHashMap<>();
        linkedHashMap.put(3, "Three");
        linkedHashMap.put(1, "One");
        linkedHashMap.put(2, "Two");
    }
}
```

### Iterator and ListIterator
**Example:**  
```java
import java.util.*;

public class IteratorDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("A"); list.add("B"); list.add("C");
        
        // Iterator - forward only
        Iterator<String> it = list.iterator();
        while(it.hasNext()) {
            System.out.println(it.next());
        }
        
        // ListIterator - bidirectional
        ListIterator<String> lit = list.listIterator();
        while(lit.hasNext()) {
            System.out.println("Next: " + lit.next());
        }
        while(lit.hasPrevious()) {
            System.out.println("Previous: " + lit.previous());
        }
    }
}
```

### Comparable and Comparator
**Example:**  
```java
import java.util.*;

class Person implements Comparable<Person> {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public int compareTo(Person p) {
        return this.name.compareTo(p.name); // Natural ordering by name
    }
}

class AgeComparator implements Comparator<Person> {
    @Override
    public int compare(Person p1, Person p2) {
        return p1.age - p2.age; // Order by age
    }
}

public class ComparisonDemo {
    public static void main(String[] args) {
        List<Person> people = new ArrayList<>();
        people.add(new Person("Bob", 30));
        people.add(new Person("Alice", 25));
        
        Collections.sort(people); // Uses Comparable
        Collections.sort(people, new AgeComparator()); // Uses Comparator
    }
}
```

## 11. Generics

### Generic Classes and Methods
**Example:**  
```java
// Generic class
class Box<T> {
    private T content;
    
    void setContent(T content) {
        this.content = content;
    }
    
    T getContent() {
        return content;
    }
}

// Generic method
class Util {
    public static <T> void printArray(T[] array) {
        for(T item : array) {
            System.out.println(item);
        }
    }
}

public class GenericsDemo {
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.setContent("Hello Generics");
        System.out.println(stringBox.getContent());
        
        Integer[] nums = {1, 2, 3};
        Util.printArray(nums);
    }
}
```

### Bounded Type Parameters
**Example:**  
```java
class NumericBox<T extends Number> { // T must be Number or subclass
    private T number;
    
    NumericBox(T number) {
        this.number = number;
    }
    
    double square() {
        return number.doubleValue() * number.doubleValue();
    }
}

public class BoundedDemo {
    public static void main(String[] args) {
        NumericBox<Integer> intBox = new NumericBox<>(5);
        System.out.println(intBox.square()); // 25.0
        
        // NumericBox<String> strBox; // Compile error - String not Number
    }
}
```

### Wildcards
**Example:**  
```java
import java.util.List;

class WildcardDemo {
    // Upper bounded wildcard (accepts List of Number or any subclass)
    static double sumOfList(List<? extends Number> list) {
        double sum = 0.0;
        for(Number num : list) {
            sum += num.doubleValue();
        }
        return sum;
    }
}
```