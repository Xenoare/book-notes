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

+ The C++ Keywords are
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/5993f8ad-5f4b-44a8-a070-f720d4c40894">
</p>

### Part 7 : Pointer and Reference
+ The Pointer and Reference is the most tricky ones. So basically, the fundamental operation on a pointer is called `deferencing` (that's it, referencing to the object pointed by the pointer).
+ In other hand, `Reference` is an alternate names of an object, or so called an alias. The main usage of reference is to specifying an argument and return values for function in general and for overload operator in particular.
+ To reflect the lvalue/rvalue and const/non-const distinctions, there are three kinds of references:
1. lvalue references: to refer to objects whose value we want to change
2. const references: to refer to objects whose value we do not want to change (e.g., a constant)
3. rvalue references: to refer to objects whose value we do not need to preserve after we have used it (e.g., a temporary)

+ First, the notation of `&x` means `reference to x`. It often called _lvalue references_, for examples
```
void g() {
    int var = 0;
    int& rr {var};
    ++rr; // var is incremented to 1
    int∗ pp = &rr; // pp points to va
}
```

+ Here, `++rr` doesn't increment the reference `rr`, but `++` is applied to the `int` which `rr` refers to (var). Consequently, the value of the reference cannot be change after initialization (it's always refers to the object was reference to denote).
+ To get the pointer to the object denoted by the reference we can use the `&` as on the line 4 of `g` function. Thus, we cannot have a pointer to a reference. Furthermore, we cannot define an array of references. In that sense, a reference is not an object.
+ A reference can be used to specify a function argument such that the value that passed to the function can be modified. For example
```
struct Point {
    int x;
    int y;
};

void modifyPoint(Point& p) {
    p.x += 10;
    p.y += 5;
}

int main() {
    Point myPoint = {5, 8};
    modifyPoint(myPoint);
```

+ An `rvalue` reference in other hand refers to an temporary object, which the user of the reference can modify (assuming the object will never be used again).
+ `rvalue` references can be used for moving semantic, allowing efficient transfer of resources between object.
```
std::vector<int> createVector(){
    std::vector<int> tempVec = {1, 2, 3, 4, 5};
    return tempVec;
}

int main(){
    // With move semantics (using an rvalue reference), ownership is transferred efficiently
    std::vector<int>&& refVec = createVector();
}
```

+ One implemenation of using `rvalue`, consider a `swap()` function that takes an T type that can swap some element. But if the T is a type which can be expensive to copy elements (such as `string` or `vector`). This will result in an expensive operation.
+ Since we didn't want any copies at all (just move the values of a, b, and temp). We can try to do this
```
template <class T>
void swap(T& a, T& b) {
    T tmp {static_cast<T&&> (a)
    a = static_cast<T&&> (b)
    b = static_cast<T&&> (a)
}
```

+ The result value of `static_cast<T&&>(x)` is an rvalue of type T&& for x. But nowadays, the use of `static_cast` had been changed by using the `move()` (`move(x)` means `static_swap<T&&>(x)`).
+ Last and yet it was trival, the relation between pointer and references. Pointer and references are two mechanism for refferring an object from different program without needed to copying.
+ If you need to change object to refer to, use a pointer. You can use the `pointer arithmatic` to change the value of the pointer variable.
```
void fp(char *p){
    while(*p){
        cout << *++p;
    }
}
```

+ If you want a collection of something that refers to an object, you must use a pointer
```
int x, y;
string& a1[] = {x, y}; // error : array of references
string∗ a2[] = {&x, &y}; // OK
vector<string&> s1 = {x , y}; // error : vector of references
vector<string∗> s2 = {&x, &y}; // OK
```

+ Conversely, if you want to be sure that a name always refers to the same object, use a reference.
+ If you want to use a user-defined (overload) operator on something that refers to an object, use a reference.
```
Matrix operator+(const Matrix&, const Matrix&); // OK
Matrix operator−(const Matrix∗, const Matrix∗); // error : no user-defined type argument

Matrix y, z; // ...
Matrix x = y+z; // OK
Matrix x2 = &y−&z; // error and ugly
```

+ Use containers (e.g., vector, array, and valarray) rather than built-in (C-style) arrays.

### Part 8 : Structures, Unions and Enumeration
+ The expanded of user-defined types is very useful in certain scenarios. But there are 3 most primitives variants
1. A `struct` is a sequence of elements (called `members`) of arbitary types.
2. A `union` is a struct that holds the value of just one elements at any one time.
3. An `enum` (or called enumeration) is a type with a set of named constants (called enumerators).

+ One trivial thing about the size of the `struct` is based on the order on how the are declared. So you can minimize the wasted space created on the `struct` by ordering based on the highest member first. For example
```
struct Readout {
int value;
char hour; // [0:23] 
char seq; // ['a':'z']
}
```

+ This would give us the size of the `Readout Structure`
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/c4dcf677-16db-43ff-8acb-e2e6e857b09c">
</p>

+ Every `struct` must have a `unique` definition on their program.
+ It is possible to bundle several tiny variable (in bit) in such a struct (this is called `bit-field`). A member is defined to be a field by specifying the number of bit to occupy. For example
```
struct Flags {
    unsigned int isSet : 1;  // 1-bit bit-field
    unsigned int value : 4;  // 4-bit bit-field
};
```

+ Fields are simply a convenient shorthand for using bitwise logical operators. It is typically much faster to access the `int` / `char` rather than the bit-field.
+ The `union` in other hands are completely different than struct, where union is to allow different types to share the same memory space. Hence, allowing to represent a value in multiple ways.
+ Use unions to save space (represent alternatives) and never for type conversion (Advice from the book)
+ Mostly union are used as the `Type Conversion` where we work with low-level bit program to manipulate the value. Take an example on how the union are used to represnt the floating-point types
```
union FloatComponents {
    float floatValue;
    struct {
        uint32_t mantissa : 23;
        uint32_t exponent : 8;
        uint32_t sign : 1;
    } components;
};
```

+ Lastly, `enum` (enumeration) are ways to represent a `set` of constants. There are two kinds of enumeration
1. `enum class`es, for which the enumerator names (e.g., red) are local to the enum and their values do not implicitly convert to other types.
2. `Plain` enum, for which the enumerator names are in the same scope as the enum and their values implicitly convert to `integers`.

+ By default the underlining types for `enum` are immplicitly `integer`. But for the `enum class`es, it must be explicitly define the underling types, whether `int`, `char`, `unsigned int`, and etc.
+ And for convertion itself, both enumeration need some explicit conversion to convert to other data types. This can be done with the help of `static_cast`.

### Part 9 : Statements
+ A good comment states the piece of code is supposed to do (the intent of the code), whereas the code itself states what it does (the way it does it). Some preference in making a good comments are
1. A comment for each source file stating what the declarations in it have in common, references to manuals, the name of the programmer, general hints for maintenance, etc.
2. A comment for each class, templates, and namespace.
3. A comment for each global and namespace variable and constant

### Part 10 : Expression
+ A program consist of four main parts: a `parser`, an `input function`, a `symbol table`, and a `driver`.
+ Basically, a program are some sequence of expression (the defition of `expression` are varied from the value of the variable, an argument of a function an many more). Such a basic expression are the binary and unary operation (+, -, *, /).
+ The next step is the parser do, is to tokenize the expression and identifier and applied the grammar rules of the language (This step is done by the `Token_stream` mechanism). We can look on how the tokenize of the code `int x = 4;`
```
std::vector<Token> tokenStream = {
Token(Token::KEYWORD, "int"),
    Token(Token::IDENTIFIER, "x"),
    Token(Token::OPERATOR, "="),
    Token(Token::INT_LITERAL, "4"),
    Token(Token::SEMICOLON, ";")
};
```

+ As the parser processes the tokens and builds the AST, it populates the symbol table. The symbol table keeps track of all identifiers (such as variable names, function names, etc.) declared in the program along with their types, scopes, and other attributes. The parser uses the symbol table to check for name conflicts, verify that variables are declared before use, and resolve references to variables and functions.
+ Lastly, the driver orchestrates the overall process. It invokes the input function to read the source code, passes the tokens to the parser, and manages the interaction between the parser and the symbol table.
+ Here's some basic rules for the grammar. Remember, the operator in higher place have higher precedance. It means that the `*p++` is actually `*(p++)`, not `(*p)++`.
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/8e0b0000-0b0d-4046-90ba-10bc014da934">
</p>
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/ce2c099c-7554-49ce-84cb-ac7c57fea4fe">
</p>
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/7a97a2a4-4cfe-49d7-97f5-af3bcb4a631e">
</p>

+ Back again on how the parser work. Before we applying the grammar rules of the language, some lexical token are commpose from a character. Like in the case of `int x = 4;`. This is called `Max Munch Rule`.
<p align="center">
    <img width="500" src="https://github.com/Xenoare/book-notes/assets/67181778/7706ef10-6820-4845-b2a5-8d4713ff3b67">
</p>

### Part 11 : Select Operation
+ Object allocated with `new` operator said to be on `free store` (or called `on the heap`, or in the `dynamic memory`).
+ As rule of thumb, any object created by `new` **exist** until it is explicitly destroyed by `delete`.
+ But the main problem with free store is that
1. Leaked objects: People use new and then forget to delete the allocated object.
2. Premature deletion: People delete an object that they have some other pointer to and later use that other pointer.
3. Double deletion: An object is deleted twice, invoking its destructor (if any) twice.

+ We can try to overloading the `new` and `delete` operators. For the `new` operators there are 3 version of `new` based on the docs.
```
throwing (1)	void* operator new (std::size_t size);
nothrow (2)	 void* operator new (std::size_t size, const std::nothrow_t& nothrow_value) noexcept;
placement (3)	 void* operator new (std::size_t size, void* ptr) noexcept;
```

+ Throwing new (1): This is the standard version of the new operator that attempts to allocate memory and throws a std::bad_alloc exception if it fails. It takes a single argument, the size of the memory to be allocated.
+ Nothrow new (2): This version of the new operator is similar to the throwing new but does not throw an exception if memory allocation fails. Instead, it returns a null pointer. It also takes a single argument, the size of the memory to be allocated, and a second argument, std::nothrow.
+ Placement new (3): This version of the new operator is used for constructing an object at a specific memory location (known as placement new). It takes two arguments: the size of the memory to be allocated and a pointer to the memory location where the object should be constructed. This version does not actually allocate new memory but merely constructs an object at the specified memory location.
+ For the `delete`, it just dealocate the storage (You can look up on the docs).
+ A `lambda expression` or just known as the `lambda function` is a way to define the anonymus function object. The basic syntax for the lambda are
```
[capture list] (parameters) mutable(optional) exception attribute -> return type { function body }
```

+ Capture List: Specifies which external variables are available inside the lambda function. It can capture variables by value or by reference.
+ Parameters: The parameters of the lambda function, if any.
+ Mutable: Allows the lambda to modify captured variables by value.
+ Exception Attribute: Specifies the type of exceptions the lambda can throw.
+ Return Type: The return type of the lambda function.
+ Function Body: The code that is executed when the lambda is invoked.

+ You can use a capture-default mode to indicate how to capture any outside variables referenced in the lambda body: `[&]` means all variables that you refer to are captured by reference, and `[=]` means they're captured by value. You can use a default capture mode, and then specify the opposite mode explicitly for specific variables. For example, if a lambda body accesses the external variable `total` by reference and the external variable `factor` by value, then the following capture clauses are equivalent:
```
[&total, factor]
[factor, &total]
[&, factor]
[=, &total]
```

### Part 12 : Functions
+ The definition of function declaration in C++, a function declaration can contain a variety of specifier and modifier. Such as we can have
1. The name of the function; required
2. The argument list, which may be empty `()`; required
3. The return type, which may be void and which may be prefix or suffix (using `auto`); required
4. inline, indicating a desire to have function calls implemented by inlining the function body
5. constexpr, indicating that it should be possible to evaluate the function at compile time if given constant expressions as arguments.
6. noexcept, indicating that the function may not throw an exception.
7. A linkage specification, for example, `static`
8. [[noreturn]], indicating that the function will not return using the normal call/return mechanism

+ In addition, member function may be specified as
1. virtual, indicating that it can be overridden in a derived class 
2. override, indicating that it must be overriding a virtual function from a base class 
3. final, indicating that it cannot be overriden in a derived class 
4. static, indicating that it is not associated with a particular object 
5. const, indicating that it may not modify its object

+ I don't know but the syntax for the function declaration is more like this
```
struct S {
[[noreturn]] virtual inline auto f(const unsigned long int ∗const) −> void const noexcept;
};
```

+ Every function declaration contains the specification of the function return `types`. However, there are two declaration for returning types
```
int multiply(int x){} // prefix
auto multiply(int x){} -> int //suffix
```

+ The essential use for a suffix return type comes in function template declarations in which the return type depends on the arguments. For example:
```
template<class T, class U>
auto product(const vector<T>& x, const vector<U>& y) −> decltype(x∗y)
```

+ In general, a function will not be evaluated at compile time and therefore it cannot be called in a constant expression. But, by defining the a function `constexpr` we indicate that we want it to be usable in constant expressions if given constant expressions as argument.
```
constexpr int fac(int x) {
    return (x > 1) ? x fac(x-1): 1
}

constexpr int f9 = fac(9) // may be evaluated in compile time
```

+ To be evaluated a compile time, a `constexpr` function must consist of a single `return` statement; no `loops` and no local `variables` are allowed. Also, a constexpr function may not have `side effects`. That is, a constexpr function is a pure function.
+ A local variable or constant is initialized when a thread of execution reaches its definiion. If a `local variable` declared as a `static`, a `single` statically allocated object will be used to represent that variable in all calls of a function. It will only initialized only the first time the thread of execution reaches is definition.
+ The general rule of thumb of passing an arguments to a function is like this
1. Use `pass-by-value` for a small object
2. Use `pass-by-const-reference` for a larger object that you don't need to modify
3. Return an result as a `return` value rather than modifying the argument object
4. Use rvalue references to implement move (§3.3.2, §17.5.2) and forwarding
5. Pass a pointer if ‘‘no object’’ is a valid alternative (and represent ‘‘no object’’ by nullptr).
6. Use pass-by-reference only if you have to.

+ For some case, where we don't know the number and type of arguments be expected in a function, we can solve this by introducing some `variadic function` which take variable number of arguments. One tool for doing this is `elipsis (...)`, this is done by the macros `<cstdarg>`.
+ When a function `fn` is called. The compiler must determine which of the function name `fn` to invoke. This can be done by comparing the types of an actual arguments with the type of the parameter of all functions in the scope called `fn`.
+ The idea is to invoke the function that is the best match to the arguments and give a compile-time error if no function is the best match
```
void print(long l)
void print(double d)

int main() {
    print(1L) // print long
    print(2.3) // print double
    print(1) // Error, ambigous: print(long(1)) or print(double(1))
}
```

+ To approximate our notions of what is reasonable, a series of criteria are tried in order:
1. Exact match; that is, match using no or only trivial conversions (for example, array name to pointer, function name to pointer to function, and T to const T)
2. Match using promotions; that is, integral promotions (bool to int, char to int, short to int, and their unsigned counterparts; §10.5.1) and float to double
3. Match using standard conversions (e.g., int to double, double to int, double to long double, `Derived∗` `to Base∗`, `T∗` to `void∗`, int to unsigned int 
4. Match using user-defined conversions (e.g., double to complex<double>;)
5. Match using the ellipsis ... in a function declaration

+ Return types are not consider an overload resolution. The reason is to keep the resolution for an individual operator or function call `context-independent`.
+ Multiple functions share the same name but differ in the types of their parameters. The compiler uses the argument types to decide which overloaded function to call.
```
int pow(int, int);
double pow(double, double);
complex pow(double, complex);
complex pow(complex, int);
complex pow(complex, complex);

void k(complex z)
{
int i = pow(2,2); // invoke pow(int,int)
double d = pow(2.0,2.0); // invoke pow(double,double)
complex z2 = pow(2,z); // invoke pow(double,complex)
complex z3 = pow(z,2); // invoke pow(complex,int)
complex z4 = pow(z,z); // invoke pow(complex,complex)
}
```

+ Declaring too few (or too many) overloaded versions of a function can lead to ambiguities. Where possible, consider the set of overloaded versions of a function as a whole and see if it makes sense according to the semantics of the function. Often the problem can be solved by adding a version that resolves ambiguities
```
void inline fun1(n) { fun1(long(n)) }
```

+ Finally, like an object, the code also put somewhere in the memory about the function body (so it has an address). We can point to an function, but here are only two things
one can do to a function: `call it` and `take its address`. The pointer obtained by taking the address of a function can then be used to call the function
```
void error(string s) { /*... */ }
void (∗efct)(string); // pointer to function taking a string argument and returning nothing

void f()
{
efct = &error; // efct points to error
efct("error"); // call error through efct
}
```

+ The compiler will discover `efct` is a pointer and call the function pointed to. For the deferencing itself, you can optianally deferencing the function pointer with `*` and use the `()` to call the function, or just directly call the function through the pointer.
```
void (∗f1)(string) = &error; // OK: same as = error
void (∗f2)(string) = error; // OK: same as = &error

void g()
{
f1("Vasa"); // OK: same as (*f1)("Vasa")
(∗f1)("Mary Rose"); // OK: as f1("Mary Rose")
}
```

+ Prefer function objects (including lambdas) and virtual functions to pointers to functions
+ A function should perform a single logical operation
+ If you must use macros, use ugly names with lots of capital letters

### Part 13 : Exception Handling
+ Use Hierarchial error handling, like this
```
exception
   logic_error
      domain_error
      invalid_argument
      length_error
      out_of_range
   runtime_error
      range_error
      overflow_error 
      underflow_error 
```

+ Use the `Resource Acquisition Is Initialization` technique to manage resources
+ Release locally owned resources before throwing an exception
+ Beware of memory leaks caused by memory allocated by new not being released in case of an exception
+ A library shouldn’t unilaterally terminate a program. Instead, throw an exception and let a caller decide

### Part 14 : Namespaces
+ Use namespaces to express logical structure
+ If necessary, use namespace aliases to abbreviate long namespace names
+ Use the `Namespace::member` notation when defining namespace members
+ Use `using`-directives for transition, for foundational libraries (such as `std`), or within a local scope
+ Don’t put a `using`-directive in a header file

### Part 15 : Source and Program Files
+ Don’t define global entities with the same name and similar-but-different meanings in different translation units
+ Distinguish between `users` interfaces and `implementers` interfaces
+ Use `#include` only at global scope and in namespaces
+ Use `include guards`
+ Make headers self-contained
