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

**Define a constructor**

There are two main types of constructor in Kotlin:
1. **Primary constructor**. A class can only have one primary constructor (which is defined as part of class header).
2. **Secondary constructor**. A class can have multiple secondary constructor. The secondary constructor can initalize the class and has a body, which contain initialization logic.

![image](https://github.com/Xenoare/book-notes/assets/67181778/d3ad46ec-5857-499b-9d54-289cccc021d7)

For example if, you have and API that returns status code of `Int` `statusCode`. You can create a secondary constructor to convert `statusCode` parameter to string representation.
```kotlin
class SmartDevice(val name: String, val category: String){
    val deviceStatus = "online"

    constructor(name: String, category: String, statusCode: Int) : this(name, category){
        deviceStatus = when (statusCode) {
            0 -> "offline"
            1 -> "online"
            else -> "unknown"
        }
    } 
}
```

**Relationship between classes**

In Kotlin, all classes are final by default (which means you can't extand them, so you have to define the relationship between them).

The `open` keyword informs that the class is extandable
```kotlin
open class SmartDevice(val name: String, val category: String) {}
```
and you can create a subclass that extends the superclass
```kotlin
class SmartTvDevice(deviceName: String, deviceCategory: String) :
    SmartDevice(name = deviceName, category = deviceCategory) {}
```
Remember the `constructor` definition of `SmartTvDevice` doesn't specify whether the properties are mutable or immutable (which means that `deviceName` and `deviceCategory` parameters are literal `constructor` parameters intead of class properties). You won't be able to use them in class, but simply pass into the superclass constructor.

When you use inheritance, you establish  a relationship between two classes called `IS-A` relationship (an objects that instance from the superclass). And also `HAS-A` relationship (an object can own an instance of another class without actually being an instance of that class itself).
![image](https://github.com/Xenoare/book-notes/assets/67181778/9c3b538a-7379-4533-ab16-91ff0258d6bb)

1. IS-A relationship
When you specify an IS-A relationship between the SmartDevice superclass and SmartTvDevice subclass, it means that whatever the SmartDevice superclass can do, the SmartTvDevice subclass can do.
```kotlin
// Smart TV IS-A smart device.
class SmartTvDevice : SmartDevice() {}
```

2. HAS-A relationship
The HAS-A relationship between two classees is also referred to as composition. You can have a instance of another class (for example, home is contains a smart device or in other words, the home has a smart device)
```kotlin
// Smart Home HAS-A smart TV device and smart light.
class SmartHome(
    val smartTvDevice: SmartTvDevice,
    val smartLightDevice: SmartLightDevice
) {
```

**Override superclass methods from superclass**

The `override` keyword informs that the kotlin runtime to execute the code enclosed in the method define in the subclasss. Let's say we have a super class `SmartDevice`
```
open class SmartDevice {
    ...
    var deviceStatus = "online"

    open fun turnOn() {
        // function body
    }

    open fun turnOff() {
        // function body
    }
}
```
The subclass can access the `turnOn()` and `turnOff()` methods with `override` keyword and customize the function desired, this is an example of polymorphism where method on a variable and type are depending on what actual value of the variable is.

**Reusing superclass code in subclasses with `super` keyword**
To call the overriden method from the superclass, you need to use the `super` keyword. Instead of using a `.`. operator between the object and method, you need to use `super` keyword which informs the kotlin compiler to call on the superclass instad of the subclass.
![image](https://github.com/Xenoare/book-notes/assets/67181778/8e03ae6b-2206-4228-9e83-a961615e7f9b)
```kotlin
    override fun turnOn() {
        super.turnOn()
        println("Smart TV turned on. Speaker volume set to $speakerVolume.")
    }
```

**Override superclass properties from subclasses**

Property is being overridden with a new value in the Subclass, but it's not actually reassigning the property. Instead, it's shadowing the property from the superclass with a new value specific to the subclass.
```kotlin
open class Superclass {
    open val property: String = "Superclass"
}

class Subclass : Superclass() {
    override val property: String = "Subclass"
}
```

**Visibility Modifier**

Visibility modifier play an important role to achive encapsulation:
- In a class, they let to hide properties and methods from unauthorized access outside the class.
- In a package, they let you hide the classes and interfaces from unauthorized access outside the package.

Kotlin provides four visibility modifier
1. `public`. Default visibility modifier, makes the declaration accessible everywhare.
2. `private`. Makes the declaration accessible in the same class or source file.
3. `protected`. Makes the declaration accessble in subclasess.
4. `internal`. Makes the declaration accessible in the same module. The internal modifier is similar to private, but you can access internal properties and methods from outside the class as long it's being accessed in the same module.

**Define property delegates**

You can reuse the range-check code in setter with delegates. Instead of using field, and a getter and setter function to manage the value, the delegate manages it.

The syntax to create a property delegates starts with the declaration of a variable followeb by the `by` keyword, and the delegate object handle the getter and seetter functions for the property.
![image](https://github.com/Xenoare/book-notes/assets/67181778/bf7607aa-7679-45f7-b859-f0f1d2f15bb5)

**Function Types and Lambda Expression**

### Declarative Programming Paradigm
With Views, the way to updating the UI is to walk the tree of UI widgets such as defining UI in XML, finding views from XML in code, and then calling the setter function (such as using function `findViewById()` and changes nodes by calling methods such as `button.setText(String)` to get UI like you want. 

Manipulating views manually can increase the likelihood of errors, such as if a pice of data is rendered in multiple places. In general, the software maintenance complexity grows with the number of views that require updating.

### Simple composable funtion
