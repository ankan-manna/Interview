# 1. File Handling

## File Streams

C++ provides three classes for file handling:

- `ifstream` (input file stream) for reading from files
- `ofstream` (output file stream) for writing to files
- `fstream` (file stream) for both reading and writing

### Characteristics:

- Inherit from iostream classes
- Provide methods for opening, closing, and manipulating files
- Support both text and binary modes

### Example: Reading/Writing to Files

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    // Writing to a file
    std::ofstream outFile("example.txt");
    if (outFile.is_open()) {
        outFile << "Hello, File Handling!\n";
        outFile << 42 << "\n";
        outFile.close();
    }

    // Reading from a file
    std::ifstream inFile("example.txt");
    std::string line;
    if (inFile.is_open()) {
        while (getline(inFile, line)) {
            std::cout << line << "\n";
        }
        inFile.close();
    }

    return 0;
}
```

## Binary Files

For handling non-text data like images or structured binary data.

### Example: Binary File Operations

```cpp
#include <iostream>
#include <fstream>

struct Person {
    char name[50];
    int age;
    double height;
};

int main() {
    Person p1 = {"Alice", 30, 5.7};

    // Writing binary
    std::ofstream outFile("person.dat", std::ios::binary);
    outFile.write(reinterpret_cast<char*>(&p1), sizeof(Person));
    outFile.close();

    // Reading binary
    Person p2;
    std::ifstream inFile("person.dat", std::ios::binary);
    inFile.read(reinterpret_cast<char*>(&p2), sizeof(Person));
    inFile.close();

    std::cout << "Name: " << p2.name << ", Age: " << p2.age 
              << ", Height: " << p2.height << "\n";

    return 0;
}
```

# 2. Templates (Generic Programming)

## Function Templates

Allow functions to operate with generic types.

### Example:

```cpp
#include <iostream>

template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    std::cout << max(3, 7) << "\n";          // int
    std::cout << max(3.14, 2.71) << "\n";    // double
    std::cout << max('a', 'z') << "\n";      // char
    return 0;
}
```

## Class Templates

Allow classes to have members that use template parameters as types.

### Example:

```cpp
#include <iostream>

template <typename T>
class Box {
private:
    T content;
public:
    void setContent(T newContent) {
        content = newContent;
    }
    T getContent() {
        return content;
    }
};

int main() {
    Box<int> intBox;
    intBox.setContent(123);
    std::cout << intBox.getContent() << "\n";

    Box<std::string> strBox;
    strBox.setContent("Hello Templates!");
    std::cout << strBox.getContent() << "\n";

    return 0;
}
```

## Template Specialization

Provide a specialized implementation for specific types.

### Example:

```cpp
#include <iostream>

template <typename T>
void printType(T value) {
    std::cout << "Generic type: " << value << "\n";
}

template <>
void printType<double>(double value) {
    std::cout << "Specialized for double: " << std::scientific << value << "\n";
}

int main() {
    printType(5);        // Generic
    printType(3.14);     // Specialized
    printType("Hello");  // Generic
    return 0;
}
```

# 3. Exception Handling

## Basic Exception Handling

```cpp
#include <iostream>
#include <stdexcept>

double divide(double a, double b) {
    if (b == 0) {
        throw std::runtime_error("Division by zero!");
    }
    return a / b;
}

int main() {
    try {
        std::cout << divide(10, 2) << "\n";
        std::cout << divide(5, 0) << "\n";  // This will throw
    } catch (const std::runtime_error& e) {
        std::cerr << "Error: " << e.what() << "\n";
    } catch (...) {
        std::cerr << "Unknown error occurred\n";
    }
    return 0;
}
```

## Custom Exception Classes

```cpp
#include <iostream>
#include <stdexcept>

class NegativeValueError : public std::runtime_error {
public:
    NegativeValueError() : std::runtime_error("Negative value not allowed") {}
};

void processPositive(int value) {
    if (value < 0) {
        throw NegativeValueError();
    }
    std::cout << "Processing: " << value << "\n";
}

int main() {
    try {
        processPositive(10);
        processPositive(-5);  // Throws custom exception
    } catch (const NegativeValueError& e) {
        std::cerr << "Custom Error: " << e.what() << "\n";
    }
    return 0;
}
```

# 5. Lambda Expressions

## Basic Syntax

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    // Simple lambda
    auto greet = []() { std::cout << "Hello Lambda!\n"; };
    greet();

    // Lambda with parameters
    auto add = [](int a, int b) { return a + b; };
    std::cout << "5 + 3 = " << add(5, 3) << "\n";

    // Lambda with STL
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    std::for_each(numbers.begin(), numbers.end(), [](int n) {
        std::cout << n * n << " ";
    });
    std::cout << "\n";

    return 0;
}
```

## Capturing Variables

```cpp
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // Capture by value
    auto captureByValue = [x]() { std::cout << "x: " << x << "\n"; };
    captureByValue();

    // Capture by reference
    auto captureByRef = [&y]() { y++; std::cout << "y: " << y << "\n"; };
    captureByRef();
    std::cout << "y after lambda: " << y << "\n";

    // Mixed capture
    auto mixed = [x, &y]() { std::cout << "x: " << x << ", y: " << y << "\n"; };
    mixed();

    // Capture all by value
    auto allByValue = [=]() { std::cout << "x: " << x << ", y: " << y << "\n"; };
    allByValue();

    // Capture all by reference
    auto allByRef = [&]() { x++; y++; };
    allByRef();
    std::cout << "After allByRef, x: " << x << ", y: " << y << "\n";

    return 0;
}
```

# 6. Smart Pointers (C++11)

## unique_ptr

```cpp
#include <iostream>
#include <memory>

class Resource {
public:
    Resource() { std::cout << "Resource acquired\n"; }
    ~Resource() { std::cout << "Resource released\n"; }
    void use() { std::cout << "Resource used\n"; }
};

int main() {
    // unique_ptr example
    std::unique_ptr<Resource> res1(new Resource());
    res1->use();

    // Transfer ownership
    std::unique_ptr<Resource> res2 = std::move(res1);
    if (res1) res1->use();  // Won't execute
    if (res2) res2->use();  // Will execute

    return 0;  // Resource automatically released
}
```

## shared_ptr and weak_ptr

```cpp
#include <iostream>
#include <memory>

class Node {
public:
    int value;
    std::shared_ptr<Node> next;
    std::weak_ptr<Node> prev;  // Break circular reference

    Node(int val) : value(val) { std::cout << "Node " << value << " created\n"; }
    ~Node() { std::cout << "Node " << value << " destroyed\n"; }
};

int main() {
    auto node1 = std::make_shared<Node>(1);
    auto node2 = std::make_shared<Node>(2);

    // Create circular reference
    node1->next = node2;
    node2->prev = node1;

    // Access through weak_ptr
    if (auto sharedPrev = node2->prev.lock()) {
        std::cout << "Previous node value: " << sharedPrev->value << "\n";
    }

    return 0;  // Both nodes properly destroyed
}
```

# 7. Multithreading (C++11 and beyond)

## Basic Threading

```cpp
#include <iostream>
#include <thread>
#include <vector>

void printHello(int id) {
    std::cout << "Hello from thread " << id << "\n";
}

int main() {
    std::vector<std::thread> threads;
    
    for (int i = 0; i < 5; ++i) {
        threads.emplace_back(printHello, i);
    }

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```

## Mutexes and Locks

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <vector>

std::mutex mtx;
int sharedData = 0;

void incrementData(int id) {
    for (int i = 0; i < 5; ++i) {
        std::lock_guard<std::mutex> lock(mtx);
        ++sharedData;
        std::cout << "Thread " << id << " incremented to " << sharedData << "\n";
    }
}

int main() {
    std::vector<std::thread> threads;
    
    for (int i = 0; i < 3; ++i) {
        threads.emplace_back(incrementData, i);
    }

    for (auto& t : threads) {
        t.join();
    }

    std::cout << "Final value: " << sharedData << "\n";
    return 0;
}
```

# 8. Move Semantics and Rvalue References

## Move Semantics

```cpp
#include <iostream>
#include <vector>
#include <utility>

class Buffer {
    int* data;
    size_t size;
public:
    Buffer(size_t sz) : size(sz), data(new int[sz]) {
        std::cout << "Constructed buffer of size " << size << "\n";
    }
    
    // Copy constructor
    Buffer(const Buffer& other) : size(other.size), data(new int[other.size]) {
        std::copy(other.data, other.data + size, data);
        std::cout << "Copied buffer of size " << size << "\n";
    }
    
    // Move constructor
    Buffer(Buffer&& other) noexcept : size(other.size), data(other.data) {
        other.data = nullptr;
        other.size = 0;
        std::cout << "Moved buffer of size " << size << "\n";
    }
    
    ~Buffer() {
        delete[] data;
        std::cout << "Destroyed buffer\n";
    }
};

int main() {
    Buffer b1(100);  // Regular constructor
    
    Buffer b2 = b1;  // Copy constructor
    
    Buffer b3 = std::move(b1);  // Move constructor
    
    std::vector<Buffer> buffers;
    buffers.push_back(Buffer(200));  // Move constructor called
    
    return 0;
}
```

# 9. Namespaces

## Namespace Usage

```cpp
#include <iostream>

namespace Math {
    const double PI = 3.14159;
    
    double square(double x) {
        return x * x;
    }
}

namespace Physics {
    const double G = 9.81;
    
    double potentialEnergy(double mass, double height) {
        return mass * G * height;
    }
}

// Nested namespace
namespace Game {
    namespace Physics {
        const float G = 2.0f;
    }
}

// Namespace alias
namespace GP = Game::Physics;

int main() {
    std::cout << "Math PI: " << Math::PI << "\n";
    std::cout << "Math square: " << Math::square(5) << "\n";
    
    std::cout << "Physics G: " << Physics::G << "\n";
    std::cout << "Game Physics G: " << Game::Physics::G << "\n";
    std::cout << "Alias Physics G: " << GP::G << "\n";
    
    return 0;
}
```

# 10. Type Casting

## C++ Style Casts

```cpp
#include <iostream>
#include <string>

class Base {
public:
    virtual ~Base() {}
    virtual void print() { std::cout << "Base\n"; }
};

class Derived : public Base {
public:
    void print() override { std::cout << "Derived\n"; }
    void specific() { std::cout << "Derived specific\n"; }
};

int main() {
    // static_cast - compile-time checked
    double d = 3.14;
    int i = static_cast<int>(d);
    std::cout << "static_cast: " << i << "\n";

    // dynamic_cast - runtime checked (for polymorphism)
    Base* b = new Derived();
    Derived* derived = dynamic_cast<Derived*>(b);
    if (derived) {
        derived->specific();
    }

    // const_cast - add/remove const
    const int x = 10;
    int& y = const_cast<int&>(x);
    y = 20;  // Undefined behavior if x was actually const
    std::cout << "const_cast: " << x << ", " << y << "\n";

    // reinterpret_cast - low-level reinterpreting
    intptr_t p = reinterpret_cast<intptr_t>(b);
    std::cout << "reinterpret_cast: " << p << "\n";

    delete b;
    return 0;
}
```

# 11. Memory Management Internals

## RAII Example

```cpp
#include <iostream>
#include <memory>

class FileHandler {
    FILE* file;
public:
    FileHandler(const char* filename, const char* mode) : file(fopen(filename, mode)) {
        if (!file) throw std::runtime_error("Failed to open file");
        std::cout << "File opened\n";
    }
    
    ~FileHandler() {
        if (file) {
            fclose(file);
            std::cout << "File closed\n";
        }
    }
    
    void write(const char* text) {
        if (fputs(text, file)) {
            throw std::runtime_error("Write failed");
        }
    }
};

int main() {
    try {
        FileHandler fh("test.txt", "w");
        fh.write("RAII example\n");
        // File automatically closed when fh goes out of scope
    } catch (const std::exception& e) {
        std::cerr << "Error: " << e.what() << "\n";
    }
    return 0;
}
```

# 12. Modern C++ Features

## C++11/14/17 Features

```cpp
#include <iostream>
#include <vector>
#include <optional>
#include <variant>
#include <any>

// auto and decltype
auto add(auto a, auto b) -> decltype(a + b) {
    return a + b;
}

// Range-based for loop
void printVector(const std::vector<int>& vec) {
    for (const auto& item : vec) {
        std::cout << item << " ";
    }
    std::cout << "\n";
}

// Structured bindings (C++17)
std::tuple<int, double, std::string> getData() {
    return {42, 3.14, "Hello"};
}

int main() {
    // auto and nullptr
    auto ptr = nullptr;
    if (!ptr) {
        std::cout << "ptr is nullptr\n";
    }

    // std::optional (C++17)
    std::optional<int> maybeInt;
    if (!maybeInt) {
        std::cout << "maybeInt has no value\n";
    }
    maybeInt = 42;
    if (maybeInt) {
        std::cout << "maybeInt has value: " << *maybeInt << "\n";
    }

    // std::variant (C++17)
    std::variant<int, double, std::string> v = "Hello";
    std::cout << "Variant holds: " << std::get<std::string>(v) << "\n";

    // std::any (C++17)
    std::any a = 42;
    std::cout << "Any holds int: " << std::any_cast<int>(a) << "\n";
    a = std::string("World");
    std::cout << "Any holds string: " << std::any_cast<std::string>(a) << "\n";

    // Structured bindings
    auto [num, d, str] = getData();
    std::cout << "Structured bindings: " << num << ", " << d << ", " << str << "\n";

    return 0;
}
```

## C++20 Concepts

```cpp
#include <iostream>
#include <concepts>

// Concept definition
template <typename T>
concept Addable = requires(T a, T b) {
    { a + b } -> std::same_as<T>;
};

// Function using concept
template <Addable T>
T sum(T a, T b) {
    return a + b;
}

class MyNumber {
    int value;
public:
    MyNumber(int v) : value(v) {}
    MyNumber operator+(const MyNumber& other) const {
        return MyNumber(value + other.value);
    }
    friend std::ostream& operator<<(std::ostream& os, const MyNumber& num) {
        return os << num.value;
    }
};

int main() {
    std::cout << sum(5, 3) << "\n";              // Works with int
    std::cout << sum(MyNumber(5), MyNumber(3)) << "\n"; // Works with MyNumber
    
    // sum("a", "b"); // Would fail to compile - strings don't satisfy Addable
    
    return 0;
}
