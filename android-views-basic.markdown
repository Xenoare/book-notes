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

### Displaying a list of image
---
First thing first, we download and insert an image into the `drawable` resources. Then open the data class `Afirmation`, remember that `Affirmation` data class is hold for a value for resources ID. Both `stringResourceId` and `imageResourceId` are integer values. To avoid accidentally pass arguments in wrong order, we can use `Resource annotation`. `Annotations` are useful because they add additional info to classes, methods, or parameters. Annotations are always declared with an @ symbol. In this case, add the @StringRes annotation to your string resource ID property and @DrawableRes annotation to your drawable resource ID property.

Make sure to imports `androidx.annotations.DrawableRes` and `androidx.annotationsStringRes`
```kotlin
package com.example.affirmations.model

import androidx.annotation.DrawableRes
import androidx.annotation.StringRes

data class Affirmation(
   @StringRes val stringResourceId: Int,
   @DrawableRes val imageResourceId: Int
)
```
Then in the `Datasource` class, we can modify the `loadAffirmations()` method
```kotlin
fun loadAffirmations(): List<Affirmation>{
        return listOf<Affirmation> (
            Affirmation(R.string.affirmation1, R.drawable.image1),
            Affirmation(R.string.affirmation2, R.drawable.image2),
            Affirmation(R.string.affirmation3, R.drawable.image3),
            Affirmation(R.string.affirmation4, R.drawable.image4),
            Affirmation(R.string.affirmation5, R.drawable.image5),
            Affirmation(R.string.affirmation6, R.drawable.image6),
            Affirmation(R.string.affirmation7, R.drawable.image7),
            Affirmation(R.string.affirmation8, R.drawable.image8),
            Affirmation(R.string.affirmation9, R.drawable.image9),
            Affirmation(R.string.affirmation10, R.drawable.image10)
        )
} 
```

### Activities and Intents
---
There are two types of intent (**implicit** and **explicit**). An **explicit intent** is highly specific, where you know the exact activities to be launched, often as creen in your own app.

Whereas **Implicit intent** is a bit more abstract, where you tell the system the type of action such as opening a link, composing an email, etc.
![image](https://github.com/Xenoare/book-notes/assets/67181778/960c3899-4b4d-4d87-9947-228439d87c79)

* Set up Explicit Intent
---
Creating an intent take just a few steps
1. Open `Adapter.kt` and navigate to `onBindViewHolder()` method and set the `onClickListener` for `holder.button`
```kotlin
holder.button.setOnClickListener {

// Get a reference to the context
val context = holder.itemView.context

// Create an Intant, and passing in the context and class name of the destination activity
val intent = Intent(context, Activity::class.java)

// call putExtra method, passing "letter" as the first argument and the button text as the second argument.
intent.putExtra("letter", holder.button.text.toString())

// call the StartActivity method on the context object, passing an intent
context.startActivity(intent)
}
```
Remember that an intent is a simply set of instruction - there's no `instance of the destination activity just yet`. Instead, an extra is a `piece of data`, that `is given a name to be retrived later`.

* Set up the Activity
---
In the `onCreate` method of the Activity, we can retrive the `letterId` passed in from the `intent`
```kotlin
val letterId = intent?.extras?.getString("letter").toString()
```
The extras poroperties is of type `Bundle` and this provides a way to access all extras passed into the intent.

* Set up Implicit Intent
---
1. For this context, we will perform a Google search for the keyword. The first search result will be a dict definition of the word. Since a URL is used for every search, then it's a good idea to define as a `constant` in `companion object`.
```kotlin
companion object {
   const val LETTER = "letter"
   const val SEARCH_PREFIX = "https://www.google.com/search?q="
}
```
2. Modifty the `WordAdapter` and creating an `Uri` foe the search query. When calling `parse()` to create a `Uri` from a string, we need to use string formatting so that word is appended to `SEARCH_PREFIX`.
```kotlin
holder.button.setOnClickListener {
        val queryUrl: Uri = Uri.parse("${Activity.SEARCH_PREFIX}${item}")
}
```
3. Init a new intent object
```kotlin
val intent = Intent(Intent.ACTION_VIEW, queryURL)
```
`ACTION_VIEW` is a generic intent that takes a URI (in your case is a web address). The system then knows how to process this intent by opening the URI in the user's web browser. There are few other intent types include:
- `CATEGORY_APP_MAPS` – launching the maps app
- `CATEGORY_APP_EMAIL` – launching the email app
- `CATEGORY_APP_GALLERY` – launching the gallery (photos) app
- `ACTION_SET_ALARM` – setting an alarm in the background
- `ACTION_DIAL` – initiating a phone call

* Set up Menu and Icons
---
We will create an app bar for this application
1. First we need import two icon that represent grid and view list
![image](https://github.com/Xenoare/book-notes/assets/67181778/9d727983-a79a-48c3-8cc2-4c421afcfd8e)
2. Make an app bar layout. we can make this in the res folder `Menu` and add file `layout_menu.xml`
```kotlin
<menu xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"> 
   <item android:id="@+id/action_switch_layout" // To be referenced in the code
       android:title="@string/action_switch_layout"
       android:icon="@drawable/ic_linear_layout" // set the icon
       app:showAsAction="always" />
</menu>
```

* Implement menu button
---
1. First, we need a status to keep the layout button
```kotlin
private var isLinearLayoutManager = true
```
2. Then we can change our views by simply using layout manager
```kotlin
private fun chooseLayout() {
    if (isLinearLayoutManager) {
        recyclerView.layoutManager = LinearLayoutManager(this)
    } else {
        recyclerView.layoutManager = GridLayoutManager(this, 4)
    }
    recyclerView.adapter = LetterAdapter()
}
```
3. Then we will change the icon based on the which layout is used
```kotln
private fun setIcon(menuItem: MenuItem?) {
   if (menuItem == null)
       return

   // Set the drawable for the menu icon based on which LayoutManager is currently in use

   // An if-clause can be used on the right side of an assignment if all paths return a value.
   // The following code is equivalent to
   // if (isLinearLayoutManager)
   //     menu.icon = ContextCompat.getDrawable(this, R.drawable.ic_grid_layout)
   // else menu.icon = ContextCompat.getDrawable(this, R.drawable.ic_linear_layout)
   menuItem.icon =
       if (isLinearLayoutManager)
           ContextCompat.getDrawable(this, R.drawable.ic_grid_layout)
       else ContextCompat.getDrawable(this, R.drawable.ic_linear_layout)
}
```

For the app can actuallly use the menu. We need to override tow more methods
* `onCreateOptionsMenu` where you inflate the options menu and performs any addiontal setup
* `onOptionsItemSelected` where you'll actually call `chooseLayout()` when the button is selected.

1. Override `onCreateOptionsMenu`
```kotlin
override fun onCreateOptionsMenu(menu: Menu?): Boolean {
   menuInflater.inflate(R.menu.layout_menu, menu)

   val layoutButton = menu?.findItem(R.id.action_switch_layout)
   // Calls code to set the icon based on the LinearLayoutManager of the RecyclerView
   setIcon(layoutButton)

   return true
}
```
2. Implement `onOptionsItemSelected`
```kotlin
override fun onOptionsItemSelected(item: MenuItem): Boolean {
   return when (item.itemId) {
       R.id.action_switch_layout -> {
           // Sets isLinearLayoutManager (a Boolean) to the opposite value
           isLinearLayoutManager = !isLinearLayoutManager
           // Sets layout and icon
           chooseLayout()
           setIcon(item)

           return true
       }
       //  Otherwise, do nothing and use the core event handling

       // when clauses require that all possible paths be accounted for explicitly,
       //  for instance both the true and false cases if the value is a Boolean,
       //  or an else to catch all unhandled cases.
       else -> super.onOptionsItemSelected(item)
   }
}
```

### Fragment
---
A fragmetn is a reusable piece of UI; fragments can be reused and embedded in ore or more activities.

You can even show multiple fragments at once on a single screen, such as a master-detail layout for tablet devices. In the example below, both the navigation UI on the left and the content on the right can each be contained in a separate fragment. Both fragments exist simultaneously in the same activity.
![image](https://github.com/Xenoare/book-notes/assets/67181778/4def9234-d5a7-43bb-9d14-0f5d0e196932)

Fragment is simply a reusbale piece of your app's interface. Like activiteis, fragments have a lifecycle and can respond to user input. `A fragment is always contained within the view hierarchy when it is shown onscreen`. 

The fragment lifecycle has five states, represented by the [Lifecycle.State](https://developer.android.com/reference/kotlin/androidx/lifecycle/Lifecycle.State) enum.
* INITIALIZED: A new instance of the fragment has been instantiated.
* CREATED: The first fragment lifecycle methods are called. During this state, the view associated with the fragment is also created.
* STARTED: The fragment is visible onscreen but does not have "focus", meaning it can't respond to user input.
* RESUMED: The fragment is visible and has focus.
* DESTROYED: The fragment object has been de-instantiated.

Also similar to activities, `Fragment ` class provides many methods that you can override to repspond to lifecycle events.
* `onCreate()`: The fragment has been instantiated and is in the `CREATED` state. However, its corresponding view has not been created yet.
* `onCreateView()` This method is where you inflte the layout. The fragment has entered the `CREATED` state.
* `onViewCreated()`: This is called after the view is created. In this method, you would typically bind specific views to properties by calling `findViewById()`.
* `onStart()`: The fragment has entered the `STARTED` state.
* `onResume()`: The fragment has entered the `RESUMED` state and now has focus (can respond to user input).
* `onPause()`: The fragment has re-entered the `STARTED` state. The UI is visible to the user.
* `onStop()`: The fragment has re-entered the `CREATED` state. The object is instantiated but is no longer presented on screen.
* `onDestroyView()`: Called right before the fragment enters the `DESTROYED` state. The view has already been removed from memory, but the fragment object still exists.
* `onDestroy()`: The fragment enters the `DESTROYED` state.
![image](https://github.com/Xenoare/book-notes/assets/67181778/22525a0d-cfab-4b1c-9f4d-e0a81eda6c56)

The lifecycle states and callbacks methods are quite similar with Activities. However, keep in mind the difference with the `onCreate()` method. With activities, you `would use this method to inflate the layout and bind views`. However, in the `fragment` lifecycle, `onCreate()` is called before the view is created, so you can't inflate the layout here. Instead, you do this in `onCreateView()`. Then, after the view has been created, the `onViewCreated()` method is called, where you can then `bind properties to specific views`.

* Implement LetterListFragment
---
To implement view binding in `LetterLlistFragment`, first we need to get a nullable reference to `FragmentLetterListBinding`. `Binding classes like this are generated by Android Studio` for `each layout file`.

The type should be `FragmentLetterListBinding?` and it should have an initial value of `null`.

Why make it nullable? Because you can't inflate the layout until `onCreateView()` is called. There's a period of time in-between when the instance of `LetterListFragment` is created (when its lifecycle begins with `onCreate()`) and when this property is actually usable. Also keep in mind that fragments' views can be created and destroyed several times throughout the fragment's lifecycle. For this reason you also need to reset the value in another lifecycle method, `onDestroyView()`.

1. Make a reference to the FragmentLetterListBinding
```kotlin
private var _binding: FragmentLetterListBinding? = null
```
2. Create a new property, called binding
```kotlin
private val binding get() = _binding!!
```
`get()` is the property "get-only". For reference the property name with prefix _. This typically means that the property isn't intended to be accessed directly.
3. To display the options menu, override the `onCreate()`. And the call the `setHasOptionsMenu()` and passing to true.
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
   super.onCreate(savedInstanceState)
   setHasOptionsMenu(true)
}
```
4. Inflate the layout with in `onCreateView()` by inflating the view, and setting the value of `_binding` and returning the root view.
```kotlin
override fun onCreateView(
   inflater: LayoutInflater, container: ViewGroup?,
   savedInstanceState: Bundle?
): View? {
   _binding = FragmentLetterListBinding.inflate(inflater, container, false)
   val view = binding.root
   return view
}
```
5. Add property for the recycler view under `binding property`
```kotlin
private lateinit var recyclerView: RecyclerView
```
6. Set the `recyclerView` property in `onViewCreated()` and call the `chooseLayout()`
```kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
   recyclerView = binding.recyclerView
   chooseLayout()
}
```
7. Set `onDestroyView()` by reseting the `_binding` property to `null`, as the view no longer exist.
```kotlin
override fun onDestroyView() {
    super.onDestroyView()
    _binding = null
}
```
8. The only other thing to note is there are some subtle differences with the `onCreateOptionsMenu()` method when working with fragments. While the Activity class has a global property called `menuInflater`, Fragment does not have this property. The menu inflater is instead passed into `onCreateOptionsMenu()`. Also note that the `onCreateOptionsMenu()` method used with fragments doesn't require a return statement.
```kotlin
override fun onCreateOptionsMenu(menu: Menu, inflater: MenuInflater) {
   inflater.inflate(R.menu.layout_menu, menu)

   val layoutButton = menu.findItem(R.id.action_switch_layout)
   setIcon(layoutButton)
}
```
9. Move the remaining code from the MainActivity. The only diff to note that, unlinke an activity, a fragment is not a [Context](https://developer.android.com/reference/android/content/Context). So you can't pass in `this` (referring to the fragment object) as the layout manager's context. However, fragment provide a `context` property you can use instead.
```kotlin
private fun chooseLayout() {
    when (isLinearLayoutManager) {
        true -> {
            recyclerView.layoutManager = LinearLayoutManager(context_
            recyclerView.adapter = LetterAdapter()
        }
        false -> {
            recyclerView.layoutManager = GridLayoutManager(context, 4)
            recyclerView.adapter = LetterAdapter()
        }
    }
}

// The argument is icon id
private fun setIcon(menuItem: MenuItem?) {
    if (menuItem == null) {
        return
    }
    menuItem.icon =
        if (isLinearLayoutManager) 
            ContextCompat.getDrawable(this.requireContext(), R.drawable.ic_grid_layout)
       else ContextCompat.getDrawable(this.requireContext(), R.drawable.ic_linear_layout)
}

overrride fun onOptionsItemSelected(item: MenuItem): Boolean {
    return when(item.itemId) {
        R.id.action_switch_layout -> {
           isLinearLayoutManager = !isLinearLayoutManager
           chooseLayout()
           setIcon(item)

           return true
       }

       else -> super.onOptionsItemSelected(item)
    }
}
```
Remember that [requireContext()](https://developer.android.com/reference/androidx/fragment/app/Fragment#requireContext()) returns the Context this fragments is currently associated with.


* Jetpack Navigation Component
---
Android Jetpack provides the *Navigation component* to help handle any navigation implementation.

Th navigation component has three key parts which you'll use to implement navigation.
* Navigation Graph: The navigation graph is an XML file that provides a visual representation of navigation in your app. The file consists of destinations which correspond to individual activities and fragments as well as actions between them which can be used in code to navigate from one destination to another. Just like with layout files, Android Studio provides a visual editor to add destinations and actions to the navigation graph
* `NavHost`: A `NavHost` is used to display destinations from a navigation graph within an activity. When you navigate between fragments, the destination shown in the `NavHost` is updated. You'll use a built-in implementation, called `NavHostFragment`, in your MainActivity.
* `NavController`: The `NavController` object lets you control the navigation between destinations displayed in the `NavHost`. When working with intents, you had to call `startActivity` to navigate to a new screen. With the Navigation component, you can call the NavController's `navigate()` method to swap the fragment that's displayed. The NavController also helps you handle common tasks like responding to the system "up" button to navigate back to the previously displayed fragment.

* Navigation Dependency
---
In the project-level `build.gradle` file. in **buildscript > ext** below `material_version`. Set the `nav_version` equal to `2.5.2`
```kotlin
buildscript {
    ext {
        appcompat_version = "1.5.1"
        constraintlayout_version = "2.1.4"
        core_ktx_version = "1.9.0"
        kotlin_version = "1.7.10"
        material_version = "1.7.0-alpha2"
        nav_version = "2.5.2"
    }

    ...
}
```
also add this dependencies
```kotlin
implementation "androidx.navigation:navigation-fragment-ktx:$nav_version"
implementation "androidx.navigation:navigation-ui-ktx:$nav_version"
```

* Safe Args Plugin
---
Before you start implementing the Navigation component into the Words app, you'll also add something called `Safe Args`—a Gradle plugin that will assist you with type safety when passing data between fragments.
1. In the top-level `build.gradle` file. add this classpath
```kotlin
classpath "androidx.navigation:navigation-safe-args-gradle-plugin:$nav_version"
```
2. in the app-level `build-gradle` file. within `plugins` at the top, add `android.navigation.safeargs.kotlin`
```kotlin
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-kapt'
    id 'androidx.navigation.safeargs.kotlin'
}
```

* Using Navigation Graph
---
The Navigation Graph (NavGraph) is a virtual mapping of your apps navigation. Each screen, of fragment in your case, become possible "destination" that can be navigated to. A `NavGraph` can be represented by XML file showing each destination relates to one another.

Use FragmentContainerView in MainActivity
---
Because your layouts are now contained in `fragment_letter_list.xml` and `fragment_word_list.xml`, your `activity_main.xml` file no longer needs to contain the layout for the first screen in your app. Instead, you'll repurpose `MainActivity` to contain `FragmentContainerView` to act as the `NavHost` for your fragments.
1. Replace the content of `FrameLayout` in **activity_main.xml** that is `androidx.recyclerview.widget.RecyclerView` with a `FragmentContainerView`. Give it an ID of nav_host_fragment and set its height and width to `match_parent` to fill the entire frame layout.
```xml
<androidx.fragment.app.FragmentContainerView
   android:id="@+id/nav_host_fragment"
   android:layout_width="match_parent"
   android:layout_height="match_parent" />
```
2. Below the id attribute, add a name attribute and set it to `androidx.navigation.fragment.NavHostFragment`. While you can specify a specific fragment for this attribute, setting it to `NavHostFragment` allows your `FragmentContainerView` to navigate between fragments.
```xml
android:name="androidx.navigation.fragment.NavHostFragment"
```
3. Below the `layout_height` and `layout_width` attributes, add an attribute called `app:defaultNavHost` and set it equal to `"true"`. This allows the fragment container to interact with the navigation hierarchy. For example, if the system back button is pressed, then the container will navigate back to the previously shown fragment, just like what happens when a new activity is presented.
```xml
app:defaultNavHost="true"
```
4. Add an attribute called `app:navGraph` and set it equal to `"@navigation/nav_graph"`. This points to an XML file that defines how your app's fragments can navigate to one another. For now, the Android studio will show you an unresolved symbol error. You will address this in the next task.
```xml
app:navGraph="@navigation/nav_graph"
```
5. Finally, because you added two attributes with the app namespace, be sure to add the `xmlns:app` attribute to the `FrameLayout`.
```xml
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   tools:context=".MainActivity">
```

* Set Up Navigation Graph
---
Add a navigation graph file name `nav_graph.xml` as the name you set for the `app:navGraph` attribute under the `navigation` directory
![image](https://github.com/Xenoare/book-notes/assets/67181778/d6a8f179-2b64-4827-9d18-cdffbc22a217)

* Create a Navigation action
---
To create a navigation action between the `letterListFragment` to the `wordListFragment` destinations, hover your mouse over the `letterListFragment` destination and drag from the circle that appears on the right onto the wordListFragment destination.
![image](https://github.com/Xenoare/book-notes/assets/67181778/346a53e7-821e-462f-be23-739f5c4a2b9c)
You should see an `action` arrows between those two fragments, and the name of this action is `action_letterListFragment_to_wordListFragment` that can be referenced.

* Specify Arguments for WordListFragment
---
When navigating between activities using an intent, you specified an "extra" so that the selected letter could be passed to the `wordListFragment`. Navigation also supports passing parameters between destinations and plus does this in a type safe way.
![image](https://github.com/Xenoare/book-notes/assets/67181778/1db54d72-08b1-4020-877a-bfd91ba14400)

* Perform the Navigation Action
---
1. Delete the contents of the button's `setOnClickListener()`. Instead, you need to retrieve the navigation action you just created. Add the following to the `setOnClickListener()`.
```kotlin
val action = LetterListFragmentDirections.actionLetterListFragmentToWordListFragment(letter = holder.button.text.toString())
```
`LetterListFragmentDirections` lets you refer to all possible navigation paths starting from the `letterListFragment`.

Once you have a reference to your navigation action, simply get a reference to your NavController (an object that lets you perform navigation actions) and call navigate() passing in the action.
```kotlin
holder.view.findNavController().navigate(action)
```

* Configure MainActivity
---
1. Create a `navController` property that marked as `lateinit` since it will be set in `onCreate`
```kotlin
private lateinit var navController: NavController
```
2. Then, after the call to `setContentView()` in `onCreate()`, get a reference to the `nav_host_fragment` (this is the ID of your `FragmentContainerView`) and assign it to your `navController` property.
```kotlin
val navHostFragment = supportFragmentManager
    .findFragmentById(R.id.nav_host_fragment) as NavHostFragment
navController = navHostFragment.navController
```
3. Then in `onCreate()`, call `setupActionBarWithNavController()`, passing in `navController`. This ensures action bar (app bar) buttons, like the menu option in `LetterListFragment` are visible.
```kotlin
setupActionBarWithNavController(navController)
```
4. Finally, implement `onSupportNavigateUp()`. Along with setting `defaultNavHost` to true in the XML, this method allows you to handle the up button. However, your activity needs to provide the implementation.
```kotlin
override fun onSupportNavigateUp(): Boolean {
   return navController.navigateUp() || super.onSupportNavigateUp()
}
```

* Getting Arguments in WordListFragment
---
Accessing safe arguments is pretty straightforward, and you don't have to wait until `onViewCreated()` is called either.
1. In `WordListFragment`, create a `letterId` property. You can mark this as lateinit so that you don't have to make it nullable
```kotlin
private lateinit var letterId: String
```
2. Then override `onCreate()` and add following:
```kotlin
override fun onCreate(savedInstances: Bundle?) {
    super.onCreate()

    arguments?.let {
        letterId = it.getString(LETTER).toString()
    }
}
```
Because it's possible for **arguments** to be optinal, notice you call `let()` and pass in a lambda. If the arguments are null, then the lambda will not execute.

What exactly is a `Bundle?` Think of it as a key-value pair used to pass data between classes, such as activities and fragments. Actually, you've already used a bundle when you called `intent?.extras?.getString()` when performing an intent in the first version of this app. Getting the string from arguments when working with fragments works exactly the same way.

3. Finally, you can access the letterId when you set the recycler view's adapter. Replace `activity?.intent?.extras?.getString(LETTER).toString()` in` onViewCreated()` with `letterId`.
```kotlin
recyclerView.adapter = WordAdapter(letterId, requireContext())
```

## Architecture Component
Notes: 
+ [Additional github project](https://github.com/google-developer-training/android-basics-kotlin-unscramble-app/tree/starter)

Table of Contents 
+ [Common Architecture Principles](#common-architectural-principles)
+ [Store Data in ViewMode](#store-data-in-viewmodel)
+ [Setup ViewModel](#setup-a-viewmodel)
+ [Use LiveData with ViewModel](#use-livedata-with-viewmodel)

#### Common Architectural Principles
---
> Ref. https://developer.android.com/topic/architecture

An app architectue defines the boundaries between parts of the app and the responsibillites each part should have. In order to meet the needs mentioned above, you should design your app architecture to follow a few specific principles.
1. Separation of concerns <br>
The most important principle to follow is [Separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns). It's a common mistake to write all your code in `Activity` or `Fragment`. These UI-based classes should only contain logic that handles UI and operating system interaction, by keeping these classes as lean as posibble, you can avoid many problems related to the component lifecycle, and improve the testability of these classes.
2. Drive UI from data moodels <br>
Another important principle is that you should drive your UI from data models, preferably persistent models. Data models can represents the data of an app.
They are indepenent from the UI element and the other components in your app. This means that they are not tied to the UI and app component lifecycle, but will still be destroyed when the OS decided to remove the app's process from memory. <br>
Persistent models are ideal for the following reasons:
    * Your users don't lose data if the Android OS destroys your app to free resources.
    * Your app continous to work in casees when a network connection is flaky or not available.
3. Single source of truth <br>
When a new data type is defined in your app, you should assing a `Single Source of Truth` (SSOT) to it. The SSOT is the owner of that data, and only the SSOT can modify or mutate it. In an offline-first application, the source of truth for appliction data is typically a database. In some other cases, the source truth can be a ViewModel or even the UI.
4. Undirectional Data Flow <br>
The principle of SSOT, is often used in Undirectional Data Flow (UDF) pattern. In UDF, **state** flows in only one direction. The **events** that modify the data flow in the opposite direction. <br>
In Android, state or data usually flow the higher-scoped types of the hierarchy to the lower-scoped ones. Events are usually triggred from the lower-scoped types until they reach the SSOT for the corresponding data type. <br>
For example, application data usually flows from data sources to the UI. User events such as button presses flow the UI to th SSOT where the application data is modified and exposed in an immmutable type.

#### Store Data in ViewModel
---
Model are components that are responsible for handling the data for an app. They're independent from the `Views` and app component. <br>
The main classes or components in Android Architecture are UI Controller (`activity`/`fragment`), `ViewModel`, `LiveData` and `Room` (Livedata and Room later).

![image](https://github.com/Xenoare/book-notes/assets/67181778/2b54af9e-23ba-490b-81e0-50791ce4655d)

1. UI Controller <br>
Activities and Fragments are UI controllers. UI controllers control the UI by drawing views on the screen, and anything else related to the UI that user interects with (Data in the app or any decision-making logic about data should not be in the UI controller classes).
2. ViewModel <br>
The `ViewModel` stores the app related data that isn't destroyed when activity or fragment is **destroyed** and **recreated** by Android framework. `ViewModel` objects are automatically retained (they are not destroyed like the activity or a fragment instance)

#### Setup a ViewModel
---
To associate a `ViewModel` to a UI controller, create a `reference` (object) to the `ViewModel` inside the UI controller.
```kotlin
// Fragment.kt

// Initialize the GameViewModel using kotlin property delegate
private val viewModel: GameViewModel by viewModels()
```

* **Kotlin Propery Delegate** <br>
In kotlin, each mutable (`var`) property has default setter and getter function autmatically generated with it. Rather than read-only property (`val`) that only have getter function is generated by default. <br>
**Property delegation** in kotlin helps you to handoff the getter-setter responsibility to a different class. The instance class (*delegate class*) provides **getter** and **setter** function fo the property and handles its changes. <br>
A delegate property is defined using `by` clause and delegate class instance:
    ```kotlin
    // Syntax for property delegation
    var <property-name> : <property-type> by <delegate-class>()
    ```
  *Let's* say that if the initialization of view model using default             `GameViewModel` constructor as below. 
    ```kotlin
    private val viewModel = GameViewMoel()
    ```
    Then the app will lose the state of the `viewModel` *reference* when the device goes through a configuration change (For example, if you rotating the device, then the activity is **destroyed** and **created** again, and you'll have a new view model instance with the initial state again). <br>
    The `delegate` class creates the `viewModel` object for you on the first access, and retains its value through configuration changes and returns when requested.

* **Move data to the ViewModel** <br>
you can't make the visibility modifiers of the properties `public` —the data should not be editable by other classes. This is risky because an outside class could change the data in unexpected ways that don't follow the game rules specified in the view model. <br>
Inside the ViewModel, the data should be editable, so they should be private and var. From outside the ViewModel, data should be readable, but not editable, so the data should be exposed as public and val. To achieve this behavior, Kotlin has a feature called a [backing property](https://kotlinlang.org/docs/reference/properties.html#backing-properties).

  1. Backing property <br>
    A backing property allows you to return something from a `getter` other than the object. For getter and setter methods, you could `override` one or both of these methods and **provide your own custom behavior**. To implement a `backing property`, you will override the getter method to return a read-only version of your data.
        ```kotlin
        // Declare private mutable variable that can only be modified
        // within the class it is declared.
        private var _count = 0 
        
        // Declare another public immutable field and override its getter method. 
        // Return the private property's value in the getter method.
        // When count is accessed, the get() function is called and
        // the value of _count is returned. 
        val count: Int
           get() = _count
        ```
        Let's break the code.
     * Inside the `ViewModel` class. The property _count is private and mutable. Hence, it is only accessible and editable within the ViewModel class. The convention is to prefix the private property with an underscore.
     * Outside the `ViewModel` class. The default visibility modifier in Kotlin is `public`, so `count` is public and accessible from other classes like UI controllers. Since only the `get()` method is being **overridden**, this property is immutable and read-only. When an outside class accesses this property, it returns the value of `_count` and its value can't be modified. This **protects the app data** inside the `ViewModel` from unwanted and unsafe changes by external classes, but it allows external callers to safely access its value.
    
     in `GameViewMode` we can change the `currentScrambleWord` declaration to add a backing property. and then Now `_currentScrambleWord` is accessible and editbale only within `GameViewModel`. The UI controller, `GameFragment` can read its value using read-only property
     ```kotlin
     private var _currentScrambledWord = "test"
     val currentScrambledWord: String
         get() = _currentScrambledWord
     ```

* **The lifecycler of a ViewModel** <br>
The framework keeps the `ViewModel` alive as long as the scope of the activity or fragment is alive. A `ViewModel` is not destroyed if its owner is destroyed for a configuration change, such as screen rotation. The new instance of the owner reconnects to the existing `ViewModel` instance.

  ![image](https://github.com/Xenoare/book-notes/assets/67181778/daea78d2-5f9d-4c71-8718-27cd3c8900bf)

    * Understanding ViewModel lifecycle <br>
    In `GameViewModel.kt`, add an `init` block with log statement.
        ```kotlin
        class GameViewModel : ViewModel() {
           init {
               Log.d("GameFragment", "GameViewModel created!")
           }
        
           ...
        }
        ```
    Kotlin provides the **initializer block** (also known as the `init` block) as a place for initial setup code needed during the initialization of an object instance. This block of code is run when the object instance is first created and initalized.<br>
    In the `ViewModel` class, override the `onCleared()` method. The `ViewModel` is destroyed when the asoicated fragments is detached or when the activity is finished. <br>
    Right before the ViewModel is destroyed, the `onCleared()` callback is called
  ```kotlin
  override fun onCleared() {
      super.onCleared()  
  }
  ```
    In `GameFragment`. override the `onDetach()` callback method, which will be called when the corresponding activity and fragments are destroyed.
  ```kotlin
  override fun onDetach() {
    super.onDetach()
  }
  ```

* **Poplate ViewModel** <br>
`Late Initalization` is a concept where you declare a variable, you provide it with an *initial* value upfront. However, if you're not ready to assign a value yet, you can assign it later. <br>
To late initialization a property in Kotlin, you have to use the keyword `lateinit`, which means late initalization. If you are guarantee that you will initalize the property before using it, you can declare the property with `lateinit`. Memory is not allocated to the variable until it is initialized. If you try to access the variable before initalizing it, thee app will crash.
    1. In `GameViewModel`, add a new class of variable of type `MutableList<String>` called `wordList`, to hold list of words used in the game, to avaoid repetations. Also add calss variable `currentWord` to hold the word player is trying to *unscramble*.
     ```kotlin
     private var wordsList: MutableList<String> = mutableListOf()
     private lateinit var currentWord: String
     ```
  2. Implement the `getNextWord()` method for your reference
     ```kotlin
         private fun getNextWord() {
           currentWord = allWordsList.random()
           val tempWord = currentWord.toCharArray()
           tempWord.shuffle()
        
           while (String(tempWord).equals(currentWord, false)) {
               tempWord.shuffle()
           }
           if (wordsList.contains(currentWord)) {
               getNextWord()
           } else {
               _currentScrambledWord = String(tempWord)
               ++currentWordCount
               wordsList.add(currentWord)
           }
        }
     ```

    Since that you've created the `getNextWord()` method, to get the next scramble word. You'll make a call when the `GameViewModel` is initialized for the first time. <br>
    We can use the `init` block to initialize `lateinit` properties in the class such as the current word. The result will be that the first word displayed on the screen will be sccrambled word instaed of **test**
    ```kotlin
    init {
        Log.d("GameFragment", "GameViewModel created!")
        getNextWord()
    }
    ```
    Now add the `lateinit` modifier onto the `_currentScrambleWord` property. Add an explicit mention of data type `String`.
    ```kotlin
    private lateinit var _currentScrambleWord: String
    ```

* **Dialogs** <br>
The anatomy of Alert Dialogs

    ![image](https://github.com/Xenoare/book-notes/assets/67181778/ae4e5c95-b8d5-4b20-a390-d533568b86b7)
    1. Alert Dialog
    2. Title (optional)
    3. Message
    4. Text buttons

    The implementation of the final score are using the `MaterialAlertDialog` from the Material Design Components Library to add a dialog. <br>
    
    Since a dialog is UI related, the `GameFragment` will be responsible for creating and showing the final score dialog.
    1. First, add a backing property to the `score` variable. In `GameViewModel`, change the `score` variable declaration to the following
        ```kotlin
        private var _score = 0
        val score: Int
            get(): _score
        ```
    2. In `GameFragment` add a private function called `showFinalScoreDialog()`. To create a `MaterialAlertDialog`, use [MaterialAlertDialogBuilder](https://developer.android.com/reference/com/google/android/material/dialog/MaterialAlertDialogBuilder) class to build up parts of the dialog step-by-step. The `MaterialAlertDialogBuilder` constructor passing the **context** in the content using the fragment's `requireContext()` method.
        ```kotlin
        private fun showFinalScoreDialog() {
            MaterialAlertDialogBuilder(requireContext())
        }
        ```
        [Context](https://developer.android.com/reference/android/content/Context.html) will `refers` to the context of the `current` state of an application, activity or fragment. It is contains the information regarding the activity, fragment or application Usually used to get access to the `resources`, `databases`, and other system.
    3. Add code to set the title on the alert dialog, and use the string resourece from `strings.xml`
        ```kotlin
        MaterialAlertDialogBuilder(requireContext())
            .setTitle(getString(R.string.congratulation))
        ```
    4. Chain this method also to show the messsage the final score. You also can use the `read-only` version of the score variable (`viewModel.score`)
       ```kotlin
           .setMessage(getString(R.string.you_scored, viewModel.score))
       ```
    5. Make your alert dialog not cancelable when the back key is pressed by using the `setCancelable()` method and passing false `false`.
       ```kotlin
           .setCancelable(false)
       ```
    6. Add tow text buttons **EXIT** and **PLAY AGAIN** using the methods `setNegativeButton()` and `setPositiveButton()`. Call the `exitGame()` and `restartGame()` respectively from the lambdas.
        ```kotlin
            .setNegativeButton(getString(R.string.exit)) { _, _ ->
            exitGame()
        }
        .setPositiveButton(getString(R.string.play_again)) { _, _ ->
            restartGame()
        }
        ```
        This syntax will takes in two _parameters_. A `String` and a function `DialogInterface.OnClickListener()` which can be expressed as a lambda. When the last argument being passed in is a function, you can express the lambda function outside the _parentheses_ (known as [trailing lambda syntax](https://kotlinlang.org/docs/reference/lambdas.html#passing-a-lambda-to-the-last-parameter).
    7. At the end, add `show()`, which creates and then display the alert dialog.
        ```kotlin
            .show()
        ```

* **Implement `onClickListener` for submit button** <br>
    First thing first, we acan add a helper **method to validate player word** in `GameViewModel`, `increaseScore()` with no parameters and no return value. We can increase the `score` variable by `SCORE_INCREASE`.
        ```kotlin
        private fun increaseScore() {
            _score += SCORE_INCREASE
        }
        ```
    also now implement `isUserWordCorrect()` to validate the player's word and increase the store if the guess is correct
    ```kotlin
    fun isUserWordCorrect(playerWord: String): Boolean {
        if (playerWord.equals(currentWord, true) {
            increaseScore()
            return true
        }
        return false
    }
    ```

* **Implement the Skip Button** <br>
    Similar to `onSubmitWord()`, add a condition in the `onSkipWord()` method. If `true`, then display the word on the screen. Otherwise show the alert dialog with the final score.
    ```kotlin
    private fun onSkipWord() {
        if (viewModel.nextWord()) {
            setErrorTextField(false)
            updateNextWordOnScreen()
        } else {
            showFinalScoreDialog()
        }
    }
    ```

* **Update Game Restart Logic** <br>
    To reset the app data, in `GameViewModel` add a method called `reinitalizeData()` and set the score and word count to `0`. Clear the word list and call the `getNextWord()` method.
    ```kotlin
    /*
    * Re-initializes the game data to restart the game.
    */
    fun reinitializeData() {
       _score = 0
       _currentWordCount = 0
       wordsList.clear()
       getNextWord()
    }
    ```
    In `GameFragment` at the top of the method `restartGame()`, make a call to the newly created method, `reinitalizeData()`.
    ```kotlin
    private fun restartGame() {
        viewModel.reinitializeData()
        setErrorTextField(false)
        updateNextWordOnScreen()
    }
    ```

 #### Use LiveData with ViewModel
 ---
 * **What is Livedata** <br>
 [LiveData](https://developer.android.com/topic/libraries/architecture/livedata) is an observable data holdre class that is lifecycler-aware. Here's some characteristics of `LiveData`
    + `LiveData` holds data; `LiveData` is a wrapper that can be used with any type of data.
    + `LiveData` is observable, which means that an observer is notified when the data held by the `LiveData` object changes.
    + `LiveData` is lifecycle-aware, which means when you attach an observer to the `LiveData`. The observer is assocated with a [LivecyclerOwner](https://developer.android.com/topic/libraries/architecture/lifecycle#lco) (which usually an `acitity` or `fragment`). The `LiveData` only updates observers that are in active lifecycler state such as `STARTED` or `RESUMED`.

* **Add LiveData to the current Scrambled Word**
`MutableLiveData` is the mutable version of the `LiveData`, that is the value of the data stored within it can be changed.
    1. In `GameViewModel`, changes the type of the variable `_currentScrambleWord` to `MutableLiveData <String>`.
    2. Change the variable type of `_currentScrambleWord` to `val` becuase of the `LiveData` / `MutableLiveData` object will remain the same, and only the data stored within the same object will change.
        ```kotlin
        private val _currentScrambledWord = MutableLiveData<String>()
        ```
    3. Change the backing field, `currentScrambledWord` type to `LiveData<String>`, because it is immutable by default.
        ```kotlin
        val currentScrambleWord: LiveData<String>
        get() = _currentScrambleWord
        ```
    4. **To acccess the data within a `LiveData` object**, use the `value` property in `GameViewModel` inside the `getNextWord()` method.
        ```kotlin
        private fun getNextWord() {
             { else }
                _currentScrambleWord.value = String(tempWord)
            }
        }    
        ```

* **Attach observer to the LiveData object (One Way to use LiveData)** <br> 
    The observer that will changes the app's data in `currentScrambleWord`. The `LiveData` if `lifecycle-aware`, which means that it only updates observer that are in an active lifecycler state. So the observer in the `GameFragment` will only be notified when the `GameFragment` is in `STARTED` or `RESUMED` states.
    1. Attach an observer for `currentScrabmbledWord` `LiveData`. In `GameFragment` at the end of the callback `onViewCreated()`, call the [observe](https://developer.android.com/reference/androidx/lifecycle/LiveData#observe(androidx.lifecycle.LifecycleOwner,%20androidx.lifecycle.Observer%3C?%20super%20T%3E)) method on `currentScrambleWord`.
        ```kotlin
        viewModel.currentScrambledWord.observe()
        ```
    2. This will give a warning since `observe()` require some parameters to be passed on.
    3. Pass `viewLifecyclerOwner` as the first parameter, this represents the `Fragment's View` lifecycle. This helps the `LiveData` to be aware of the `GameFragment` lifecycle and notify the observer only when the `GameFragment` is in active states (`STARTED` or `RESUMED`)
    4. Also add a `lambda` expression as the second parameter.
        ```kotlin
        // Observe the scrambledCharArray LiveData, passing in the LifecycleOwner and the observer.
        viewModel.currentScrambledWord.observe(viewLifecycleOwner,
           { newWord ->
               binding.textViewUnscrambledWord.text = newWord
           })
        ```
        
* **Use LiveData with data Binding (Another method to using LiveData)** <br>
    Data binding binds the UI components in your layouts to data sources in your app using a declarative format. Here's the example using view binding in UI controller.
    ```kotlin
    binding.textViewUnscrambledWord.text = viewModel.currentScrambledWord
    ```
    And the using data binding in layout file
    ```xml
    android:text="@{gameViewModel.currentScrambleWord}"
    ```
    The main advantage of using data binding is, it lets you remove many UI framework calls in your activites, such that making simpler and easier to maintain.
    1. Configure the gradle files. enable the `dataBinding` property under the `buildFeatures` section
       ```xml
       buildFeatures {
        viewBinding = true
       }
       ```
    2. Also apply the `kotlin-kapt` plugin.
       ```xml
       plugins {
           id 'com.android.application'
           id 'kotlin-android'
           id 'kotlin-kapt'
       }    
       ```
    3. Data binding layout files are slightly diff and start with a root tag of `<layout>` folllowed by an optional `<data>` element and a `view` root element.<br> To convert the layout to a Data Binding layout, wrap the root element in a     `<layout>` tag. You'll also have to move the namespace definitions (the attributes that start with `xmlns`:) to the new root element. Add `<data></data>` tags inside `<layout>` tag above the root element. Android Studio offers a handy way to do this automatically: Right-click the root element (`ScrollView`), select Show Context Actions > Convert to data binding layout.
    ![image](https://github.com/Xenoare/book-notes/assets/67181778/4a40c94d-edd1-496a-907d-77348a040ff3)

    4. The new layout should look like this
        ```kotlin
        <layout xmlns:android="http://schemas.android.com/apk/res/android"
           xmlns:app="http://schemas.android.com/apk/res-auto"
           xmlns:tools="http://schemas.android.com/tools">
        
           <data>
        
           </data>
        
           <ScrollView
               android:layout_width="match_parent"
               android:layout_height="match_parent">
        
               <androidx.constraintlayout.widget.ConstraintLayout
                 ...
               </androidx.constraintlayout.widget.ConstraintLayout>
           </ScrollView>
        </layout>
        ```
    5. Change the instantiation of the binding variable of the `onCreateView()` method. Replace
       ```kotlin
       binding = GameFragmentBinding.inflate(inflater, container, false)
        ```
        With
       ```kotlin
       binding = DataBindingUtil.inflate(inflater, R.layout.game_fragment, container, false)
        ```

* **Add data binding variables** <br>
    1. In `game_fragment.xml`, inside the <data> tag add a child tag called `<variable>`, declare a property called `gameViewModel` and of the type `GameViewModel`. you will use this to bind the data in `ViewModel` to the layout.
        ```xml
        <data>
           <variable
               name="gameViewModel"
               type="com.example.android.unscramble.ui.game.GameViewModel" />
        </data>
        ```
        Notice that the type of `gameViewModel` contains the package name. make sure to matches with the package name in the app.
    2. Add another inside `<data>` tag with type of `Integer` and name `maxNoOfWords`, You will use this bind to the variable in the `ViewModel` to store the number of words per game.
       ```xml
       <data>
       ...
           <variable
               name="maxNoOfWords"
               typa="int" />
       </data>
        ```
    3. In `GameFragment` at the beginning of `onViewCreated()` method, init the layout variables `gameViewModel` and `maxNoOfWords`.
        ```kotlin
        overrride fun onViewCreated(view: View, savedInstancesState: Bundle?) {
            super.onViewCreated(view, savedInstancState)
    
            binding.gameViewModel = viewModel
    
            bindng.maxNoOfWords = MAX_NO_OF_WORDS
        }
        ```
    4. The `LiveData` is lifecycle-aware observable, so you have to pass the lifecycler owner to the layout. In the `GameFragment`, inside the `onViewCreated()` method, add this line
       ```kotlin
        // Specify the fragment view as the lifecycle owner of the binding.
        // This is used so that the binding can observe LiveData updates
        binding.lifecycleOwner = viewLifecycleOwner
       ```

* **Use Binding Expression** <br>
    Binding expressions are written within the layout in the attribute properties (such as `android:text`) referencing the layout properties. Layout properties are declared at the top of the data binding layout file, via the `<variable>` tag.

    **Syntax for binding expressions** <br>
    Binding expressions start with an `@` symbol and are wrapped inside the curly braces `{}`.
    ```xml
    <TextView android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="@{user.firstName}" />
    ```

    1. Add binding expression to the current word <br>
        + in `game_fragment.xml` add a `text` attribute to the `android:id`. Use the new layout variable, `gameViewModel` and assign `@{gameViewModel.currentScrambleWord}` to the `text` attribute.
       ```xml
        <TextView
           android:id="@+id/textView_unscrambled_word"
    
           android:text="@{gameViewModel.currentScrambleWord}"
       ```

    2. Add binding expression to the score and the word count
        + Resourece in data binding expressions
          A data binding can reference app resources with the following syntax.
          ```xml
          android:padding="@{@dimen/largePadding}"
          ```
          You also can pass layout properties as resources parameters.
          ```xml
          android:text="@{@string/example_resource(user.lastName)}"
          ```
          ```xml
          # strings.xml
          <string name="example_resource">Last Name: %s</string>
          ```

    In this step, you will add binding expressions to the score and word count text views, passsing in the resources parameters.
    1. In `game_fragment.xml`, update the `text` attribute for `word_count` text view with the following binding expression. Use `word_count` string resource and pass in `gameViewModel.currentWordCount`, and `maxNoOfWords` as resource parameters.
        ```xml
            <TextView
           android:id="@+id/word_count"
           ...
           android:text="@{@string/word_count(gameViewModel.currentWordCount, maxNoOfWords)}"
           .../>
        ```
    2. Update the `text` attribute for `score` text view with the following binding expression.
        ```xml
        <TextView
       android:id="@+id/score"
       ...
       android:text="@{@string/score(gameViewModel.score)}"
       ... />
        ```

## Advanced Navigation App
Notes: 
+ [Additionals github Project](https://github.com/google-developer-training/android-basics-kotlin-cupcake-app/tree/starter)

Table of Contents:
+ [Setup a Shared ViewModels](#setup-a-shared-viewmodels)

#### Setup a Shared ViewModels
* **Complete the Navigation Graph** <br>
Given the starter code, connect destinations in navigation graph (**res > navigation > nav_graph.xml**
    ![image](https://github.com/Xenoare/book-notes/assets/67181778/01a16cec-ec94-49c7-a991-d61a92e50b5b)

* **Navigate from start to other fragments** <br>
Navigate between **startFragment** to **flavorFragment** by tapping the buttons in the first fragments by using the `findNavController` method in the `onViewCreated()` method.
    ```kotlin
    fun orderCupcake(quantity: Int) {
        findNavController().navigate(R.id.action_startFragment_to_flavorFragment)
    }
    ```
    do this also for other fragments.

* **Update the title in app bar** <br>
    1. Override the `onCreate()` method to set up thee navigation controller. Get an instance of `NavController` from the `NavHostFragment`.
    2. Make a call to `setupActionBarWithNavController(navController)` by passing the instance of `navController`. This will do the following: Show a titile in the app based off the destination's label.
        ```kotlin
        class MainActivity : AppCompatActivity(R.layout.activity_main) {
    
            override fun onCreate(savedInstanceState: Bundle?) {
                super.onCreate(savedInstanceState)
        
                val navHostFragment = supportFragmentManager
                        .findFragmentById(R.id.nav_host_fragment) as NavHostFragment
                val navController = navHostFragment.navController
        
                setupActionBarWithNavController(navController)
            }
        }
        ```
    3. Open the `navigation/nav_graph.xml` and modify the `android:label` atribute for each fragment distribution.

* **Create a Shared ViewModel** <br>
Recall that the app data is saed within the `ViewModel` during configuration changes.
**Follow `ViewModel` Best Practices** <br>
In a `ViewModel`, it is a recommended practice to not expose view model data as `public variables`. Otherwise the app data can be modifier in _unexpected ways_ by the external classes and create edge cases your app didn't expeact to handle. <br>
Instead, make these mutable properties `private`, and implementing a backing property, and expose the `public` immutable version of each property, if needed. <br>
We're going to create a properties and methods for this `ViewModel` such that
    + Order quantity (`Integer`)
    + Cupcake flavor (`String`)
    + Pickup date (`String`)
    + Price (`Double`)
    + `setQuantity(numberCupcakes: Int)`
    + `setFlavor(desiredFlavor: String)`
    + `setDate(pickupDate: String)`

    We don't need a setter function for the price because it will be calculated within the `OrderViewModel` using another properties.
    ```kotlin
    private val _quantity = MutableLiveData<Int>(0)
    val quantity: LiveData<Int> = _quantity
    ...
    fun setQuantity(numberCupcakes: Int) {
        _quantity.value = numberCupcakes
    }
    ```







   
