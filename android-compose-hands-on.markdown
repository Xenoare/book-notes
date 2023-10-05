## Thinking in Compose

### Kotlin Fundamentals
- [Nullability](#nullability)
- [Class and Object](#class-and-object)

---
### Nullability
> https://kotlinlang.org/docs/null-safety.html#what-s-next

You can use `null` to indicate that there's no value assocated with the variable.
```
fun main() {
    val favoriteActor = null
}
```

**Understand non-nullable and nullable variables**

In Kotlin, there's a distinction betweeen nullable and non-nullable types:
- Nullable types are variables that *can* hold `null`.
- Non-null types are variables that *can't* hold `null`.
A type is only nullable if you explicity let it hold `null`. As the error message says, the `String` data type is a non-nullable type, so you can't reassign the variable to `null`.

![image](https://github.com/Xenoare/book-notes/assets/67181778/83a01382-93d4-4f56-9225-28877721f5d7)

**Declaration Nullable Types**

To declare nullable variables in Kotlin, you need to add a `?` operator to the end of the type. For example, a `String?` type can hold either string or `null`, whereas a `String` type can only hold a string.
```
fun main() {
    var favoriteActor: String? = "Sandra Oh"
    favoriteActor = null
}
```

**Note**

```yaml
While you should use nullable variables for variables that can carry `null`,
you should use non-nullable variables for variables that can never carry `null`
because the access of nullable variables requires more complex handling.
```

**Access a property of a nullable variable**

Kotlin intentionally applies syntactic rules so that it can achive `null` *safety*, which guarantee that *no accidental calls are made on potentially `null` variables*.
```yaml
This doesnt mean that variables can't be null. It means that if a member of variable is accessed, the variable can't be null.
```

There is various techniques and operators to work with nullable types.
1. **Use the `?.` safe-call operator**

You can use the `?.` safe call operator to access methods or propeties of nullable variables.
![image](https://github.com/Xenoare/book-notes/assets/67181778/5467db6c-2fc8-4f9e-9a12-33970af4e040)
The `?.` safe-call operator allows safer access to nullable variables because Kotlin compiler stops any attempt of member access to `null` references and return `null` for the member accessed.
```kotlin 
fun main() {
    var favoriteActor: String? = "Sandra Oh"
    println(favoriteActor?.length)
}
```

2. **Use the `!!` not-null assertion operator**
![image](https://github.com/Xenoare/book-notes/assets/67181778/8fa9238c-9b66-4bb7-b50d-5d9830b96578)

Unlike `?.` safe-call operators, the use of a `!!` not-null assertion operator may result in a NullPointerException error being thrown if the nullable variable is indeed null. Thus, it should be done only when the variable is always non-nullable or proper exception handling is set in place. When not handled, exceptions cause runtime errors.
```kotlin
fun main() {
    var favoriteActor: String? = "Sandra Oh"
    println(favoriteActor!!.length)
}
```

3. **Use the `?:` Elvis operator**

With the `?:` Elvis operator, you can add a default value when the `?.` safe-call returns `null` (similar to `if/else` expression).
If the variable *isn't* `null`, the expression before `?:` Elvis operator executes. Otherwise, the expression after the `?:` Elvis operator executes.
![image](https://github.com/Xenoare/book-notes/assets/67181778/2a5efc8e-6e68-4584-bdbe-ffac460be59b)
```kotlin
fun main() {
    var favoriteActor: String? = "Sandra Oh"

    val lengthOfName = favoriteActor?.length ?: 0

    println("The number of characters in your favorite actor's name is $lengthOfName.")
}

```

### Class and Object
**Getter and Setter Function in Properties**

When you don't define the **getter** and **setter** function for a property, the kotlin compiler internally creates the function.
![image](https://github.com/Xenoare/book-notes/assets/67181778/9f9e8f60-db8d-48f5-bc7c-8130684fd92c)
```kotlin
var speakerVolume = 2
    get() = field  
    set(value) {
        field = value    
    }
```

Otherwisse, the immutable property has two differences:
* It starts with the `val` keyword.
* The variables of `val` type are read-only (don't have `set()` functions)

Kotlin properties use a backing field to hold a value in memory. A backing field is basically a class variable defined internally in the properties. A backing field is scoped to a property, which means that you can only access it through the get() or set() property functions.






### Declarative Programming Paradigm
With Views, the way to updating the UI is to walk the tree of UI widgets such as defining UI in XML, finding views from XML in code, and then calling the setter function (such as using function `findViewById()` and changes nodes by calling methods such as `button.setText(String)` to get UI like you want. 

Manipulating views manually can increase the likelihood of errors, such as if a pice of data is rendered in multiple places. In general, the software maintenance complexity grows with the number of views that require updating.

### Simple composable funtion
