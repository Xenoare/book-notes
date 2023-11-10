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
    private val viewModel = GameViewModel()
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
+ [String Res](https://developer.android.com/guide/topics/resources/string-resource#Plurals)
+ [Intent Action](https://developer.android.com/guide/components/intents-common#Email)
+ [Scope Function](https://kotlinlang.org/docs/reference/scope-functions.html)
+ [Talkbacl](https://developer.android.com/guide/topics/ui/accessibility/testing#explore_your_app_with_talkback)

Table of Contents:
+ [Setup a Shared ViewModels](#setup-a-shared-viewmodels)
+ [Navigaion and back stack](#navigation-and-back-stack)
+ [Task and Back Stack](#task-and-back-stack)

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

* **Use the ViewModel to update the UI** <br>
To use the shared view model in `StartFragment` you will init the `OrderViewModel` using `acitivityViewModels()` instead of `viewModels()` delegate classs.
    + `viewModels()` gives you the `ViewModel` instance scoped to the current fragment. This will be diff. for diff. fragments.
    + `activityViewModels()` gives you the `ViewModel` instance scoped to the current activity. Therefore the **instance will remain the same accross multiple fragments in the same activity**.

**Using Kotlin Property Delegate** <br>
1. In `StartFragment` class, get a reference to the shared view model as a class variable.
    ```kotlin
    import androidx.fragment.app.activityViewModel
    import com.example.cupcake.mmodel.OrderViewModel
    
    private val sharedViewModel: OrderViewModel by activityViewModel()
    ```
2. Use the `sharedViewModel` instance before navigating in each fragments
   ```kotlin
    fun orderCupcake(quantity: Int) {
        sharedViewModel.setQuantity(quantity)
        findNavController().navigate(R.id.action_startFragment_to_flavorFragment)
    }
   ```
3. Within the `OrderViewModel` class, add the following method to check if the flavor for the order has been set or not.
    ```kotlin
    # OrderViewModel.kt
    fun hasNoFlavorSet(): Boolean {
        return _flavor.value.isNullOrEmpty()
    }
    ```
4. Inside the `OrderCupcake` method, after setting the quantity, set the default flavor as Vanila if no flavor is set, before navigating to the flavor fragment.
   ```kotlin
   fun orderCupcake(quantity: Int) {
       sharedViewModel.setQuantity(quantity)
       if (sharedViewModel.hasNoFlavorSet()) {
        sharedViewMode.setFlavors(getString(R.string.vanilla))
       }
       findNavController().navigate(R.id.action_startFragment_to_flavorFragment)
   }
   ```

* **Use ViewModel with Data Binding** <br>
Data binding is binding data (from code) to views + view binding (binding views to code). By setting up these bindings and having updates be automatic, this helps you reduce the chance for errors if you forget to manually update the UI from your code.
1. In `layout/fragment_flavor.xml`, add a `<data>` tag inside the root `<layout>` tag. Then add a layout variable called `viewModel` with type of package URL. Also add for another layout.
    ```kotlin
    <layout>
        <data>
            <variable
                name="viewModel"
                type="com.example.cupcake.model.OrderViewModel" />
        </data>
        ...
    </layout>
    ```
2. In the `FlavorFragment` class, inside the `onViewCreated()`, **bind the view model instance** with the shared view model instance in the layout. Do it also for another fragments.
   ```kotlin
   binding?.apply {
       viewModel = sharedViewModel
       ...
   }

**Apply scope function** <br>
[`Apply`](https://kotlinlang.org/docs/reference/scope-functions.html) is a scope function that executes a block of code within the context of an object. It forms a temporary scope, and in that scope, you can access the object without its name.
```kotlin
clark.apply {
    firstName = "Clark"
    lastName = "James"
    age = 18
}

// The equivalent code without apply scope function would look like the following.

clark.firstName = "Clark"
clark.lastName = "James"
clark.age = 18
```

3. In `fragment_flavor.xml`, use the new layout variable, `viewModel` to set the `checked` attribute of the radio buttons based on the flavor value in the view model. If the flavor represented by a radio button is the same as the flavor that's saved in the view model, then display the radio button as selected (`checked` = true). <br>
Essentially, this is comparing the `viewModel.flavor` property with the corresponding resource using the [equals](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-any/equals.html) function. <br>
**Note: Remember that binding expressions start with an @ symbol and are wrapped inside curly braces {}. **
    ```xml
    # fragment_flavor.xml
    <RadioButton
        android:id="@+id/vanilla"
        ...
        android:checked="@{viewModel.flavor.equals(@string/vanilla)}"
        />
    
    <RadioButton
        android:id="@+id/chocolate"
        ...
        android:checked="@{viewModel.flavor.equals(@string/chocolate)}"
        />

    <RadioButton
        android:id="@+id/red_valvet"
        ...
        android:checked="@{viewModel.flavor.equals(@string/red_valvet)}"
        />
    ...
    ```

* **Listener Bindings** <br>
Listener bindings are `lambda` expression that run when an event happens, such as `onClick` event. They are similar to method references such as `textview.setOnClickListener(clickListener)` but listener bindings let you run arbitrary data binding expressions.

4. In `fragment_flavor.xml`, add event listener to the radio buttons using listener bindings and lambda expression.
    ```kotlin
    <RadioButton
        android:id="@+id/vanila"
        android:onClick="@{() -> viewModel.setFlavor(@string/vanila}" />

    <RadioButton
        android:id="@+id/chocolate"
        android:onClick="@{() -> viewModel.setFlavor(@string/chocolate}" />

    <RadioButton
        android:id="@+id/red_valvet"
        android:onClick="@{() -> viewModel.setFlavor(@string/red_valvet}" />
    ...
    ```

* **Update pickup and summary fragment to use View model** <br>
**Date Formatter** <br>
The android framework provides a class called [SimpleDateFormat](https://developer.android.com/reference/java/text/SimpleDateFormat), which is a class for formatting and parsing dates in locale-sensitive manner. <br>
You can create an instance of `SimpleDateFormat` by passing in a pattern string and a locale.
    ```kotlin
    SimpleDateFormat("E MMM d", Locale.getDefault())
    ```
    A pattern string like "`E MMM d`" is a representation of Date and Time formats. Letters from '`A`' to '`Z`' and from '`a`' to '`z`' are interpreted as pattern letters representing the components of a date or time string. For example, `d` represents day in a month, `y` for year and `M` for month. If the date is `January 4 in 2018`, the pattern string "`EEE, MMM d`" parses to "Wed, Jul 4". For a complete list of pattern letters, please see the documentation. <br>
    A [Locale](https://developer.android.com/reference/java/util/Locale) object represents a specific geographical, political, or cultural region. It represents a language/country/variant combination. Locales are used to alter the presentation of information such as numbers or dates to suit the conventions in the region. Date and time are locale-sensitive, because they are written differently in different parts of the world. You will use the method `Locale.getDefault()` to retrieve the locale information set on the user's device and pass it into the `SimpleDateFormat` constructor.

Now using `SimpleDateFormat` and `Locale` to determine the available pickup dates for the app.
1. In `OrderViewModel` create a method `getPickupOptions()` to create and return the list of pickup dates.
    ```kotlin
    private fun getPickupOptions(): List<String> {
        val options = mutableListOf<String>()
    }
    ```
2. Create a formatter string using `SimpleDateFormat` passing patter string `"E MMM d"`, and the locale. In the patter string, `E` stands for the day name in week and it parses to "Tue Dec 10"
    ```kotlin
    val formatter = SimpleDateFormat("E MMM d", Locale.getDefault())
    ```
3. Get a `Calendar` instance and assigned it to a new variable. Make it `val`. This variable will contain the current date and time.
   ```kotlin
   val calendar = Calendar.getInstance()
   ```
4. Build up a list of dates starting with the current date and following three dates. You'll need [repeat](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/repeat.html) block to repeat the format date, add into the list and increament the date by 1 day
   ```kotlin
   repeat(4) {
       options.add(formatter.format(calendar.time))
       calendar.add(Calendar.DATE, 1)     
   }
   return options
   ```
5. In `OrderViewModel` class, add a class property called `dateOptions` that's a `val`.
   ```kotlin
   val dateOptions = getPickupDate()
   ```

* **Update the Layout to Display Pickup Options** <br>
Since we have 4 available pickup dates, update the `fragment_pickup.xml` layout to dipslay these dates (use data binding to display the checked status of each radio button and to update the date in the view model when diff radio button is selected).
    ```xml
    <RadioButton
        android:id="@+id/option0"

        android:checked="@{viewModel.date.equals(viewModel.dateOptions[0])}"
        android:onClick="@{() -> viewModel.setDate(viewModel.dateOptions[0])}"
        android:text="@{viewModel.dateOptions[0]}" />
        ...
        # Do this for other 3 date options
    ```
    1. Within the `OrderViewModel` class, create a function called `resetOrder()`, to reset the `MutableLiveDate` properties in the view model.
    ```kotlin
    fun resetOrder() {
        _quantity.value = 0
        _flavor.value = ""
        _date.value = dateOptions[0]
        _price.value = 0.0
    }
    ``` 
    2. Add an `init` block to the calss and call the `resetOrder()` from inside
    ```kotlin
        resetOrder()
    ```

* **Update Summary Fragment to Use View Model** <br>
The order summary fragment is intended to show a summary of order details by using the advantage of Shared View Model.
1. In `fragment_summary.xml`, read from the viewModel to update the screen with the order summary details. Update the quantity, flavor and date `TextViews` by adding the following text attributes.
    ```xml
        <TextView
            android:id="@+id/quantity"
            ...
            android:text="@{viewModel.quantity.toString()}" />
        <TextView
            android:id="@+id/flavor"
            ...
            android:text="@{viewModel.flavor.toString()}" />
        <TextView
            android:id="@+id/date"
            ...
            android:text="@{viewModel.date.toString()}" />
    ```

* **Calculate price from order details** <br>
So here's the rules for the cupcake shop
+ Each cupcake is $2.00 each
+ Same day pickup adds an extra $3.00 to the order.

To update the price in view model, Firstly we can tackle the price per cupcake first and ignore the same day pickup cost.
1. Open the `OrderViewModel` and store the price per cupcake in a variable. `Declare` it as a `top-level private constant` at the top of the file.
    ```kotlin
    private const val PRICE_PER_CUPCAKE = 2.00

    class OrderViewModel : ViewModel() {}
    ```
2. Now create a helper method (`updatePrice()`) to calculate the price.
   ```kotlin
   private fun updatePrice() {
       _price.value = (quantity.value ?: 0) * PRICE_PER_CUPCAKE
   }
   ```
3. In the same `OrderViewModel` class, update the price variable when the quantity is set. make a call to the new function in the `setQuantity()` function.
   ```kotlin
   fun setQuantity(numberCupcakes: Int) {
       _quantity.value = numberCupcakes
       updatePrice()
   }
   ```

    **Bind the price to the UI** <br>
    Update the TextView of price for each fragments layout.
        ```xml
        <TextView
            android:id="@+id/subtotal"
            android:text="@{@string/subtotal_price(viewHolder.price))}"
            />
        ```

* **Charge extra for same day pickup** <br>
We will implement the second rule for same day pick up that add extra $3.00.
1. First thing first, we need to setup the const for this
    ```kotlin
    private const val PRICE_FOR_SAME_DAY_PICKUP = 3.00
    ```
2. In `UpdatePrice()`, check if the user selected the same day options, by checking the view model (`_date.value`) is the same as the first day in `dateOptions`
   ```kotlin
   private fun updatePrice() {
       var calculatedPrice = (quantity.value ?: 0) * PRICE_PER_CUPCAKE
       if (dateOptions[0] == _date.value) {
           calculatedPrice += PRICE_FOR_SAME_DAY_PICKUP
       }
        _price.value = calculatedPrice
   }
   ```
3. Call `updatePrice()` helper method from `setDate()` method
    ```kotlin
    fun setDate(pickupDate: String) {
        _date.value = pickupDate
        updatePrice()
    }
    ```

* **Set Lifecycle Owner to observe LiveData** <br>
[LifecyclerOwner](https://developer.android.com/reference/androidx/lifecycle/LifecycleO wner) is a class that has an Android Lifecycle, such as an activity or a fragment. The `LiveData` observers are the binding expressions in layout files with observable data like price. With Data Binding, when an observable value changes, the UI elements it's bound to are updated automatically. <br>
Example of binding expression
`android:text="@{@string/subtotal_price(viewModel.price}"`

For the UI element automatically update, you'll have to associate `binding.lifecycleOnwer`
1. in the 4 fragments classes, inside the `onViewCreated()` method, set the lifecycle owner on the binding object.
    ```kotlin
    binding?.apply {
        lifecycleOwner = viewLifecyclerOwner
        ...
    }
    ```

* **Format price with LiveData Transformation** <br>
The `LiveData` transformation method provides a way to perform data manipulations on the source `LiveData` and return a resultin `LiveData` object. In simple terms, it transforms the value of `LiveData` into another value. These transformations aren't **calculated unless an observer is observing the `LiveData` object**. <br>
The [Transformations.map()](https://developer.android.com/reference/androidx/lifecycle/Transformations.html#map(androidx.lifecycle.LiveData%3CX%3E,%20androidx.arch.core.util.Function%3CX,%20Y%3E)) is one of the transformation functions, this method takes the source `LiveData` and a function as parameters. The function manipulates the source `LiveData` and returns an updated value which is also observable. <br>
Some real-time examples where you may use a LiveData transformation:
+ Format date, time strings for display
+ Sorting a list of items
+ Filtering or grouping the items
+ Calculate the result from a list like sum of all the items, number of items, return the last item, and so on.

In this task, we will use `Transformations.map()` method to format the price to use the local currency. You'll transform the original price as a decimal value (`LiveData<Double>`) into a value (`LiveData<String>`).
1. In `OrderViewModel` class, change the backing property type to `LiveData<String>` instead of `LiveData<Double>`. The formatted price will be a string with a currency symbol such as `$`.
   ```kotlin
   private val _price = MutableLiveData<Double>()
   val price: LiveData<String>
   ```
2. Use `Transformations.map()` to init the new variable, pass in the `_price` and a lambda function. Use `getCurrencyInstance()` method in the [NumberFormat](https://developer.android.com/reference/kotlin/android/icu/text/NumberFormat) class to convert the price to local currency format.
   ```kotlin
   private val _price = MutableLiveData<Double>()
   val price: LiveData<String> = Transformations.map(_price) {
       NumberFormat.getCurrencyInstance().format(it)
   }
   ```

* **Setup click listener using listener binding** <br>
Use the listener binding to bind the button click listener in the fragment classes.
1. In the `fragment_start.xml`, add a data variable called `startPackage` with type URL to fragment.
   ```kotlin
   <layout ...>

    <data>
        <variable
            name="startFragment"
            type="com.example.cupcake.StartFragment" />
    </data>
    ... 
    <ScrollView ...>
   ```
2. In `StartFragment`, in `onViewCreated()` method, bind the new data variable to the fragment instance. You can access the fragment instance inside the fragment using `this` keyword. Remove the `binding?.apply` block.
   ```kotlin
   override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        binding?.startFragment = this
    }
   ```
4. In `fragment_start.xml` add event listener binnding to the `onClick` attribute.
   ```xml
   <Button
    android:id="@+id/order_one_cupcake"
    android:onClick="@{() -> startFragment.orderCupcake(1)}" 
    ... />

    <Button
        android:id="@+id/order_six_cupcakes"
        android:onClick="@{() -> startFragment.orderCupcake(6)}" 
        ... />
    
    <Button
        android:id="@+id/order_twelve_cupcakes"
        android:onClick="@{() -> startFragment.orderCupcake(12)}" 
        ... />
    ```
5. Do this also to bind another fragment instance.
   ```xml
   # fragment_flavor.xml
   <data>
        <variable
            ... />

        <variable
            name="flavorFragment"
            type="com.example.cupcake.FlavorFragment" />
    </data>

   # fragment_pickup.xml
   <data>
        <variable
            ... />

        <variable
            name="pickupFragment"
            type="com.example.cupcake.PickupFragment" />
    </data>

    # fragment_summary.xml
   <data>
        <variable
            ... />

        <variable
            name="summaryFragment"
            type="com.example.cupcake.SummaryFragment" />
    </data>
    ```
6. In the rest of the fragment classes, in `onViewCreated()` methods, delete the code that manually sets the click listener on the buttons.
7. In the `onViewCreated()` methods bind the fragment data variable with the fragment instance. You will use `this` keyword differently here, because inside the `binding?.apply` block, the keyword this refers to the binding instance, not the fragment instance. Use `@` and explicitly specify the fragment class name, for example this@FlavorFragment.
   ```kotlin
    // FragmentFlavor
    binding?.apply {
        lifecycleOwner = viewLifecycleOwner
        viewModel = sharedViewModel
        flavorFragment = this@FlavorFragment
    }

   // PickupFragment
    binding?.apply {
       lifecycleOwner = viewLifecycleOwner
       viewModel = sharedViewModel
       pickupFragment = this@PickupFragment
    }

    // SummaryFragment
    binding?.apply {
       lifecycleOwner = viewLifecycleOwner
       viewModel = sharedViewModel
       summaryFragment = this@SummaryFragment
    }
   ```
8. Add a listener binding to the `onClick` atribute on the layout fragments
   
#### Navigation And Back Stack
* **Implement Up Button Behavior** <br>
In the **Cupcake** app, the app bar shows an arrow to return to the previous screen (this is known as the `Up` button). We need to configure this so it can be used.
![image](https://github.com/Xenoare/book-notes/assets/67181778/b61fc7b5-8d14-4879-8800-c586b0ea3df8)

1. In the `MainAcitivity`, you should already have code to setup the app bar (also known as action bar) with nav controller. Make `navController` a class variable so you can use it in another method.
   ```kotlin
   class MainActivity : AppCompatActivity(R.layout.activity_main) {

            private lateinit var navController: NavController
        
            override fun onCreate(savedInstanceState: Bundle?) {
                super.onCreate(savedInstanceState)
        
                val navHostFragment = supportFragmentManager
                        .findFragmentById(R.id.nav_host_fragment) as NavHostFragment
                navController = navHostFragment.navController
        
                setupActionBarWithNavController(navController)
            }
        }
   ```
2. Override the `onSupportNavigateUp()` method. This code will ask the `navController` to handle navigating up in the app. Otherwise, fall back to the superclass implementation (in `AppCompactActivity`) of handling the **Up** button.
    ```kotlin
    override fun onSupportNavigateUp(): Boolean {
        return navController.navigateUp() || super.onSupportNavigateUp()
    }
    ```

#### Task and Back Stack
Now we are going to implement **Cancel** button within the order flow of the app. Cancelling an order at any point sends the user back to `StartFragment`.

**Tasks** <br>
**Activities** in Android exist within tasks. When you open an app for the first time from the launcher icon, **Android creates a new task with your main activity**. A task is a collection of activities that the user interacts with when performing a certain job (i.e. checking email, creating a cupcake order, taking a photo). <br>
Activities are arranged in a stack, known as a back stack, where each new activity the user visits gets pushed onto the back stack for the task. You can think of it as a stack of pancakes, where each new pancake is added on top of the stack. The activity on the top of the stack is the current activity the user is interacting with.
![image](https://github.com/Xenoare/book-notes/assets/67181778/3831d167-6bf1-4386-8986-237ba0bc51cd)

When you first lunch the app, the `MainActivity` opens and is addes to the task's back stack.
    ![image](https://github.com/Xenoare/book-notes/assets/67181778/908eb1b6-59ab-4ec7-9664-e378dcf28dd7)
    
When you click on a letter, the `DetailActivity` is launched and pushed onto the backstack. This means the `DetailActivity` has been _created, started, and resumed_ so the user can interact with it. The `MainActivity` is put into the background, and shown with the gray background color in the diagram.
    ![image](https://github.com/Xenoare/book-notes/assets/67181778/de2aa0a6-8ed2-4281-97f5-900e6604a1cd)
    
If you tap the **Back** button, the `DetailActivity` is popped off the back stack and the `DetailActivity` instance is destroyed and finished.
    ![image](https://github.com/Xenoare/book-notes/assets/67181778/099eb3bb-39e7-445c-95c9-4a5d3cada723)
    
Then the next item on top of the back stack (the `MainActivity`) is brought to the foreground.
    ![image](https://github.com/Xenoare/book-notes/assets/67181778/8724a7e4-951a-40d2-ac19-f75c924d2c1d)

* **Modify the back stack in the Cupcake app** <br>
First, modify the `FlavorFragment`, `PickupFragment` and `SummaryFragment` class and layout files in navigation action.
1. Open the Navigation action (`res > navigation > nav_graph.xml`) and make a new action to `StartFragment`
   ![image](https://github.com/Xenoare/book-notes/assets/67181778/fd72fd4a-40ee-441d-a9d1-d4f2e54ff710)
   
    Implement a cancel button to layout, except for the `StartFragment`, There may be a diffrent implementation in styling for those fragments. But it still share the same purpose
   ```xml
       ...
    
    <TextView
        android:id="@+id/subtotal" ... />
    
    <Button
        android:id="@+id/cancel_button"
        style="?attr/materialButtonOutlinedStyle"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginEnd="@dimen/side_margin"
        android:text="@string/cancel"
        app:layout_constraintEnd_toStartOf="@id/next_button"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@id/next_button" />
    
    <Button
        android:id="@+id/next_button" ... />
    
    ...
   ```
3. Add a cancel button listener <br>
   Within each fragment class (except `StartFragment`), add a helper method that handles when the **Cancel** button is clicked.
   + Add this `cancelOrder()` method inside all `FlavorFragment`, `PickupFragment` and `SummaryFragment`. If the user decides to cancel their order, then clear out the view model by calling the `sharedViewModel.resetOrder()`. Then navigate back to `StartFragment` using navigation action with ID `R.id.action_flavorFragment_to_startFragment`.
     ```kotlin
     fun cancelOrder() {
        sharedViewMode.resetOrder()
         findNavController().navigate(R.id.action_flavorFragment_to_startFragment)
     }
     ```
   + Use listener binding to setup the `Cancel` button in the both fragments
     ```xml
     # fragment_flavor.xml
     <Button
        android:id="@+id/cancel_button"
        android:onClick="@{() -> flavorFragment.cancelOrder()}"
         ....
     />
     ```
   + Repeat the same proces for the rest of the fragments.

But there's a bug that when a **Back** button is clicked, then it bounce back to order summary screen with 0 cupcakes and no flavor.
![image](https://github.com/Xenoare/book-notes/assets/67181778/88a11627-d1d1-4f6b-85d1-bd14737ec7e5)

The user likely does not want to go back through the order flow. Plus, all the order data in the view model has been cleared out, so this information is not useful. Instead, tapping the `Back` button from the `StartFragment` should leave the `Cupcake app`. <br>
From the `SummaryFragment`, when cancelled an order. Android added another instance of `StartFragment` as a new destination on the back stack.
![image](https://github.com/Xenoare/book-notes/assets/67181778/6e7921bf-1fa3-43d1-9c9a-193514155a5e)

That is why when you tapped the `Back` button from the `StartFragment`, the app ended up showing the `SummaryFragment` again (with blank order information).

* **Pop Additionals Destination off the back stack** <br>
Introduding **Navigation action: popUpTo attribute** by an including `app:popUpTo` attribute on the navigation action in the navigation graph, more than one dest can be popped off the back stack until that specified dest. is reached. If you specify `app:popUpTo="@id/startFragment"`, then destinations in the back stack will get popped off until you reach `StartFragment`, which will remain on the stack. <br>
When you add this change to your code and run the app, you'll find that when you cancel an order, you return to the `StartFragment`. But this time, when you tap the `Back` button from the `StartFragment`, you see `StartFragment` again (**instead of exiting the app**). This is also not the desired behavior. As mentioned earlier, **since you are navigating to StartFragment, Android actually adds StartFragment as a new destination on the back stack**, so now you have 2 instances of StartFragment on the back stack. Hence, you need to tap the Back button twice to exit the app.
![image](https://github.com/Xenoare/book-notes/assets/67181778/4200038a-656e-4097-9f35-0b3af95caf12)

* **Navigation actoin: popUpToInclusive attirbute** <br>
Do this by specifying `app:popUpTo="@id/startFragment"` and `app:popUpToInclusive="true"` on the appropriate navigation actions. That way, you will only have the one new instance of `StartFragment` in the back stack. Then tapping the `Back` button once from the `StartFragment` will exit the app.
![image](https://github.com/Xenoare/book-notes/assets/67181778/d567e589-5982-43fe-90c0-2c9827607da9)

1. Modify the navigation actions <br>
   + First, navigate through **Navigation Editor** by opening up the **res > navigation > nav_graph.xml**
   + Select the action that goes from `summaryFragment` to the `startFragment`
     ![image](https://github.com/Xenoare/book-notes/assets/67181778/4eeaa7c3-3d08-4ab3-9c46-06e611116362)
     
   + From the dropdown options, set `popUpTo` to be `startFragment`. This means all the destinations in the back stack will be popped off (starting from the top of the stack and moving downwards), up to the `startFragment`.
   + Then click on the checkbox for `popUpToInclusive` until it shows a checkmark and label `true`. This indicates that you want to pop off destinations up to and including the instance of `startFragment` that's already in the back stack. Then you won't have two instances of `startFragment` in the back stack.
     ![image](https://github.com/Xenoare/book-notes/assets/67181778/af11b35c-125c-4c2e-b30c-11810fd4af9a)
   + Repeat this also for another fragments

* **Send the Order** <br>
It would be a more useful experience if the order could be sent out from the app. Take advantage of what you learned in earlier codelabs about using an implicit intent to share information from your app to another app. That way, the user can share the cupcake order information with an email app on the device, allowing the order to be emailed to the cupcake shop.
![image](https://github.com/Xenoare/book-notes/assets/67181778/2f96993f-628d-4fad-8bc2-8c9aec717aea)
To implement tihs feature, take a look a how eamil subject and email body are structured in the above screenshot, Look the this **resource** in `strings.xml`
```xml
<string name="new_cupcake_order">New Cupcake Order</string>
<string name="order_details">Quantity: %1$s cupcakes \n Flavor: %2$s \nPickup date: %3$s \n Total: %4$s \n\n Thank you!</string>
```
`order_details` is a string res. with 4 diff format arguments in it, which are placeholder for the actual quantity of `cupcakes`, `desired flavor`, `pickup date` and `total price`. <br>
The arguments are numbered from 1 to 4 with the syntax `%1` to `%4`. The type of argument is also specified (`$s` means a string is expected here). <br>
In Kotlin code, you will be able to call `getString()` on `R.string.order_details` followed by the 4 arguments (order matters!). As an example, calling `getString(R.string.order_details, "12", "Chocolate", "Sat Dec 12", "$24.00")` creates the following string, which is exactly the email body you want.
```xml
Quantity: 12 cupcakes
Flavor: Chocolate
Pickup date: Sat Dec 12
Total: $24.00

Thank you!
```
1. In `SummaryFragment`, modifty the `sendOrder()` method. Construct a order summary text. Create a formatted `order_details` string by getting the order quantity, flavor, date, and price from the shared view model.
    ```kotlin
    val orderSummary = getString(
        R.string.order_details,
        sharedViewModel.quantity.value.toString(),
        sharedViewModel.flavor.value.toString(),
        sharedViewModel.date.value.toString(),
        sharedViewModel.price.value.toString()
    )
    ```
2. Still witihin the `sendOrder()` method, create an implicit intent for sharing the oder to another app. See the [docs](https://developer.android.com/guide/components/intents-common#Email) for how to create an email intent. Specify `Intent.ACTION_SEND` for the intent action, set type to `"text/plain"` and include the intent extras for the email subject (`Intent.EXTRA_SUBJECT`) and email body (`Intent.EXTRA_TEXT`).
    ```kotlin
    val intent = Intent(Intent.ACTION_SEND)
        .setType("text/plain")
        .putExtra(Intent.EXTRA_SUBJECT, getString(R.string.new_cupcake_order))
        .putExtra(Intent.EXTRA_TEXT, orderSummary)
    ```
3. Since this is an implicit intent, you don't need to know ahead of time which specific component or app will handle this intent. The user will decide which app they want to use to fulfill the intent. However, before launching an activity with this intent, check to see if there's an app that could even handle it. This check will prevent the Cupcake app from crashing if there's no app to handle the intent, making your code safer.
    ```kotlin
    if (activity?.packageManager?.resolveActivity(intent, 0) != null) {
        startActivity(intent)
    }
    ```
Perform this check by accessing the [PackageManager](https://developer.android.com/reference/android/content/pm/PackageManager), which has information about what app packages are installed on the device. The `PackageManager` can be accessed via the fragment's activity, as long as the `activity` and `packageManager` are not null. Call the PackageManager's `resolveActivity()` method with the intent you created. **If the result is not null, then it is safe to call startActivity() with your intent**.
5. Run the app

But, note that in the testing scenarios. You may notice a bug that if you only have 1 cupcake, the Order summary says **1 cupcakes**, this is a grammatically incorrect.
![image](https://github.com/Xenoare/book-notes/assets/67181778/593010da-d81a-4b41-9811-516c676f7149)
If you want to choose whether the word cupcake or cupcakes is used based on the quantity value, then you can use something called [quantity strings](https://developer.android.com/guide/topics/resources/string-resource#Plurals) in Android. By declaring a `plurals` resource, you can specify different string resources to use based on what the quantity is, for example in the singular or plural case.
6. Add a plural resource in `strings.xml`
```xml
<plurals name="cupcakes">
    <item quantity="one">%d cupcake</item>
    <item quantity="other">%d cupcakes</item>
</plurals>
```
In the singular case (`quantity="one"`), the singular string will be used. In all other cases (`quantity="other"`), the plural string will be used. Note that instead of `%s` which expects a string argument, `%d` expects an integer argument, which you will pass in when you format the string.
7. Update the `order_details` string res so that the plural versoin of **Cupcakes** is no longer hardcoded
```xml
<string name="order_details">Quantity: %1$s \n Flavor: %2$s \n Pickup date: %3$s \n Total: %4$s \n\n Thank You! </string>
```
8. Update the  `SummaryFragment` class method `sendOrder()` to use the new quantity string, and then formt the `order_details` string. But, instead of passing in the `numberOfCupcakes` as the quantity argument direcly, create a formatted cupcakes with `resources.getQuantityString(R.plurals.cupcakes, numberOfCupcakes, numberOfCupcakes)`
```kotlin
    fun sendOrder() {
        val numberOfCupcakes = sharedViewModel.quantity.value ?: 0
        val orderSummary = getString(
            R.string.order_details,
            resources.getQuantityString(R.plurals.cupcakes, numberOfCupcakes, numberOfCupcakes),
            sharedViewModel.flavor.value.toString(),
            sharedViewModel.date.value.toString(),
            sharedViewModel.price.value.toString()
        )
    
        val intent = Intent(Intent.ACTION_SEND)
            .setType("text/plain")
            .putExtra(Intent.EXTRA_SUBJECT, getString(R.string.new_cupcake_order))
            .putExtra(Intent.EXTRA_TEXT, orderSummary)
        
        if (activity?.packageManager?.resolveActivity(intent, 0) != null) {
            startActivity(intent)
        }
    }
```

## Adaptive Layouts (Later since the android studio seems not working)

## Coroutines

Notes: 
+ [Coroutine Apps](https://developer.android.com/kotlin/coroutines)
  
* **Multithreading and Concurrency** <br>
Concurrency allows multiple units of code to be execute out of order or parallel permitting more efficient use of resources. The operating system can use characteristics of the system, programming language and concurrency unit to manage mmultitasking.

![image](https://github.com/Xenoare/book-notes/assets/67181778/fe31edda-61c6-4da1-b7c8-337731dfcbf9)

**Thread** is the smallest unit of code that can be scheduled and run in the confines of a program. You can craete a simple thread by providing a lambda.
    ```kotlin
    fun main() {
        val thread = Thread {
            println("${Thread.currentThread()} has run.")
        }
        thread.start()
    }
    ```
The thread isn't executed until the function reaches the `start()` function call. The output either should look like tihs
    ```yaml
    Thread[Thread-0, 5, main' has run
    ```
Note that `currentThread()` returns a `Thread` instance which is converted to its string representation which returns the thread's name, priority, and thread group. The output above might be slightly different.

* **Coroutines in Kotlin** <br>
Coroutines enable multitasking, but provide another level of abstraction over simply working with threads. <br>
Onne key feature of coroutines is the ability to `store state`, so that they can be `halted` and `resumed`. A `coroutine` may or maynot execute. <br>

The state, represented by _continuations_, allows portions of code to signal when they need to hand over control or wait for another coroutine to complete its work before resuming. This flow is called cooperative multitasking. Kotlin's implementation of coroutines adds a number of features to assist multitasking. <br>
in additions to continuations, creating a coroutine encompasses that work in a `Job`, a cancelable unit of work with a lifecycle, inside a `CoroutineScope`. <br>
A `CoroutineScope` is a context that enforces cancellation and other rules to its children and their children recursively. A `Dispatcher` manages which backing thread the coroutine will use for its execution, removing the responsibility of when and where to use a new thread from the developer.
![image](https://github.com/Xenoare/book-notes/assets/67181778/d5ca2aa8-fa97-41a4-ac9e-85401dba9fd5)

Let's look at the examples of using coroutines:
```kotlin
import kotlinx.coroutines.*

fun main() {
    repeat(3) {
        GlobalScope.launch {
            println("Hi from ${Thread.currentThread()}")
        }
    }
}   
```
```xml
Hi from Thread[DefaultDispatcher-worker-2@coroutine#2,5,main]
Hi from Thread[DefaultDispatcher-worker-1@coroutine#1,5,main]
Hi from Thread[DefaultDispatcher-worker-1@coroutine#3`,5,main]
```
The snippet above creates three coroutines in the Global Scope using the default Dispacther. The `GlobalScope` allows any coroutines in it to **run as long as the app is running**.<br>
For the reasons we talked about concerning the main thread, this is not recommended outside example code. When you use coroutines in your apps, we will use other scopes. <br>
The `launch()` function creates a coroutine from the enclosed code wrapped in a cancelable Job object. `launch()` is used when a return value is not needed outside the confines of the coroutine.

* **A word about runBlocking** <br>
`runBlocking()` as the name suggest, implies the starts of a new coroutine blocks and the current thread until completion. It is mainly used to bridge between blocking and non-blocking code in main function and test. Given the code
    ```kotlin
    import kotlinx.coroutines.*
    import java.time.LocalDateTime
    import java.time.format.DateTimeFormatter
    
    val formatter = DateTimeFormatter.ISO_LOCAL_TIME
    val time = { formatter.format(LocalDateTime.now()) }
    
    suspend fun getValue(): Double {
        println("entering getValue() at ${time()}")
        delay(3000)
        println("leaving getValue() at ${time()}")
        return Math.random()
    }
    
    fun main() {
        runBlocking {
            val num1 = getValue()
            val num2 = getValue()
            println("result of num1 + num2 is ${num1 + num2}")
        }
    }
    ```
    Now the `getValue()` returns a random number after a set delay time. Look at the output return
  ```kotlin
  entering getValue() at 17:44:52.311
    leaving getValue() at 17:44:55.319
    entering getValue() at 17:44:55.32
    leaving getValue() at 17:44:58.32
    result of num1 + num2 is 1.4320332550421415
  ```
  Replace the `main` method with the following
  ```
  fun main() {
    runBlocking {
        val num1 = async { getValue() }
        val num2 = async { getValue() }
        println("result of num1 + num2 is ${num1.await() + num2.await()}")
        }
    }
  ```
  The `async()` function returns a value of type `Deferred`. A `Deffered` is a cancelable `Job` that can hold a reference to a future value. By using a `Deferred`, you can still call a function as if it immediately returns a value - a `Deferred` just **serves as a placeholder**, since you can't certain when an asyncrhonous task will return. <br>
  A `Deferred` (also known as Promise or Future in other languages) **guarantees that a value will be returned to this object at a later time**. <br>
  An asynchronous task, on the other hand, will not block or wait for execution by default. To initiate that the current line of code needs to wait for the output of a `Deferred`, you can call `await()` on it. It will return the raw value.


## Get Data From Internet
Notes :
+ [Android Permission](https://developer.android.com/guide/topics/permissions/overview)
+ [Moshi with Retrofit](https://proandroiddev.com/moshi-with-retrofit-in-kotlin-%EF%B8%8F-a69c2621708b)
+ [Coil](https://coil-kt.github.io/coil/)
+ [Binding Adapter](https://medium.com/android-news/binding-adapters-with-kotlin-part-1-78b957ad6b8b)

Table of Contents
+ [Connecting to the Internet](#connecting-to-the-internet)
+ [Load and display an image from internet](#load-and-display-an-image-from-internet)
+ [Display a Grid of Images with RecyclerView](#display-a-grid-of-images-with-recyclerview)

* **Web Services and Retrofit** <br>
Mars photos data is stored on a web server. To get this data, you need to establish a connection and communicate with the server on the internet.

![image](https://github.com/Xenoare/book-notes/assets/67181778/377645ae-59a2-4fe8-b049-e15e597a7c51)

![image](https://github.com/Xenoare/book-notes/assets/67181778/099b7c53-8825-468b-bbed-5efcad7f8f39)

Request are made to RESTful web services in a standardized way via `URI (Uniform Resource Identifier). An URI **identifies a resource in the server by name, without implying its location or how to access it**. <br>
A Unifrom Resource Locator (URL) is an URI that specifies the means of acting upon or obtaining the representation of a resourece, i.e. specifying both its primary access mechanism and network location.

**Web services Request** <br>
Each web service contains a URI, and is transferred to the server using the same HTTP protocol. Common HTTP operations include:
+ GET for retrieving server data
+ POST or PUT for add/create/update the server with the new data
+ DELETE for deleting the data from server

The response from a web service is commonly formatted in one of the common web formats like `XML` or `JSON` - formats for representing structured data in key-value pairs.

**External Libraries**
Retrofit library will communicate with the backend. It creates URI's for the web service based on the parameters we pass to it. You will see more on this in later sections.

![image](https://github.com/Xenoare/book-notes/assets/67181778/31d4523d-0e4e-4631-8203-672d52a96b40)

* **Setup Retroit Dependencies** <br>
Android Gradle allows you to add external libraries to your project. In addition to the library dependency, you should also include the repository where the library is hosted. The Google libraries such as `ViewModel` and `LiveData` from the Jetpack library are hosted in the Google repository. The majority of community libraries like Retrofit are hosted on Google and MavenCentral repositories.
    1. Open the `build.gradle(Project: MarsPhotos)` file and add `google()` and `mavenCentral()` repo
       ```kotlin
       repositories {
           google()
           mavenCentral()
       }
       ```
    2. Add the Retrofit libraries in the `dependencies section`
       ```kotlin
        // Retrofit 
        implementation "com.squareup.retrofit2:retrofit:2.9.0"
        // Retrofit with Scalar Converter
        implementation "com.squareup.retrofit2:converter-scalars:2.9.0"
       ```

### Connecting to the Internet
Retrofit creates a network API for the app based on the content from the web services. It fetches data from the web service and routes it through a seperate converter library that knows how to decode the data and return it in the form of objects like `String` (`JSON` format).
![image](https://github.com/Xenoare/book-notes/assets/67181778/f42ab187-e3cb-4758-a251-181e192d68f6)

You will impelement the Retrofit service API, with the following steps.
+ Create a network layer, the `MarsApiService` class.
+ Create a Retrofit object with the base URL and the converter factory.
+ Create an interfacce that explains how Retrofit talks to our web server.
+ Create a Retrofit service and expose the instance to the api service to the  rest of the app.

The implementations are below:
1. Create a new pakcage `network` and create a new Kotlin file named `MarsApiSevice`.
2. In `MarsApiService` add the following constant to the base URL
   ```kotlin
   private const val BASE_URL =
      "https://android-kotlin-fun-mars-server.appspot.com"
   ```
3. Add a Retrofit builder and create a Retrofit object.
    ```kotlin
    private val retroit = Retrofit.Builder()
    ```
4. Retrofit needs the base URI for the web service, and a converter factory to bulid a web service API. The converter tells Retrofit what to do with the data it gets back from the service. In this case, you want Retrofit to fetch JSON response from the web service, and return it as a `String`. <br>
    Retrofit has a `ScalarsConverter` that supports strings and other primitive types, so you call `addConverterFactory()` on the builder with an instance of `ScalarsConverterFactory`.
   ```kotlin
   private val retrofit = Retrofit.Builder()
       .addConverterFactory(ScalarsConverterFactory.create())
   ```
5. Add the base URL for the web service using `baseUrl()` and call `build()` to create the **Retrofit Object**
    ```kotlin
    private val retrofit = Retrofit.Builder()
   .addConverterFactory(ScalarsConverterFactory.create())
   .baseUrl(BASE_URL)
   .build()
    ```
6. Below the Retrofit builder, define an interface called `MarsApiService`, that defines how Retrofit talks to the web service using HTTP request. and add a function called `getPhotos()` to get the response string from the web service.
    ```kotlin
    interface MarsApiService {
        fun getPhotos()
    }
    ```
7. Use the `@GET` annotation to tell Retrofit that this is `GET` request, and specify an endpoint, for that website service method. in this case is called `photos`, and specify the type of function to `String`
    ```kotlin
    interface MarsApiService {
        @GET("photos")
        fun getPhotos() : String
    }
    ```

**Object Declaration** <br>
In kotlin, [object declarations](https://kotlinlang.org/docs/reference/object-declarations.html#object-declarations) are used to declare singleton objects. [Singleton pattern](https://en.wikipedia.org/wiki/Singleton_pattern) ensures that one, and only one, instance of an object is created, has one global point of access to that object. Object declaration's initialization is thread-safe and done at first access. <br>
Kotlin makes it easy to declare singletons. Following is an example of an object declaration and its access. Object declaration always has a name following the `object` keyword.
```kotlin
// Object Declaration
object DataProviderManager {
    fun registerDataProvider(provider: DataProvider) {
        // ...
    }
​
    val allDataProviders: Collection<DataProvider>
        get() = // ...
}

// To refer to the object, use its name directly.
DataProviderManager.registerDataProvider(...)
```
The call to `create()` function on a `Retrofit` object is expensive and the app needs only one instance of Retrofit API service. <br>
So, you expose the service to the reset of the app using _objecct declaration_.
1. Outside the `MarsApiService` interface declaration, define a public object called `MarsApi` to initialize the Retrofit service. This is the public singleton object that can be accessed from the rest of the app.
   ```kotlin
   object MarsApi {}
   ```
2. Inside the `MarsApi` object declaration, add a lazily initialized retrofit object property named `retrofitService` of the type `MarsApiService`. You make this lazy initialization, to make sure it is initialized at its first usage. Init the `retrofitService` variable using `retrofit.create()` method with the `MarsApiService` interface.
   ```kotlin
   object MarsApi {
        val retrofitService : MarsApiService by lazy {
               retrofit.create(MarsApiService::class.java)
           }
    }
   ```
    The Retrofit setup is done! Each time your app calls `MarsApi.retrofitService`, the caller will access the same singleton Retrofit object that implements `MarsApiService` which is created on the first access. In the next task, you will use the Retrofit object you have implemented.

* **Call the web service in OverViewModel** <br>
A [ViewModelScope](https://developer.android.com/topic/libraries/architecture/coroutines#viewmodelscope) is the built-in coroutine scope that defined for each `ViewModel` in your app. Any coroutine launched in this scope is **automatically canceled** if the `ViewModel` is clered. <br>
In this context, we are going to use `ViewModelScope` to launch the coroutine and make the Retrofit network call in the background.
4. In `MarsApiService`, make `getPhotos()` a suspend function. **So you can call this method from within a coroutine**.
    ```kotlin
    @GET("photos")
    suspend fun getPhotos(): String
    ```
5. Open the `overview/OverViewModel`. and in `getMarsPhotos()` method, launch the coroutine using `viewModelScope.launch`
   ```kotlin
   private fun getMarsPhotos() {
        viewModelScope.launch {
       }
   }
6. Inside the `viewModelScope`. Use the singleton object `MarsApi`, to call the `getPhotos()` method from the `retrofitService` interface. Save the returned response in a `val` called `listResult`. And assign the result from the server into the `_status.value`.
   ```kotlin
   viewModelScope.launch {
       val listResult = MarsApi.retrofitService.getPhotos()
       _status.value = listResult
   }
   ```

* **Add Internet Permission and Exception Handling** <br>
The purpose of permission on Android is to protect the privacy of an Android user. Android apps must declare or request permission to access **sensitive user data such as contacts, call logs and certain system**. <br>
To learn more about Android permissions and its types [here](https://developer.android.com/guide/topics/permissions/overview).
1. Open the `manifest/AndroidManifest.xml` add this line beore `<application>` tag.
   ```xml
    <uses-permission android:name="android.permission.INTERNET" />
   ```

**Exception Handling** <br>
[Exception](https://developer.android.com/reference/java/lang/Exception) are errors that can occour during the runtime and terminate the app abruptly without notifying the user. Exception handling is a mehcanism by which you preveent the app from terminating abruptly and handle it in a user friendly way. <br>
The examples of potential issues while connection to a server:
+ The URL or URI used in the API is incorrect.
+ The server is unavailable and the app could not connect to it.
+ Network latency issue.
+ Poor or no internet connection on the device.

You can use `try-catch` block to handle the exception in the runtime. Inside the `try` block you will perform the code where you anticipate an exception. 
1. Open `overview/OverViewModel`, and inside the `getMarsPhotos()` method. add a `try` block around `MarsApi` to handle exceptions.
   ```kotlin
   viewModelScope.launch {
       try {
           val listResult = MarsApi.retrofitService.getPhotos()
           _status.value = listResult
       } catch (e: Exception) {}
   }
   ```
2. Inside the `catch` block, handle the failure response by displaying the error message.
    ```kotlin
    catch (e: Exception) {
       _status.value = "Failure: ${e.message}"
    }
    ```

* **Parsing the JSON response with Moshi** <br>
The requested data is typically formatted in one of the common data formats like XML or JSON. Each call returns structured data and your app needs to know what's structure in order to read the data from the response. <br>
From given the data in URL, you will see the structure of the JSON format.
![image](https://github.com/Xenoare/book-notes/assets/67181778/d496dd0b-20ee-4861-8f62-587eb170977e)
+ JSON response is an array, indicated by the square brackets. The array contains JSON objects.
+ The JSON objects are surrounded by `{}`
+ Each JSON objects contain a set of name-value pairs seperated by a comma.
+ The name and avlue in a pair are seperated by a colon.
+ Names are surrounded by quotes.
+ Values can be numbers, strings, a boolean, an array, an objects (JSON objects) or null

There's a external library called [Moshi](https://github.com/square/moshi), which is an Android JSON parser that converts JSON string into Kotlin objets. Retrofit also have these converter that works with Moshi also.

* **Moshi Library Dependencies** <br>
1. Open the `build.gradle (Module: app)`
2. In the dependecies section, add the code shown below to include the Moshi dependency. This dependency adds supports for the Moshi JSON library with Kotlin support.
    ```xml
    // Moshi
    implementation 'com.squareup.moshi:moshi-kotlin:1.9.3'
    ```
3. Replace the Retrofit dependencies
   ```xml
    // Retrofit
    implementation "com.squareup.retrofit2:retrofit:2.9.0"
    // Retrofit with scalar Converter
    implementation "com.squareup.retrofit2:converter-scalars:2.9.0"
   ```
   with this
   ```xml
   // Retrofit with Moshi Converter
   implementation 'com.squareup.retrofit2:converter-moshi:2.9.0'
   ```

* **Implement the Mars Photos data Class** <br>
A sample entry of the JSON response you get from the web service looks like this
```xml
[{
    "id":"424906",
    "img_src":"http://mars.jpl.nasa.gov/msl-raw-images/msss/01000/mcam/1000ML0044631300305227E03_DXXX.jpg"
},
...]
```
In the example above, notice that each Mars photo entry has these JSON key and value pairs:
+ `id`: the ID of the property, as a string. Since it is wrapped in `" "` it is of the type `String` not Integer.
+ `img_src`: The image's URL as a string.

Moshi parses this JSON data and converts it into Kotlin objects. To do this, Moshi needs to have a Kotlin data class to store the parsed results, so in this step you will create the data class, `MarsPhoto`.
1. Make a new data class `MarsPhoto` under the `network package` and add these following class defintion
   ```kotlin
   data class MarsPhoto (
       val id: String, val img_src: String
   )
   ```
Notice that each of the variable in the `MarsPhoto` class represents the `key name` in `JSON` objects. <br>
When Moshi parses the JSON, it matches the keys by name and fills the data objects with appropriate values.

**@JSON Annotation**
Sometimes the key names in a JSON response can make confusing Kotlin properties, or may not match recommended coding style—for example, in the JSON file the `img_src` key uses an underscore, whereas Kotlin convention for properties use upper and lowercase letters ("camel case").

To use variable names in your data class that differ from the key names in the JSON response, use the `@Json` annotation. In this example, the name of the variable in the data class is `imgSrcUrl`. The variable can be mapped to the JSON attribute img_src using @Json(`name = "img_src"`).
5. Replace the line of `img_src` key with this
```kotlin
@Json(name = "img_src")
val imgSrcUrl: String
```

* **Update the MarsApiService and OverviewViewModel** <br>
You will replace `ScalarsConverterFactory` with the `KotlinJsonAdapterFactory` to let `Retrofit` know it can use `Moshi` to convert the `JSON` response into Kotlin objects. You will then update the network API and `ViewModel` to use the Moshi object.
1. Open `network/MarsApiService`. Notice that the `ScalarsConverterFactory` is unresolve reference error becuase we change the `Retrofit Dependency`.
2. At the top of the, file, just before the Retrofit bulder, add the following code to create the Moshi object, simillar to the Retrofit object.
    ```kotlin
    private val moshi = Moshi.Builder()
    ```
3. For `Moshi` annotations to work properly with Kotlin, in the Moshi Builder, add the `KotlinJsonAdapterFactory` and then call build().
    ```kotlin
    private val moshi = Moshi.Builder()
        .add(KotlinJsonAdapterFactory())
        .build()
    ```
4. In the `retrofit` object declaration change for the `Retrofit` builder to use the `MoshiConverterFactory` intead of the `ScalarConverterFactory`, and pass in the `moshi` instance you just created.
    ```kotlin
    private val moshi = Moshi.Builder()
        .add(KotlinJsonAdapterFactory()
        .build()
    ```
5. In the `retrofit` object declaration change the Retrofit builder to use the `MoshiConverterFactory` instead of the `ScalarConverterFactory` and pass the `moshi` instance that just been created.
    ```kotlin
    private val retrofit = Retrofit.Builder()
       .addConverterFactory(MoshiConverterFactory.create(moshi))
       .baseUrl(BASE_URL)
       .build()
    ```
6. Now that you have `MoshiConverterFactory` in place, you can ask Retrofit to return a list of `MarsPhoto` objeccts from JSON array instead of returning a JSON string. Update the `MarsApiService` interface to have Retrofit return a lsit of `MarsPhoto` objects, instead of `String`.
   ```kotlin
   interface MarsApiSerice {
       @GET("photos")
       suspend fun getPhotos(): List<MarsPhotos>
   }
   ```
7. Do similar changes to the `viewModel`. open `OverviewViewModel` in the `getMarsPhotos()` method, `listResult` is a `List<MarsPhotos>` not a `String` anymore. <br>
    The size of that list is the number of photos that were reeived and parsed. To print the number of photos retrieved update `_status.value` as follows
   ```kotlin
   _status.value = "Success: ${listResult.size} Mars photos retrieved"
    ```

### Load and display an Image from internet
In order to display a photo from web URL. The image has to be downloaded, internally stored and decoded from its compressed format to an image that Android can use. <br>
Fortunately, you can use a community-developed library called [Coil](https://coil-kt.github.io/coil/) to download, buffer, decode and cache your images. <br>
Coil basically needs two things:
+ The URL of the image you want to load and display.
+ An `ImageView` object to actually display that image.

**Add Coil dependancy**
1. In the `dependencies` `build.gradle (Module: app)`, add this Coil library
    ```xml
        // Coil
        implementation "io.coil-kt:coil:2.2.2"
    ```
2. Coil library is hosted and available on the `mavenCentral()` repo. In `build.gradle (Project: MarsPhotos)` add `mavenCentral()` in the top repositories block.
   ```xml
   repositories {
       google()
       mavenCentral()
    }
   ```

**Update the ViewModel** <br>
In this step, you will add a `LiveData` property to the `OverviewViewModel` class to store the Kotlin object received, MarsPhoto.
1. Open `overview/OverviewViewModel`. add a new mutable property called `_photos` of the type `MutableLiveData` that can store a single `MarsPhoto` object
   ```kotlin
   privat val _photo = MutableLiveData<MarsPhoto>
   ```
2. Add a `backing field` called `photos` of the type `LiveData<MarsPhoto>`
   ```kotlin
   val photos: LiveData<MarsPhoto>
    get() = _photos
   ```
3. In the `getMarsPhotos()` method, inside the `try{}` block. Assign the first Mars photo retrieved to the new variable `_photos`. Assign the first photos url at the index `0`. This will throw an error that you will fix later.
    ```kotlin
    try {
        _photos.value = MarsApi.retrofitService.getPhotos()[0]
    }
    ```
4. In the next line, update the `status.value` to display the first image URL from the photo List.
    ```kotlin
    try {
        _photos.value = Mars.retrofitService.getPhotos()[0]
        _status.value = "First Mars image URL : ${_photos.value!!.imgSrcUrl}
    }
    ```

* **Use Binding Adapters** <br>
Binding adapters are annotated method thah used to create a custom setters for custom properties of your view. <br>
Usually when you set an attribute in your XML using the code: `android:text="Sample Text"`. The Android system automatically looks for a setter with the same name as the `text` attribute, which is set by the `setText(String: text)` method. The `setText(String: text)` method is a setter method for some views provided by the Android Framework. <br>
**Example of a Binding Adapter**
```kotlin
@BindingAdapter("imageUrl")
fun bindImage(imgView: ImageView, imgUrl: String?) {
    imgUrl?.let {
        // Load the image in the background using Coil.
        }
    }
}
```
+ The `@BindingAdapter` annotation takes the attribute name as its parameter.
+ In the `bindImage` method, the first method parameter is the type of the target View and the second is the value being set to the attribute.
+ Inside the method, the Coil library loads the image off the UI thread and sets it into the `ImageView`.

* **Create a binding adapter and use Coil** <br>
1. Create a kotlin file inside the `com.example.android.marsphotos` package called `BindingAdapters`. This file will hold the binding adapters that you use throughput the app.
2. In `BindingAdapter`, create a method `bindImage()` function as a `top-level function` (not inside a class) that takes an `ImageView` and a `String` as parameters.
   ```kotlin
   fun bindImage(imgView: ImageView, imgUrl: String?) { }
   ```
3. Annotate the function with `@BindingAdapter`. The `@BindingAdapter` annotation tells `data binding` to execute this binding adapter when a `View item` has the imageUrl attribute.
   ```kotlin
   @BindingAdapter("imageUrl")
   fun bindImage(imgView: ImageView, imgUrl: String?) {}
   ```

**Let Scope function** <br>
`let` is one the Kotlin's sccope function which lets you execute a code block within the context of an object.
+ `let` is used to invoke one or more unctions on results of call chains.
+ The `let` function along with the safe call operator (`?.` is used to perform a null safe operation on the object.

4. add a `let{}` block to tthe `imgUrl` argument with safe call operator. Add the following line to convert the URL string to a `Uri` object using the `toUri()` method. To use the HTTPS schme, append `buildUpon.scheme("https") to the `toUri` builder. Call `bulid()` to build the object.
    ```kotlin
    val imgUri = imgUrl.toUri().buildUpon().scheme("https").build()
    ```
5. After `imgUri` declaration, use the `load()` to load the image from the `imgUri` object into the `imgView`
   ```kotlin
   imgView.load(imgUri) {}
   ```
6. Here's the complete code
   ```kotlin
   @BindingAdapter("imageUrl")
    fun bindImage(imgView: ImageView, imgUrl: String?) {
        imgUrl?.let {
            val imgUri = imgUrl.toUri().buildUpon().scheme("https").build()
            imgView.load(imgUri) 
        }
    }
   ```

* **Update the layout and fragments** <br>
1. Update the `<ImageView>` element in `grid_view_item.xml`. Add data element for data binding and bind to the `OverviewViewModel` class.
    ```xml
    <data>
        <variable
            name="viewModel"
            type="com.example.android.marsphotos.overview.OverviewViewwModel" />
    </data>
    ```
2. Add an `app:imageUrl` attribute to the `ImageView` element to use the new image loading from binding adapter. <br>
    Remember that the `photos` contain a list of `MarsPhotos` retrieved from the server. Assign the first entry `URL` to the `imageUrl` attribute.
   ```xml
       <ImageView
        android:id="@+id/mars_image"
        ...
        app:imageUrl="@{viewModel.photos.imgSrcUrl}"
        ... />
   ```
3. Open the `OverviewFragment`, in the `onCreateView()` comment the lines that inflate the `FragmentOverviewBindning` class and change with `GridViewItemBindin` class instead.
   ```kotlin
   //val binding = FragmentOverviewBinding.inflate(inflater)
   
    val binding = GridViewItemBinding.inflate(inflater)
   ```

* **Add loading and error images** <br>
Using Coil can improve the user exprerience by showing a placeholder image while loading the image and an error image if the loading fails. 
1. In the `bindImage()` method, update the call to `imgView.load(imgUri)` to add a trailing lambdas. This code sets the placeholder loading image to use while loading (the `loading_animation` drawbale). This code also sets an image to use if image loading fails (the `broken_image` drawable)
   ```kotlin
   @BindingAddapter("imageUrl")
   fun bindImage(imgView: ImageView, imgUrl: String?) {
       imgUrl?.set {
           val imgUrl = imgUrl.toUri().buildUpon().schme("https").build()
           imgView.load(imgUri) {
               placeholder(R.drawable.loading.animation)
               error(R.drawable.ic_broken_image)
           }
       }
   }

### Display a Grid of Images with RecyclerView
* **Update the View Model** <br>
In prev task, in the `OverviewViewModel`, you've added an `LiveData` object called `_photos` that holds one `MarsPhoto` object - _the first one in the response_ list from the web service. Now, we will change this `LiveData` to hold the entire list of `MarsPhoto` objects.
1. in the `OverviewViewModel`, change the `_photos` type to be list of `MarsPhoto` objects, also don't forget to replace the backing property of `photos`
    ```kotlin
    private val _photos = MutableLiveData<List<MarsPhoto>>()
    val photos: LiveData<List<MarsPhoto>> = _photos
    ```
2. Change the `_photos.value` and _status.value so it returns list of `MarsPhoto` objects
   ```kotlin
    try {
        _photos.value = MarsApi.retrofitService.getPhotos()
        _status.value = "Success: Mars properties retrieved"
    } catch (e: Exception) {
        _status.value = "Failure: ${e.message}"
    }
   ```

* **Grid Layout** <br>
Grid layout arranges items in a grid of rows and columns. Assuming vertical scrolling, by default, each item in a row takes up one "span." An item can occupy multiple spans. In the case below, one span is equivalent to the width of one column that is 3.
![image](https://github.com/Xenoare/book-notes/assets/67181778/313a1e53-75df-4f9b-bb1f-d771f7c44b3d)

* **Add RecyclerView** <br>
1. Open `grid_view_item.xml` and change the `<data>` content tags
    ```xml
    <data>
       <variable
           name="photo"
           type="com.example.android.marsphotos.network.MarsPhoto" />
    </data>
    ```
2. Also in `<ImageView>`, change the `app:imageUrl` attribute to refer to the image URL in the `MarsPhoto` objects.
    ```xml
    app:imageUrl="@{photo.imgSrcUrl}"
    ```
3. Now open the `fragment_overview.xml`. Delete the entire `<TextView>` element. and add the following `<RecyclerView>` element instead. <br>
    Set the Id to `photos_grid`, `widht` and `height` attributes are `0dp`, so it fills the parent `ConstraintLayout`. <br>
    Since you'll be using GridLayout, so set the `layoutManager` attribute to be `androidx.recyclerview.widget.GridLayoutManager`. Set a `spanCount` to `2` so you'll have 2 columns.
    ```xml
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/photos_grid"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layoutManager=
           "androidx.recyclerview.widget.GridLayoutManager"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:spanCount="2" />
    ```
4. To see a preview of what the above code looks like in the `Design` view, use tools:itemCount to set the number of items displayed in our layout to `16`. The itemCount attribute specifies the number of items the layout editor should render in the Preview window. Set the layout of list items to grid_view_item using tools:listitem.
    ```xml
    <androidx.recyclerview.widget.RecyclerView
            ...
            tools:itemCount="16"
            tools:listitem="@layout/grid_view_item" />
    ```
5. According to the [Material design guidelines](https://material.io/components/image-lists#anatomy), you should hae `8dp` of space at the `top, bottom and sides` of thes list, and `4dp` of space between the items. You can achive this with a combination of padding in `fragment_overview.xml` layout and in `grid_view_item.xml` layout.
![image](https://github.com/Xenoare/book-notes/assets/67181778/42d7dcec-440d-4c3e-8341-a8a6955ac57f)

6. Since we're already got `2dp` paddings in `gridview_item.xml`, we'll need an additoinal `6dp` of padding on the outside edges to match the deisng guidelines. Here's the complete layout
    ```xml
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/photos_grid"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:padding="6dp"
        app:layoutManager=
            "androidx.recyclerview.widget.GridLayoutManager"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:spanCount="2"
        tools:itemCount="16"
        tools:listitem="@layout/grid_view_item"  />
    ```

* **ListAdapter** <br>
[List Adapter](https://developer.android.com/reference/androidx/recyclerview/widget/ListAdapter) is a subclass of the [RecyclerView.Adapter](https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView.Adapter) class for presenting List data in a `RecycleView`, including computing diff between Lists on a background thread. <br>
We're also will use the `DiffUtil` implementation in the `ListAdapter`. The advantage of using `DiffUtil` is every time some item in the `RecyclerView` is added, removed or changed, the whole list doesn't get refreshed. Only the items that have been changed are refreshed.
1. Add a Kotlin class called `PhotoGridAdapter` and extend the `PhotoGridAdapter` class from `ListAdapter`.
    ```kotlin
    class PhotoGridAdapter : ListAdapter<MarsPhoto,
        PhotoGridAdapter.MarsPhotoViewHolder>(DiffCallback) {
    }
    ```
2. Implement `onCreateViewHolder`, `onBindViewHolder` and `MarsPhotoViewHolder`. Inside the `PhotoGridAdapter`. Add an inner class definition for `MarsPhotoViewHolder` which extands `RecyclerView.ViewHolder`. You need the `GridViewItemBinding` variable for binding the `MarsPhoto` to the layout, so pass the variable into the `MarsPhotoViewHolder`. The base `ViewHolder` class requires a view in its contructor, you pass it the binding root view.
    ```kotlin
    class MarsPhotoViewHolder(private var binding: GridViewItemBinding) :
        RecyclerView.ViewHolder(binding.root) {
    }
    ```
3. In `MarsPhotoViewHolder`, create a `bind()` method that takes a MarsPhoto object as an argument and sets `binding.property` to that object. Call `executePendingBindings()` after setting the property, which causes the update to execute immediately.
    ```kotlin
        /**
     * The MarsPhotosViewHolder constructor takes the binding variable from the associated
     * GridViewItem, which nicely gives it access to the full [MarsPhoto] information.
     */
    class MarsPhotosViewHolder(
        private var binding: GridViewItemBinding
    ) : RecyclerView.ViewHolder(binding.root) {
        fun bind(marsPhoto: MarsPhoto) {
            binding.photo = marsPhoto
            // This is important, because it forces the data binding to execute immediately,
            // which allows the RecyclerView to make the correct view size measurements
            binding.executePendingBindings()
        }
    }
    ```
4. In `onCreateViewHolder()` neeeds to return a new `MarsPhotoViewHolder`, craeted by inflating the `GridViewItemBinding` and using the `LayoutInflater` from your parent `ViewGroup` context.
    ```kotlin
        /**
     * Create new [RecyclerView] item views (invoked by the layout manager)
     */
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): PhotoGridAdapter.MarsPhotoViewHolder {
        return MarsPhotoViewHolder(GridViewItemBinding.inflate(LayoutInfalter. from(parent.context)))
    }
    ```
5. In `onBindViewHolder` method, we call `getItem()` to get the `MarsPhoto` object associated with the current `RecyclerView` position, and then pass that property to the `bind()` method in the `MarsPhotoViewHolder`.
   ```kotlin
       /**
     * Replaces the contents of a view (invoked by the layout manager)
     */
   override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): PhotoGridAdapter.MarsPhotoViewHolder {
        val marsPhoto = getItem(position)
        holder.bind(marsPhoto)
    }
   ```
6. Inside the `PhotoGridAdapter`, add a companion object definition for `Diffcallback`. <br>
The `DiffCallback` object extends `DiffUtil.ItemCallback` with the generic type of object you want to compare—`MarsPhoto`. You will compare two Mars photo objects inside this implementation.  
    ```kotlin
    companion object DiffCallback : DiffUtil.ItemCallback<MarsPhoto>() {
    }
    ```
7. This is will create a `comparator methods` for the `DiffCallback` object, which are `areItemsTheSame()` and `areContentsTheSame()`.
    ```kotlin
    override fun areItemsTheSame(oldItem: MarsPhoto, newItem: MarsPhoto): Boolean {
       TODO("Not yet implemented") 
    }

    override fun areContentsTheSame(oldItem: MarsPhoto, newItem: MarsPhoto): Boolean {
   TODO("Not yet implemented") 
   }
   ```
8. In the `areItemsTheSame()` methods, this methods is called by `DiffUtil` to decide whether two objects represents the same Item. <br>
    `DiffUtil` uses this method to figure out if the new `MarsPhoto` objects is the same as the old `MarsPhoto` objects. The `ID` of every item (`MarsPhoto` object) is unique. Compare the IDs of `oldItem` and `newItem`
   ```kotlin
   override fun areItemsTheSame(oldItem: MarsPhoto, newItem: MarsPhoto): Boolean {
       return oldItem.id == newItem.id
    }
    ```
9. In `areContentsTheSame()`, this methods is called by `DiffUtil` when it wants to check whether two items have the same data. The imporatnt data in the `MarsPhoto` is the `image URL`. Compare the URLs of `oldItem` and `newItem` and return the result.
    ```kotlin
    override fun areContentsTheSame(oldItem: MarsPhoto, newItem: MarsPhoto): Boolean {
       return oldItem.imgSrcUrl == newItem.imgSrcUrl
    }
    ```

* **Add the binding adapter and connect the parts** <br>
In this step we will use a `BindingAdapter` to init the `PhotoGridAdapter` with the list of `MarsPhoto` objects. Using `BindingAdapter` to set the `RecyclerView` data causes data binding to automatically observer the `LiveData` for the list of `MarsPhoto` objects. Then the binding adapter is called automatically when the `MarsPhoto` list changes.
1. Open `BindingAdapters` and add a `bindRecyclerView()` methods that takes a `RecyclerView` and a list of `MarsPhoto` objects as argumetns. Annotate that method with a `@BindingAdapter` with `listData` attribute
    ```kotlin
    @BindingAdapter("listData")
    fun bindRecyclerView(recyclerView: RecyclerView, data: List<MarsPhoto>?) {
    }
    ```
2. Inside the `bindRecyclerView()` function, cast `recyclerView.adapter` to `PhotoGridAdapter` and assign it to a new `val` property `adapter`.
3. And at the end of this method, call `adapter.submitList()` with the Mars photos list data. This tells the `RecyclerView` when a new list is available
    ```kotlin
    @BindingAdapter("listData")
    fun bindRecyclerView(recyclerView: RecyclerView,
                        data: List<MarsPhoto>?) {
       val adapter = recyclerView.adapter as PhotoGridAdapter
       adapter.submitList(data)
    
    }
    ```
4. To connect everything together, in `fragment_overview.xml`. Add the `app:listData` attribute to the `RecyclerView` elemnt and set it to `viewModel.photos` using data binding.
   ```
   # fragment_overview.xml

   <androidx.recyclerview.widget.RecyclerView
        app:listData="@{viewModel.photos}"
        ...
       />
    ```
5. Open `OverviewFragment`. In `onCreateView()`, just before the `return` statement. Init the `RecyclerView` adapter in `binding.photosGrid` to a new `PhotoGridAdapter` object.
    ```kotlin
    binding.photosGrid.adapter = PhotoGridAdapter()
    ```
    ![image](https://github.com/Xenoare/book-notes/assets/67181778/40a8bae3-635a-43ef-bf26-3d78c02c20bd)

* **Add error handling in RecyclerView** <br>
In this time, we will add a basic error handling, to give the user a better idea of what's happening. <br>
In this task, you will create a property in the `OverviewViewModel` to represent the status of the web request. There are three states to consider—loading, success, and failure. The loading state happens while you're waiting for data. The success status is when we retrieve data successfully from the webservice. The failure status indicates any network or connection errors.

**Enum Classes** <br>
In Kotlin, an `enum` is a data type that can hold a set of constants. They are defined by adding the keyword `enum` in front of a class definition as shown below. Enum constants are separated with commas.
```kotlin
enum class Direction {
    NORTH, SOUTH, WEST, EAST
}
```
Usage
```kotlin
var direction: Direction = Direction.NORTH
```
1. Create a `enum` class that represents the available status.
   ```kotlin
   enum class MarsApiStatus {LOADING, ERROR, DONE}
   ```
2. Create a definition of status properties in `OverviewViewModel`
   ```kotlin
   private val _status = MutableLiveData<MarsApiStatus>()

   val status: LiveData<MarsApiStatus> = _status
   ```
3. Setup the mechanism getting `_status.value` in `getMarsPhotos()` to the `MarsApiStatus` enum states
   ```kotlin
   private fun getMarsPhotos() {
       viewModelScope.launch {
            _status.value = MarsApiStatus.LOADING
            try {
               _photos.value = MarsApi.retrofitService.getPhotos()
               _status.value = MarsApiStatus.DONE
            } catch (e: Exception) {
               _status.value = MarsApiStatus.ERROR
               _photos.value = listOf()
            }
        }
    }
   ```
You have defined enum states for the status and set the loading state at the beginning of the coroutine, set done when your app is finished retrieving the data from the web server, and set error when there is an exception. In the next task you will use a binding adapter to display the corresponding icons.

* **Add a binding adapter** <br>
Let's make this appear in the app. We will use Binding Adapter for an `ImageView` to display icons for the **loading and error states**.
1. Open `BindingAdapters` and add a new binding adapter called `bindStatus()` that takes an `ImageView` and `MarsApiStatus` value as arguments. Annotate `@BindingAdapter` passing in the custom attribute `marsApiStatus` as parameter.
    ```kotlin
    @BindingAdapter("marsApiStatus")
    fun bindStatus(statusImageView: ImageView, 
          status: MarsApiStatus?) {
    }
    ```
2. Add a `when {}` block inside the `bindStatus()` method to swtich between the diffrent states. In case for loading state (`MarsApiStatus.LOADING`), for this state, set the `ImageView` to visible and assign it the loading animation. This is same animation drawable you could use or Coil
    ```kotlin
    when (status) {
        MarsApiStatus.LOADING -> {
            statusImageView.visibility = View.VISIBLE
            statusImageView.setImageResource(R.drawable.ic_connection_error)
        }
    }
    ```
3. Add a case for the error state, which is `MarsApiStatus.ERROR`. Similarly to what you did for the `LOADING` state, set the status ImageView to visible and use the connection-error drawable.
   ```kotlin
   MarsApiStatus.ERROR -> {
       statusImageView.visibility = View.VISIBLE
       statusImageView.setImageResource(R.drawable.ic_connection_error)
   }
   ```
4. Add a case for the done state, which is `MarsApiStatus.DONE`. Here you have a successful response, so set the visibility of the status ImageView to View.GONE to hide it.
    ```kotlin
        MarsApiStatus.DONE -> {
       statusImageView.visibility = View.GONE
    }
    ```
5. Add the status ImageView in the `fragment_overview.xml`. Add the `ImageView` below the `RecyclerView` element
    ```xml
    <ImageView
   android:id="@+id/status_image"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:marsApiStatus="@{viewModel.status}" />
    ```
    The above `ImageView` has the same constraints as the `RecyclerView`. However, the width and height use `wrap_content` to center the image rather than stretch the image to fill the view. Also notice the `app:marsApiStatus` attribute set to `viewModel.status`, which calls your `BindingAdapter` when the `status` property in the `ViewModel` changes.
   ![image](https://github.com/Xenoare/book-notes/assets/67181778/da266d23-5208-4fd2-9397-4067ead1d677)

## Relational Database
Notes:
+ [SQL Intro](https://github.com/google-developer-training/android-basics-kotlin-sql-basics-app)
+ [Bus Schedule](https://github.com/google-developer-training/android-basics-kotlin-bus-schedule-app/tree/starter)
+ [Aggregate functions](https://www.codecademy.com/learn/learn-sql/modules/learn-sql-aggregate-functions/cheatsheet)
+ [Joins](https://www.w3schools.com/sql/sql_join.asp)

Table of Contents:
+ [Relational Database](#relational-database)
+ [Room and Flow](#introduction-to-room-and-flow)

#### Relational database
A relational database is a common type of database that organizes data into tables, columns, and rows. When writing Kotlin code, you create classes that represent objects. A table in a relational database works the same way. Besides representing data, tables can also reference other tables so that you can have relationships between them. A classic example would be a table of "students", "teachers," and "course". 
![image](https://github.com/Xenoare/book-notes/assets/67181778/f3a3c6b4-a354-4814-a280-d0541bbbd11f)

+ You can use variety of clauses in a `SELECT` statement including `WHERE`, `GROUP BY`, `ORDER BY` and `LIMIT` to make your quaries more specific.
+ You can use aggregate functions to combine data from multiple rows into a single column.
+ You can add, update and delete rows in a database using the SQL `INSERT`, `UPDATE`, and `DELETE` statements repectively.

#### Introduction to Room and Flow
An easy way to use a database in an Android app, is with library called `Room`. Room is what's called an `ORM` (`Object Relational Mapping`) library, which maps the tables in **relational database** to **objects usable** in Kotlin code. 

* **Add Room Dependancy** <br>
First things, that we can define the `Room` dependancy to be able to use room.
    ```kotlin
    // build.grade (project-level)
    ext {
       kotlin_version = "1.6.20"
       nav_version = "2.4.1"
       room_version = '2.4.2'
    }
    ```
    Next, we can define other depnedancies on app level gradle
    ```kotlin
    // build.grade (app-level)
    ext {
    implementation "androidx.room:room-runtime:$room_version"
    kapt "androidx.room:room-compiler:$room_version"
    
    // optional - Kotlin Extensions and Coroutines support for Room
    implementation "androidx.room:room-ktx:$room_version"}
    ```

* **Create an Entitiy** <br>
When working with Room, each table is repersented by a class. In an `ORM` library such as Room, there are often called _model classes_, or _entities_.
The database for the Bus Schedule app jsut consist of a single table, schedule, which includes basic information about a bus arrival.
+ `id`: An integer providing a unique identifier that serves as the primary key.
+ `stop_name`: A string
+ `arrival_time`: An integer
When working with Room, however, you should only be concerned with the Kotlin types when defining your model classes. **Mapping** the data types in your model class to the ones used in the database. <br>

When a project has many files, consider organizing your files in different package to provide better access control for each class and to make it easier to locate related classes. <br>

To create an entity for the "schedule" table, add a new **package** called `database`. Within that package, add a new package called `schedule` for the **entitiy**. Then in `database.schedule` package, create a new file called `Schedule.kt` and define a data class called `Schedule`.
```kotlin
data class Schedule ()
```
Define the primary key to uniquely idenfity the each row. The first property you'll add to the `Schedule` class is an integer to represent a unique id. Add a new property and mark it with the `@PrimaryKey` annotation.
```kotlin
@PrimaryKey val id: Int
```
Add a column name of the bus stop. The column should be type `String`. For new columns, you'll to add a `@ColumnInfo` annotations to specify a name for the column. Typically SQL column names will have **words** _seperated by an underscore_ as opposed to the `lowerCamalCase` used by Kotlin properties. For this column, we also don't want the value to be null. so you should mark it with `@NonNull` annotations.
```kotlin
@NonNull @ColumnInfo(name = "stop_name") val stopName: String,
```
Arrival times are represented in the database using integers. This is [Unix timestamp](https://www.unixtimestamp.com/) that can be converted into a usable date. While different versions of SQL offer ways to converts dates, for your purposes, you'll stick Kotlin date formatting functions.
```kotlin
@NonNull @ColumnInfo(name = "arrival_time") val arrivalTime: Int
```
By default, Room uses the class name as the database table name. Thus, the table name as defined `@Entity(tableName="schedule")`, but since Room are not case sensitive, you can omit the table name.
```kotlin
@Entity
data class Schedule(
    @PrimaryKey val id: Int,
    @NonNull @ColumnInfo(name = "stop_name") val stopName: String,
    @NonNull @ColumnInfo(name = "arrival_time") val arrivalTime: Int )
```

* **Define the DAO** <br>
DAO stands or Data Access Objects and is a Kotlin class that provides access to the data. <br>
Specifically, the DAO is where would you include 
