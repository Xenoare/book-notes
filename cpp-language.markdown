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
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/b85f93ee-88b6-4b09-9a7f-54b0ec1552c1">
</p>
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/6991303a-259b-4cee-ba23-3259ecff067b">
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
+ A C++ implementation can be either `hosted` or `freestanding`. By default, C++ will use the `hosted` environment. The `freestanding` implies that the code-running environment are on the minimal operating support system, hence a `freestanding` environment has a fewer library compare to the `hosted` environment.
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/7c6f841c-a959-4235-9c90-b4d28184a5d6">
</p>

+ One trivial things is that a implementation-defined of `char` to be either `signed` or `unsigned`, where given the case of `char c = 255` then any integer variable that takes the value such as `int i = c` will have no clue about the whether value. On the machine where the char is defined as unsigned, the variable `i` will have value of 255, otherwise the variable `i` will have value of `-1`.
+ A char must `behave identically` to either a signed char or an unsigned char. However, the three char types are distinct, so you can’t mix pointers to different char types.
+ One properties that char data types have is ability to express any character in the machine character set (This stuff is called encoding, and there are two popular character encoding which is `ASCII` and `Unicode`). 
+ For the ASCII encoding, we can represent any character combined with the octal or some hexadecimal digit, respectively. For example:
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/19b3c64a-4c48-45e7-b530-d8875f81cd4c">
</p>

+ Unlike the ASCII that have 7 bit (127 character set), we can use the Unicode that have 8-bit or 32-bit or (4 or 8 hexadecimal digit, respectively) and represent as `u` for 8-bit and `U` for 16-bit Unicode encoding
```
char euro_symbol = '\u20AC';  // Euro symbol
```

+ Well, we come to some complicated topic about integer and its relatives, floating-point types.
+ Integer itself come with 4 sizes, `short` int (2 byte), `plain` int (4 byte), `long` int (4 or 8 byte depending on the machine) and `long long` int (8 byte). Integer also come with three forms same as `char`, with `int`, `signed int` and `unsigned int`. 
+ The other relatives, floating-point types comes with three version: `float` (single-precision), `double` (double-precision), and `long double` (extended-precision). By default, a floating-point literal is `double`. and any literal for integer and floating-point can be expressed in such `prefix` and `suffix` in this given table
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/81c915e6-ba0d-47e7-b81d-81c1629ecc20">
</p>

+ Remember that prefix `R`, `L`, and `u/U` are for string / character literals.
+ If you need a custom specific size for an integer (let's say an 16-bit integer), you can `include` the standard header `<cstdint>` that define a variety of types. For example:
```
int16_t x {0xaabb}; // 2 bytes
int64_t xxxx {0xaaaabbbbccccdddd}; // 8 bytes
int_least16_t y; // at least 2 bytes (just like int)
int_least32_t yy // at least 4 bytes (just like long)
int_fast32_t z; // the fastest int type with at least 4 bytes
```

+ The structure of declaration is defined within the C++ grammar. But for the sake of simplicity, we can consider the declaration having this part.
1. Optional prefix specifiers (e.g., static or virtual)
2. A base type (e.g., vector<double> or const int)
3. A declarator optionally including a name (e.g., p[7], n, or ∗(∗)[])
4. Optional suffix function specifiers (e.g., const or noexcept)
5. An optional initializer or function body (e.g., ={7,5,3} or {return x;})

+ A declarator is composed of some name and optionally some declarator operators. Some of the most common operators are this.
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/59812d51-ce1c-4311-a732-b33df68639b3">
</p>
