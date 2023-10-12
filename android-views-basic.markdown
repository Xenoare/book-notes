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
        android:id="@+id/plain_text_input"
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
---
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
```yaml
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

