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
