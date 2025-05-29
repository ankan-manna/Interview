# Advanced C++ Topics

## 1. File Handling

### Definition:
File handling is a fundamental concept in C++ programming that allows programs to read data from and write data to files stored on a storage device such as a hard drive or SSD. It enables persistent data storage beyond the runtime of the program.

### Characteristics:
- Uses `ifstream` for input file operations (reading from files).  
- Uses `ofstream` for output file operations (writing to files).  
- Uses `fstream` for both input and output operations.  
- Supports both text and binary file modes.  
- Provides mechanisms for error handling during file operations.  
- Supports sequential and random access to files.

### Example Code:
```cpp
#include <iostream>
#include <fstream>

int main() {
    // Writing to a file
    std::ofstream outFile("data.txt");
    if (!outFile) {
        std::cerr << "Error opening file for writing." << std::endl;
        return 1;
    }
    outFile << "Hello, File Handling!" << std::endl;
    outFile.close();

    // Reading from a file
    std::ifstream inFile("data.txt");
    if (!inFile) {
        std::cerr << "Error opening file for reading." << std::endl;
        return 1;
    }
    std::string line;
    while (getline(inFile, line)) {
        std::cout << line << std::endl;
    }
    inFile.close();

    // Binary file operations
    struct Data { int x; double y; };
    Data d = {10, 3.14};

    std::ofstream binFile("data.bin", std::ios::binary);
    if (!binFile) {
        std::cerr << "Error opening binary file for writing." << std::endl;
        return 1;
    }
    binFile.write(reinterpret_cast<char*>(&d), sizeof(d));
    binFile.close();

    return 0;
}
```

## 2. Templates (Generic Programming)

### Definition:
Templates in C++ allow writing generic and reusable code that can work with any data type. They enable the creation of functions and classes that operate with generic types, promoting code reuse and type safety.

### Characteristics:
- Enable code reusability by allowing functions and classes to work with any data type.  
- Support compile-time polymorphism through template instantiation.  
- Can be specialized for specific data types to provide custom behavior.  
- Support both function templates and class templates.  
- Help reduce code duplication.

### Example Code:
```cpp
// Function template
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

// Class template
template <class T>
class Stack {
private:
    std::vector<T> elements;
public:
    void push(T const& elem) {
        elements.push_back(elem);
    }
    T pop() {
        if (elements.empty()) {
            throw std::out_of_range("Stack<>::pop(): empty stack");
        }
        T elem = elements.back();
        elements.pop_back();
        return elem;
    }
};

// Template specialization
template <>
class Stack<std::string> {
    // Special implementation for strings
};
```

## 3. Exception Handling

### Definition:
Exception handling is a mechanism to handle runtime errors and abnormal conditions in a controlled manner, allowing the program to continue or terminate gracefully.

### Characteristics:
- The `try` block contains code that might throw exceptions.  
- `catch` blocks handle specific exceptions thrown in the try block.  
- `throw` is used to raise an exception explicitly.  
- Supports exception hierarchies and polymorphic exception handling.  
- Allows resource cleanup using `finally`-like behavior with destructors or RAII.

### Example Code:
```cpp
#include <iostream>
#include <exception>

class MyException : public std::exception {
public:
    const char* what() const noexcept override {
        return "My custom exception";
    }
};

void riskyFunction(int value) {
    if (value < 0) {
        throw MyException();
    }
    if (value == 0) {
        throw std::runtime_error("Value cannot be zero");
    }
}

int main() {
    try {
        riskyFunction(-5);
    } catch (const MyException& e) {
        std::cerr << "Caught MyException: " << e.what() << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Caught standard exception: " << e.what() << std::endl;
    }
    return 0;
}
```

## 4. Standard Template Library (STL)

### Definition:
The Standard Template Library (STL) is a powerful set of C++ template classes that provide common data structures and algorithms.

### Characteristics:
- Includes container classes such as sequence containers, associative containers, and container adapters.  
- Provides iterator abstractions for traversing containers.  
- Offers a rich set of algorithms that work across containers.  
- Supports function objects (functors) for custom operations.  
- Highly optimized and widely used in C++ programming.

### Example Code:
```cpp
#include <vector>
#include <algorithm>
#include <map>
#include <set>
#include <iostream>

// Sequence containers
std::vector<int> vec = {5, 3, 1, 4, 2};
std::sort(vec.begin(), vec.end());

// Associative containers
std::map<std::string, int> population = {
    {"Tokyo", 37400068},
    {"Delhi", 28514000}
};
population["Shanghai"] = 25582000;

// Set operations
std::set<int> s = {3, 1, 4, 1, 5, 9};
if (s.find(4) != s.end()) {
    std::cout << "4 is in the set" << std::endl;
}

// Algorithms
auto it = std::find(vec.begin(), vec.end(), 3);
if (it != vec.end()) {
    std::cout << "Found 3 at position " << (it - vec.begin()) << std::endl;
}

// Utility
auto pair = std::make_pair("Alice", 25);
std::tuple<int, double, std::string> t(1, 2.3, "four");
```

## 5. Lambda Expressions

### Definition:
Lambda expressions are anonymous function objects that can be defined inline, providing a concise way to write small function objects.

### Characteristics:
- Provide a concise syntax for defining small functions.  
- Can capture variables from the enclosing scope by value or reference.  
- Often used with STL algorithms for custom behavior.  
- Support type inference with `auto`.  
- Can be mutable to modify captured variables.

### Example Code:
```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5};

    // Simple lambda
    auto print = [](int n) { std::cout << n << " "; };
    std::for_each(nums.begin(), nums.end(), print);
    std::cout << std::endl;

    // Lambda with capture
    int threshold = 3;
    auto count = std::count_if(nums.begin(), nums.end(), 
        [threshold](int n) { return n > threshold; });
    std::cout << "Count greater than " << threshold << ": " << count << std::endl;

    // Mutable lambda (can modify captured variables)
    int sum = 0;
    std::for_each(nums.begin(), nums.end(), 
        [&sum](int n) { sum += n; });
    std::cout << "Sum: " << sum << std::endl;

    // Generic lambda (C++14)
    auto genericAdd = [](auto a, auto b) { return a + b; };
    std::cout << "Generic add: " << genericAdd(3, 4) << std::endl;

    return 0;
}
```

## 6. Smart Pointers (C++11)

### Definition:
Smart pointers are automatically managed pointers that handle object lifetime and help prevent memory leaks.

### Characteristics:
- `unique_ptr`: Exclusive ownership, non-copyable.  
- `shared_ptr`: Shared ownership with reference counting.  
- `weak_ptr`: Non-owning observer of `shared_ptr`.  
- Help manage dynamic memory safely and efficiently.

### Example Code:
```cpp
#include <memory>
#include <iostream>

int main() {
    // Unique pointer
    std::unique_ptr<int> uptr(new int(10));
    // std::unique_ptr<int> uptr2 = uptr; // Error - can't copy

    // Shared pointer
    std::shared_ptr<int> sptr1 = std::make_shared<int>(20);
    {
        std::shared_ptr<int> sptr2 = sptr1; // OK - shared ownership
        std::cout << *sptr2 << std::endl;
    } // sptr2 destroyed, but object lives on

    // Weak pointer
    std::weak_ptr<int> wptr = sptr1;
    if (auto temp = wptr.lock()) {
        std::cout << "Value: " << *temp << std::endl;
    }

    return 0;
}
```

## 7. Multithreading (C++11 and beyond)

### Definition:
Multithreading allows concurrent execution of multiple threads within a program, improving performance and responsiveness.

### Characteristics:
- Uses `std::thread` for thread management.  
- Provides mutexes (`std::mutex`) for synchronization.  
- Supports atomic operations for thread-safe variables.  
- Condition variables for thread communication.  
- Helps avoid race conditions and deadlocks with proper synchronization.

### Example Code:
```cpp
#include <thread>
#include <mutex>
#include <atomic>
#include <iostream>
#include <chrono>

std::mutex mtx;
std::atomic<int> counter(0);

void increment(int id) {
    for (int i = 0; i < 5; ++i) {
        {
            std::lock_guard<std::mutex> lock(mtx);
            std::cout << "Thread " << id << " incrementing" << std::endl;
        }
        ++counter;
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
}

int main() {
    std::thread t1(increment, 1);
    std::thread t2(increment, 2);
    t1.join();
    t2.join();
    std::cout << "Final counter: " << counter << std::endl;
    return 0;
}
```

## 8. Move Semantics and Rvalue References

### Definition:
Move semantics allow efficient transfer of resources from temporary objects, reducing unnecessary copying.

### Characteristics:
- `std::move` converts an object to an rvalue reference.  
- Move constructors and move assignment operators enable resource transfer.  
- Follows the Rule of Five: destructor, copy/move constructors, copy/move assignment operators.  
- Improves performance by avoiding deep copies.

### Example Code:
```cpp
class ResourceHolder {
    int* data;
    size_t size;
public:
    // Constructor
    ResourceHolder(size_t s) : size(s), data(new int[s]) {}

    // Destructor
    ~ResourceHolder() { delete[] data; }

    // Move constructor
    ResourceHolder(ResourceHolder&& other) noexcept 
        : data(other.data), size(other.size) {
        other.data = nullptr;
        other.size = 0;
    }

    // Move assignment
    ResourceHolder& operator=(ResourceHolder&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            size = other.size;
            other.data = nullptr;
            other.size = 0;
        }
        return *this;
    }

    // Disable copying (Rule of Five)
    ResourceHolder(const ResourceHolder&) = delete;
    ResourceHolder& operator=(const ResourceHolder&) = delete;
};

ResourceHolder createResource(size_t size) {
    ResourceHolder temp(size);
    // Initialize temp
    return temp; // Invokes move constructor
}

ResourceHolder rh = createResource(100); // Move construction
```

## 9. Namespaces

### Definition:
Namespaces provide a logical grouping of code to prevent naming conflicts in large projects.

### Characteristics:
- Avoid name collisions by encapsulating identifiers.  
- Can be nested for hierarchical organization.  
- Support aliasing for convenience.  
- Use `using` directive or declaration to simplify access.

### Example Code:
```cpp
namespace Physics {
    const double GRAVITY = 9.8;

    namespace Math {
        double square(double x) { return x * x; }
    }
}

namespace PM = Physics::Math; // Namespace alias

double calculateForce(double mass) {
    return mass * Physics::GRAVITY;
}

double calculateEnergy(double mass, double velocity) {
    using Physics::Math::square;
    return 0.5 * mass * square(velocity);
}
```

## 10. Type Casting

### Definition:
Type casting is the explicit conversion between different data types in C++.

### Characteristics:
- `static_cast`: General purpose conversion checked at compile time.  
- `dynamic_cast`: Safe downcasting in polymorphic hierarchies.  
- `const_cast`: Add or remove `const` qualifier.  
- `reinterpret_cast`: Low-level reinterpretation of bit patterns.

### Example Code:
```cpp
class Base { virtual void foo() {} };
class Derived : public Base {};

Base* b = new Derived();

// Safe downcast
Derived* d = dynamic_cast<Derived*>(b);
if (d) {
    std::cout << "Successful downcast" << std::endl;
}

// Numeric conversion
double pi = 3.14159;
int approxPi = static_cast<int>(pi);

// Const manipulation
const int x = 10;
int& y = const_cast<int&>(x); // Remove const (use with caution)

// Reinterpret pointer
int* ip = new int(65);
char* cp = reinterpret_cast<char*>(ip);
```

## 11. Memory Management Internals

### Definition:
Understanding how memory is allocated and managed in C++ programs.

### Characteristics:
- Stack: Automatic, fast allocation with limited size.  
- Heap: Manual allocation, larger but slower.  
- RAII (Resource Acquisition Is Initialization): Ties resource management to object lifetime.  
- Object slicing: Loss of derived class information when copying to base class.

### Example Code:
```cpp
// Stack allocation
void stackExample() {
    int x = 10; // On stack
    // Automatically cleaned up
}

// Heap allocation
void heapExample() {
    int* y = new int(20); // On heap
    delete y; // Must manually free
}

// RAII example
class FileHandler {
    std::FILE* file;
public:
    FileHandler(const char* filename, const char* mode) 
        : file(std::fopen(filename, mode)) {}
    ~FileHandler() { if (file) std::fclose(file); }
    // Other methods...
};

// Object slicing example
class Base { public: virtual void foo() {} };
class Derived : public Base { public: int extra; };

Derived d;
Base b = d; // Slicing - extra member is lost
```

## 12. Modern C++ Features

### Definition:
Modern C++ features introduced in C++11, C++14, C++17, and C++20 enhance language expressiveness and safety.

### Characteristics:
- Type inference with `auto` and `decltype`.  
- Range-based for loops for cleaner iteration.  
- Structured bindings for unpacking tuples and pairs.  
- `std::optional` for nullable values.  
- Concepts for template constraints (C++20).  
- Modules for faster compilation (C++20).  

## 13. Preprocessor Directives

### Definition:
Preprocessor directives are instructions that are processed by the preprocessor before the actual compilation of code begins. They are used to include files, define macros, and conditionally compile parts of the code.

### Characteristics:
- Begin with the `#` symbol.  
- Common directives include `#include`, `#define`, `#ifdef`, `#ifndef`, `#endif`.  
- `#include` is used to include header files or other source files.  
- `#define` is used to define macros or constants.  
- Enable conditional compilation to include or exclude code based on conditions.  
- Help in code modularity and reuse.

### Example Code:

#### Using `#include`
```cpp
#include <iostream>
#include "myheader.h"  // User-defined header file

int main() {
    std::cout << "Hello, World!" << std::endl;
    printMessage();  // Function declared in myheader.h
    return 0;
}
```

#### Using `#define` for Constants
```cpp
#include <iostream>

#define PI 3.14159
#define MAX(a,b) ((a) > (b) ? (a) : (b))

int main() {
    std::cout << "Value of PI: " << PI << std::endl;
    std::cout << "Max of 10 and 20: " << MAX(10, 20) << std::endl;
    return 0;
}
```

#### Conditional Compilation
```cpp
#include <iostream>

#define DEBUG

int main() {
#ifdef DEBUG
    std::cout << "Debug mode is ON" << std::endl;
#endif

#ifndef RELEASE
    std::cout << "Release mode is OFF" << std::endl;
#endif

    return 0;
}
```
