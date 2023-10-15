![image](https://github.com/Xenoare/book-notes/assets/67181778/66bf3170-fc9d-4e33-ae68-d31390fbf352)### Introduction to Activities
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

### Recycler View
---
To help you bulid apps with list, android provides with `RecyclerView`. `RecyclerView` is designed to be very efficient even with large list, by reusing, or recycling, the views that have *scrolled off* the screen.
![image](https://github.com/Xenoare/book-notes/assets/67181778/ce835bbd-3813-448f-872f-3bc36ff5de74)

**1. Seting up the list data** 
Firstly, we can setup the list data for our `RecyclerView` app, in `stirings.xml`
```xml
<resources>
    <string name="app_name">Affirmations</string>
    <string name="affirmation1">I am strong.</string>
    <string name="affirmation2">I believe in myself.</string>
    <string name="affirmation3">Each day is a new opportunity to grow and be a better version of myself.</string>
    <string name="affirmation4">Every challenge in my life is an opportunity to learn from.</string>
    <string name="affirmation5">I have so much to be grateful for.</string>
    <string name="affirmation6">Good things are always coming into my life.</string>
    <string name="affirmation7">New opportunities await me at every turn.</string>
    <string name="affirmation8">I have the courage to follow my heart.</string>
    <string name="affirmation9">Things will unfold at precisely the right time.</string>
    <string name="affirmation10">I will be present in all the moments that this day brings.</string>
</resources>
```

**2. Making a data class**
We are making an object instance of `Affirmation` to represent one affirmation and contains the resource Id of the string with affirmation
```kotlin
// Affirmation.kt

package com.example.affirmation.model

data class Affirmation (val stringResourceId: Int)
```
When you create an instance of `Affirmation` you need to pass the resource ID for the affiirmation string.

**3. Create a data source class**
Data displayed in the app maybe come from different sources (such as from app project / internet). One way to do it is by making a new package and classes to take care for it (One can create a `data` package and `Datasource` class to take care of the list)
```kotlin
package com.example.affirmations.data

import com.example.affirmations.R
import com.example.affirmations.model.Affirmation

class Datasource {

    // The method is self return a list of Affirmation (an Instance of class Affirmation) from the strings.xml by passing the resource ID.
    fun loadAffirmations(): List<Affirmation> {
        return listOf<Affirmation>(
            Affirmation(R.string.affirmation1),
            Affirmation(R.string.affirmation2),
            Affirmation(R.string.affirmation3),
            Affirmation(R.string.affirmation4),
            Affirmation(R.string.affirmation5),
            Affirmation(R.string.affirmation6),
            Affirmation(R.string.affirmation7),
            Affirmation(R.string.affirmation8),
            Affirmation(R.string.affirmation9),
            Affirmation(R.string.affirmation10)
        )
    }
}
```

**4. Adding the RecyclerView to the layout**
There are a number of pices involved in creating a `RecyclerView`. The diagram below shows an overview.
* item - One data item of the list to display. Represents one Affirmation object in your app.
* Adapter - Takes data and prepares it for RecyclerView to display.
* ViewHolders - A pool of views for RecyclerView to use and reuse to display affirmations.
* RecyclerView - Views on screen
![image](https://github.com/Xenoare/book-notes/assets/67181778/e1d3d1a0-f867-4ab1-b566-a1b27b7a0682)

`RecyclerView` supports displaying items in different ways such as liniear list or a grid. Arraging the items is handled by a `LayoutManager`. Then, the final XML layout should like this
```xml
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        // Take care of the scrolling and how app display the items
        android:scrollbars="vertical"
        app:layoutManager="LinearLayoutManager" />

</FrameLayout>
```

**5. Implementing an Adapter**
Your app needs a way to take the data from `Datasource` and format such that `Affirmation` can be displayed as an item in `RecyclerView`.

Adapter is a design pattern that adapts the data into something that can be used by `RecyclerView`. In this case, you need an adapter that takes an `Affirmation` instance from the list returned by `loadAffirmations()`, and turns it into a list item view, so that it can be displayed in the `RecyclerView`.

When you run the app, `RecyclerView` uses the adapter to figure out how to display your data on screen. `RecyclerView` asks the adapter to create a new list item view for the first data item in your list. Once it has the view, it asks the adapter to provide the data to draw the item. This process repeats until the `RecyclerView` doesn't need any more views to fill the screen. If only 3 list item views fit on the screen at once, the `RecyclerView` only asks the adapter to prepare those 3 list item views (instead of all 10 list item views).


**Making a layout for items**
Each item in the RecyclerView has its own layout, which you define in a separate layout file. Since you are only going to display a string, you can use a TextView for your item layout.
```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/item_title"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```

**Creating an ItemAdapter class**
You need to add a parameter to the constructor of `ItemAdapter`, so that you can pass the list of affirmations into the adapter.

1. Add a parameter to the `ItemAdapter` constructor that is a val called dataset of type `List<Affirmation>`. Import Affirmation, if necessary.
2. Since the dataset will be only used within this class, make it private.
```kotlin
import com.example.affirmation.model.Affirmation

class ItemAdapter(private val dataset: List<Affirmation>) {}
```
The `ItemAdapter` needs information on how to resolve the string resources. This, and other information about the app, is stored in a `Context` object instance that you can pass into an ItemAdapter instance.
```kotlin
// Extend from the absract class RecyclerView.Adapter package
class ItemAdapter(private val context: Context, private val dataset: List<Affirmation>) : RecyclerView.Adapter<ItemAdapter.ItemViewHolder {}
```

**Creating a ViewHolder**.
`RecyclerView` doesn't interact directly with item views, but deals with `ViewHolders` instead. A `ViewHolder` represents a single list item view in `RecyclerView`, and can be reused when possible. A `ViewHolder` instance holds references to the individual views within a list item layout (hence the name "view holder"). This makes it easier to update the list item view with new data. View holders also add information that `RecyclerView` uses to efficiently move views around the screen.
```kotlin
class ItemAdapter(
    private val context: Context,
    private val dataset: List<Affirmation>
) : RecyclerView.Adapter<ItemAdapter.ItemViewHolder>() {

    class ItemViewHolder(private val view: View) : RecyclerView.ViewHolder(view) { 
        val textView: TextView = view.findViewById(R.id.item_title)
    }
}
```

Defaultly, the `ItemAdapter` needs to impelemnt 3 methods `getItemCount()`, `onCreateViewHolder()` and `onBindViewHolder()`.

**Implement `getItemCount()`**. This methods needs to return the size of your dataset. Your app's data is in the `dataset` property that you are passing into `ItemAdapter` constructor, and get this size with attribute `size`.
```kotlin
override fun getItemCount(): Int {
    return dataset.size
}
```

**Implement `onCreateViewHolder()`**. The `onCreateViewHolder()` method is called by the layout manager to create new view holders for the `RecyclerView` (when there are no existing view holders that can be reused). Remember that a view holder represents a single list item view.
- A `parent` parameter, which is the view group that the new list item view will be attached to as a child. The parent is the `RecyclerView`.
- A `viewType` parameter which becomes important when there are multiple item view types in the same `RecyclerView`. If you have different list item layouts displayed within the `RecyclerView`, there are different item view types. You can only recycle views with the same item view type. In your case, there is only one list item layout and one item view type, so you don't have to worry about this parameter.
1. In the `onCreateViewHolder()` method, obtain an instance of `LayoutInflater` from the provided context (`context` of the `parent`). The layout inflater knows how to inflate an XML layout into a hierarchy of view objects.
2. Once you have a `LayoutInflater` object instance, add a period followed by another method call to inflate the actual list item view. Pass in the XML layout resource ID `R.layout.list_item` and the `parent` view group. The third boolean argument is `attachToRoot`. This argument needs to be `false`, because `RecyclerView` adds this item to the view hierarchy for you when it's time.
3. In `onCreateViewHolder()`, return a new `ItemViewHolder` instance where the root view is adapterLayout.
```kotlin
override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ItemViewHolder {
    // create a new view
    val adapterLayout = LayoutInflater.from(parent.context)
        .inflate(R.layout.list_item, parent, false)

    return ItemViewHolder(adapterLayout)
}
```

**Implement onBindViewHolder()**. This method is called by the layout manager in order to replace the contents of a list item view. The `onBindViewHolder()` method has two parameter, an `ItemViewHolder` that previously created by the `onCreateViewHolder()` and an `int` that represent the current position in th list.
```kotlin
override fun onBindViewHolder(holder: ItemViewHolder, position: Int) {
    val item = dataset[position]
    holder.textView.text =  context.resources.getString(item.stringResourceId)
}
```

**6. Modify the MainActivity to use a RecyclerView**
```kotlin
package com.example.affirmations

import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.RecyclerView
import com.example.affirmations.adapter.ItemAdapter
import com.example.affirmations.data.Datasource

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Initialize data.
        val myDataset = Datasource().loadAffirmations()

        val recyclerView = findViewById<RecyclerView>(R.id.recycler_view)
        recyclerView.adapter = ItemAdapter(this, myDataset)

        // Use this setting to improve performance if you know that changes
        // in content do not change the layout size of the RecyclerView
        recyclerView.setHasFixedSize(true)
    }
}
```





