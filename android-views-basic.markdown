### Introduction to Activities
* > Kotlin Style Guide: https://developer.android.com/kotlin/style-guide

---
An `Activity` provides the window which your apps draws its UI. Typically, an `Activity` takes up the whole screen of your running app. Every app has one or more activites.

The top-level or first activity is often called the `MainActivity` and is provided by the project template.

For more complicated apps, there may be multiple screens and more than one activity. Each activity has a specific purpose.

For example, in photo gallery app, you could use `Activity` for displaying a grid of photos, a second `Activity` for viewing an individual photo and, third `Acitivity` for editing individual photo.
![image](https://github.com/Xenoare/book-notes/assets/67181778/a4e666e8-bae7-44fc-bde5-e918f0e1c373)

### Note
Android automatically assigns ID number to the resoureces in your app. (Roll button has a resource ID and etc. Resource IDs are of the form `R.<type>.<name>` such as `R.string.roll`. For view ID, the type is id (`R.id.button`).

### Project Lemonade
---
1. Build the user interface
The lemonade app just requires a basic layout which consist of 2 views.
- A `TextView` which provides instruction to the user.
- An `ImageView` which shows a graphic based on the current state of the app (such that a lemon to be squeezed).
- 
