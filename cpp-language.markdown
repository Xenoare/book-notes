by Bjarne Stroustrup

## Part 1
### Chpater 2 : The Basics
+ There's two ways of defining a Const, `const` and `constexpr`. The main difference is that `constexpr` roughly say that it can be evaluated at the runtime.
+ Cpp also support several custom User Types such as `struct`, `class` and `enum`.
+ There are two ways of manipulating the memory and indirect access to the variable, of either using `Pointer (*)` or `References (&)`
+ We can use the modulariry in the cpp (splititng files) and etc.

### Chapter 3 : Abstraction Mechanism
+ The core concept of Cpp is the feature of the _class_ (user defined types to represent the concept in the code). An astounishing number of useful classes turn out to be these classes; `Concrete Classes`, `Abstract Classes` and `Classes in the Class Hierarcies`
+ Compare to the `Concrete Classes`, `Abstract Classes` is completely insulates the user from the implementation details. Since we don't know anything about the data types of `Abstract Classes` (not even the size), we must allocate object in the memory and access later with the pointer of reference. The key itself for defining the Abstract Classes is that the Derived key must be implement all member of `Pure Virtual Functions`

### Chapter 4 : Container and Algorithm
+ Below is a standard library header that supplying declarations in namespace `std`
<p align="center">
    <img width="500" height="350" src="https://github.com/Xenoare/book-notes/assets/67181778/b85f93ee-88b6-4b09-9a7f-54b0ec1552c1">
</p>
<p align="center">
    <img width="500" height="350" src="https://github.com/Xenoare/book-notes/assets/67181778/6991303a-259b-4cee-ba23-3259ecff067b">
</p>

+ I/O for the user define types is possible, but for the input itself is kinda complicated since it has to check for correct formatting and handling error.
+ Don't reinvent the whell, just use the libraries (prefer standard libraries over the other).
<p align="center">
    <img width="500" height="350" src="https://github.com/Xenoare/book-notes/assets/67181778/130c07ce-1aa6-4786-b0e2-c4ef777270fe">
</p>

### Chapter 5 : Concurrency and Utilities
+ The standard library component are designed to not leak resources, because they are rely on `Constructor` / `Destructor` resource manager.
+ The standard libarary `<memory>` provides us way to manage objects in the free store by `unique_ptr` to represent unique ownership and `shared_ptr` to represent shared ownership

## Part 2
### Chapter 6 :  Types and Declaration
+ The C++ does not imply that the language and the library itself guarentee good code, but there are three different behavior output on every scenario.
+ Many important things are on the `implementation-defined` by the standard, which means that any implementation details must be documented.
+ Any example on `implementation-defined` are the exact size of any data types such as `int` or `float`, the definition of `NULL` macro (0, `nullptr`, ((void)*0)). This implementation are documented somewhere else, such on the manual pages, or the library header.
+ The other behaviour is `unspecified` behaviour, where this behaviour arise when the standard gives multiple valid options for the behaviour of the certain construct, but it doesn't mandate which operation should be choosen, and it's up to the compiler to decide. Given the example
```
int x = 5;
std::cout << x++ << "" << x++ << std::endl;
```

+ In this example, the order of evaluation `x++` is unspecified. The compiler is free to decide the output of either `5 6` or `6 5`.
+ The last one is the `undefined` behaviour, where this behaviour is arise when you violate certain language rules (such as `deferencing a null pointer`). The standard doesn't define the what should happen when program enter the undefined behaviour.
