         ### Introduction to Activities
---
* > Kotlin Style Guide: https://developer.android.com/kotlin/style-guide

An `Activity` provides the window which your apps draws its UI. Typically, an `Activity` takes up the whole screen of your running app. Every app has one or more activites.

The top-level or first activity is often called the `MainActivity` and is provided by the project template.

For more complicated apps, there may be multiple screens and more than one activity. Each activity has a specific purpose.

For example, in photo gallery app, you could use `Activity` for displaying a grid of photos, a second `Activity` for viewing an individual photo and, third `Acitivity` for editing individual photo.
![image](https://github.com/Xenoare/book-notes/assets/67181778/a4e666e8-bae7-44fc-bde5-e918f0e1c373)

### Note
Android automatically assigns ID number to the resoureces in your app. (Roll button has a resource ID and etc. Resource IDs are of the form `R.<type>.<name>` such as `R.string.roll`. For view ID, the type is id (`R.id.button`).

### Project Lemonade
---
The app is build around simplicity and is organized in a single activity. The different states of the app are represented by something called *state machine*. The app's state is updated, along with any other needed variables and the UI is configured (setting the image and text) seperately once all the updates have been made.

1. Build the user interface
The lemonade app just requires a basic layout which consist of 2 views.
- A `TextView` which provides instruction to the user.
- An `ImageView` which shows a graphic based on the current state of the app (such that a lemon to be squeezed).
![image](https://github.com/Xenoare/book-notes/assets/67181778/d15777f8-bbd3-4b66-ae64-8d0bab44196c)

2. Make the app interactive
There are three basic things you'll need to implement to get the lemonade app working.
- Configure the `lemonImage`  `ImageView` to respond user input.
- Implement `clickLemonImage()` to update the app's state.
- Implement `setViewElements()` to update the UI based on the app's current state.

**Cofigure the ImageView**
Notice that are two event listener that need to be set.
- `setOnClickListener()` should update the app's state. The method to do this is `clickLemonImage()`.
- `setOnLongClickListener()` responds to events where the user long presses on an image (e.g. the user taps on the image and doesn't immediately release their finger). For long press events, a widget, called a snackbar, appears at the bottom of the screen letting the user know how many times they've squeezed the lemon. This is done with the `showSnackbar()` method.
```kotlin
lemonImage = findViewById(R.id.image_lemon_state)
        setViewElements()
        lemonImage!!.setOnClickListener {
            // TODO: call the method that handles the state when the image is clicked
            clickLemonImage()

        }
        lemonImage!!.setOnLongClickListener {
            // TODO: replace 'false' with a call to the function that shows the squeeze count
            showSnackbar()
        }
```

**Implement the `clickLemonImage()`**
This method is responsible for moving the app from the current state to the next and updating the variable needed.
```kotlin
    private fun clickLemonImage() {
        when (lemonadeState) {
            SELECT -> {
            }

            SQUEEZE -> {
            }

            DRINK -> {
            }

            RESTART -> {
            }
        }
        setViewElements()
    }
```

**Implement the setViewsElements()**
The setViewElements() method is responsible for updating the UI based on the app's state. The text and image should be updated with the values shown below to match the lemonadeState.
```kotlin
    private fun setViewElements() {
        val textAction: TextView = findViewById(R.id.text_action)
        when (lemonadeState) {
            SELECT -> {
                textAction.setText(R.string.lemon_select)
                lemonImage?.setImageResource(R.drawable.lemon_tree)
            ...
        }
```

### Chapter 2: Layout
---
**Create XML layouts for Android**
There are few UI elements that are provided by Android
- `EditText` - for entering and editing text.
- `TextView` - to display text like the service question and tip amout
- `RadioButton` - a selectable radio button for each tip option
- `RadioGroup` - to group the radio button option
- `Switch` - an on/off toggle for choosing whether to round up the tip or not.

You can describe the view hierarchy of UI elements of the screen. For example, a `ConstraintLyaout` (the parent) can obtain `Buttons`, `TextViews`, `ImageViews` or other views.
![image](https://github.com/Xenoare/book-notes/assets/67181778/10b04b76-c155-4891-8fc7-a3f9d07109b5)
Each UI element is represented by an XML element in the XML file.
```xml
<ConstraintLayout>
    <TextView
        text="Hello World!">
    </TextView>
</ConstraintLayout>
```
![image](https://github.com/Xenoare/book-notes/assets/67181778/5cd83a18-07c5-48b8-95e5-986ed7e124dc)

### Build the Layout in XML
---
1. Making an Text field for allowing user to enter and and the service question
```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout     
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/cost_of_service"
        android:layout_height="wrap_content"
        android:layout_width="match_parent"
        // That's why the constraint uses "start", so that it can work with either LTR or RTL languages. Similarly, constraints use "end" instead of right
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        // Since we need to input only numbers into the EditText
        android:inputType="number"
        android:hint="Cost of Service"/>

<TextView
        android:id="+id/service_question"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="How was the service?"
        // Setting the horizontal constraint to constraint its starting edge of the parent.
        app:layout_constraintStart_toStartOf="parent"
        // Setting the vertical constraint to constarint the top edge of the text
        app:layout_constraintTop_toBottomOf="@id/cost_of_service"
/>
  
</androidx.constraintlayout.widget.ConstraintLayout>
```

2. Add Radio Buttons
You can confirm that you can use a `RadioBUtton` UI element in your layout for each radio button you need. Furthermore, you also need to group the radio buttons within a `RadiGroup` because only one option can be selected at a time.
```kotlin
<RadioGroup
    android:id="@+id/tip_options"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@id/service_question">
    // Adding default value
    app:checkedButton="@id/option_twenty_percent"

   <RadioButton
        android:id="@+id/option_twenty_percent"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Amazing (20%)"
        />

// Now we adding 2 more radiobutton

   <RadioButton
       android:id="@+id/option_eighteen_percent"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Good (18%)" />

   <RadioButton
       android:id="@+id/option_fifteen_percent"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Okay (15%)" />


</RadioGroup>
```

3. Adding Switch for rounding up the tip
You cannot use `match_parent` for any view in a `ConstraintLayout`. Instead use `0dp` which means match constraints.
```kotlin
<Switch
    android:id="@+id/round_up_switch"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:checked="true"
    android:text="Round up tip?"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="@id/tip_options"
    app:layout_constraintTop_toBottomOf="@id/tip_options" />
```

4. Adding the button
```kotlin
<Button
   android:id="@+id/calculate_button"
   android:layout_width="0dp"
   android:layout_height="wrap_content"
   android:text="Calculate"
   app:layout_constraintTop_toBottomOf="@id/round_up_switch"
   app:layout_constraintStart_toStartOf="parent"
   app:layout_constraintEnd_toEndOf="parent" />
```

5. Adding the tip result
```kotlin
<TextView
    android:id ="@+id/tip_result"
    android:width = "wrap_content"
    android:height = "wrap_content"
    app:layout_constraintEnd_toEndOf = "parent"
    app:layout_constraintTop_toBottomOf = "@+id/calculate_button"
    android:text = "Tip Amount"  />
```


### View Binding
---
> Ref: https://developer.android.com/topic/libraries/view-binding

View banding is a feature that makes it easier to interacts with *views*. Once view binding is enable in module, it generates a binding class for each XML layout file present in the module. An instance of a binding class contains direct references to all views that have an ID to corresponding layout.

**Setup**
Firstly we can enable the view binding options via `build.gradle` file
```kotlin
buildFeatures {
        viewBinding = true
}
```

**Use View Binding in activities**
To set up view binding for an activity, perform this following steps `onCreate()` method:
1. Call the static `inflate()` method included in the generated binding class. This creates an instance of the binding class for the activity to use.
2. Get a reference to the root view by either calling the `getRoot()` method or using [Kotlin property syntax](https://kotlinlang.org/docs/properties.html#declaring-properties)
3. Pass the root view to `setContentView()` to make it active view on the screen.
```kotlin
private lateinit var binding: ResultProfileBinding

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    binding = ResultProfileBinding.inflate(layoutInflater)
    val view = binding.root
    setContentView(view)
}
```
Using view binding is so much more concise that often didn't need to create a variable that hold the reference for a `view`. just use directly from the binding object.
```kotlin
// Old way with findViewById()
val myButton: Button = findViewById(R.id.my_button)
myButton.text = "A button"

// Better way with view binding
val myButton: Button = binding.myButton
myButton.text = "A button"

// Best way with view binding and no extra variable
binding.myButton.text = "A button"
```

**Calculating the Tip**
1. First thing first, we can setup an event listener for the button (when the button is clicked, we call some listener function `calculateTip()`
```kotlin
binding.calculateButton.setOnClickListener{ calculateTip() }
```

2. Get in depth on the `calculateTip()` function. First we must store the Cost of Service within `EditText` attribute into some variable `stringInTextField`.
```kotln
var stringInTextField = binding.costOfService.text
```
since `.text` is an attribute of an `EditText` that is `Editable` (text can be changed). We must converts this to string with `toString()` methods -> `toDouble` to get the double value

3. Calculating the tip percentage, we get the `checkRadioButtonId` attribute of the `tipOptions` `RadioButton` and store in a variable. To know which radio is selected, we can use the id of each radio button (`R.id.option_twenty_percent, ...) and assign the variable
```kotlin
val selectedId = binding.tipOptions.checkRadioButtonId
val tipPercentage = when (selectedId) {
    R.id.option_twenty_percent -> 0.20
    R.id.option_eighteen_percent -> 0.18
    else -> 0.15
}
```

4. Rounding up the tip, for the Switch element, we can check on the `isChecked` attribute to see whether the switch is "on" or not.
```kotlin
val roundUp = binding.roundUpSwitch.isChecked
if (roundUp) {
    tip = kotlin.math.ceil(tip)
}
```

5. Formatting the tip. Android frameworks provides methods for formatting numbers as currency, the system automatically formats currency based on the language and other settings chosen on the phone. We can use a number formatter method for this.
```kotlin
val formattedTip = NumberFormat.getCurrencyInstance().format(tip)
```

6. Display the tip. The Android framework provides a mechanism for this called string parameters, so someone translating your app can change where the number appears if needed. Open the `strings.xml`
```xml
<string name="tip_amount">Tip Amount: %s</string>
```
The `%s` is where formatted currency will be inserted. Now set the text of the `tipResult`. Back in the `calculateTip()` method in `MainActivity.kt`, call `getString(R.string.tip_amount, formattedTip)` and assign that to the text attribute of the tip result `TextView`.
```kotlin
binding.tipResult.text = getString(R.string.tip_amount, formattedTip)
```

> Debug : https://developer.android.com/codelabs/basic-android-kotlin-training-tip-calculator?continue=https%3A%2F%2Fdeveloper.android.com%2Fcourses%2Fpathways%2Fandroid-basics-kotlin-unit-2-pathway-1%23codelab-https%3A%2F%2Fdeveloper.android.com%2Fcodelabs%2Fbasic-android-kotlin-training-tip-calculator#4

### Design and Color
---
**Material Design**

[Material Design](https://material.io/design/introduction) is inspired by the physical world and its textures, including how objects reflect light and cast shadows. It provides guidelines on how to build your app UI in a readable, attractive, and consistent manner. [Material Theming](https://material.io/design/material-theming/overview.html#material-theming) allows you to adapt Material Design for your app, with guidance on customizing colors, typography, and shapes. Material Design comes with a built-in, baseline theme that can be used as-is. You can then customize it as little, or as much, as you like to make Material work for your app.

**Defining a color**. A color can be represented as 3 hex numbers representing the red, green and blue (RGB) component.
![image](https://github.com/Xenoare/book-notes/assets/67181778/f1a93123-2ea7-468f-a782-3047c3e45a82)
```xml
<color name="black">#FF000000</color>
<color name="white">#FFFFFFFF</color>
```

**More about theme colors**
Different parts of the UI android apps use different colors. The theme system groups color into 12 named attributes related to color used in text, icon, and more.
![image](https://github.com/Xenoare/book-notes/assets/67181778/d0ddf4f5-1776-487f-a2f5-6d5445851bd8)

The "On" colors are used for text and icons drawn on the different surfaces
| #  | Name              | Theme Attribute       |
|----|-------------------|-----------------------|
| 1  | Primary           | colorPrimary          |
| 2  | Primary Variant   | colorPrimaryVariant   |
| 3  | Secondary         | colorSecondary        |
| 4  | Secondary Variant | colorSecondaryVariant |
| 5  | Background        | colorBackground       |
| 6  | Surface           | colorSurface          |
| 7  | Error             | colorError            |
| 8  | On Primary        | colorOnPrimary        |
| 9  | On Secondary      | colorOnSecondary      |
| 10 | On Background     | colorOnBackground     |
| 11 | On Surface        | colorOnSurface        |
| 12 | On Error          | colorOnError          |

We can defy our theme in Android studio
```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Theme.TipTime" parent="Theme.MaterialComponents.DayNight.DarkActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/purple_500</item>
        <item name="colorPrimaryVariant">@color/purple_700</item>
        <item name="colorOnPrimary">@color/white</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/teal_200</item>
        <item name="colorSecondaryVariant">@color/teal_700</item>
        <item name="colorOnSecondary">@color/black</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor" tools:targetApi="l">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
    </style>
</resources>
```
and then defy the colors in the color resource
```xml
<?xml version="1.0" encoding="utf-8"/>
<resources>
    <color name="purple_500"> #FFBB86FC </color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
</resources>
```

### Create more Polsihed user Experience    
---
[Material Components](https://material.io/components) are common UI widgets that make it easier to implement Material styling in your app. The documentation provides information for how to use and customize the Material Design Components. There are general Material Design guidelines for each component, and Android platform-specific guidance for the components that are available on Android. The labeled diagrams give you enough information to recreate a component if it happens to not exist on your chosen platform.

#### Later more on the Styling user experiance

### Using List in Kotlin
---
**Introduction to List**. A list is a collection of items in a specific order. There are two types of lists in kotlin.
- Read-only list: `List` cannot be modified after you create it.
- Mutable list: `MutableList` can be modifed after you create it.
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6)
```

**Creating a mutable list**. When you create a `MutableList` or `List`, Kotlin tries to infer what type of list contains from the argument passed.
```kotlin
val entrees: MutableList<String> = mutableListOf()
```

### Study Case Using List
---
Cases: When it comes to ordering food at a local restaurant, there's multiple items within a single order. Using list for storing information is a really neat idea. Given a sample distribution code
```kotlin
open class Item(val name: String, val price: Int)

class Noodles : Item("Noodles", 10)

class Vegetables : Item("Vegetables", 5) 

fun main() {
    val noodles = Noodles()
    val vegetables = Vegetables()
    println(noodles)
    println(vegetables)
}
```

When you print an object instance to the output, the object `toString()` method is called (defaultly every class is automatically inherits `toString()` method)
```kotlin
class Noodles : Item("Noodles", 10) {
   override fun toString(): String {
       return name
   }
}
```

**Handling many arguments**. In case there many arguments passed. We can modified our `Vegetable` class
```kotlin
class Vegetables(vararg val toppings: String) : Item("Vegetables", 5) {
    override fun toString(): String {
        return name + " " + toppings.joinToString()
    }
}
```
The `vararg` modifier allows to pass a variable number of arguments of the same type into function or constructor.

**Handling if there's no arguments passed out**. Update `toString()` method to return `Regular Vegetable` if there's no topping passed in.
```kotlin
class Vegetables(vararg val toppings: String) : Item("Vegetables", 5) {
    override fun toString(): String {
        if (toppings.isEmpty()) {
            return "Regular $name"
        } else {
            return name + " " + toppings.joinToString()
        }
    }
}
```

**Creating an Orders Item**. Encapsulate the login within an `Order` classs
```kotlin
class Order(val orderNumber: Int) {
   private val itemList = mutableListOf<Item>()

   // addItem takes a new Item and add into the itemList
   fun addItem(newItem: Item) {
    itemList.add(newItem)
   }

   fun addAll(newItems: List<Item>) {
    itemList.addAll(newItems)
   }

   fun print() {
    println("Order #${orderNumber}")
    var total = 0
    for (item in itemList) {
        println("${item}: $${item.price}")
        total += item.price
    }
    println("Total: $${total}")
   }
}
```






 
