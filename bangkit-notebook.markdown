# Dedicated Bangkit Notebook
This page is dedicated for any note taking about material about mobile development, machine learning and cloud computing as long myself in Bangkit Periode.

## Material Design Concept in Kotlin 📱
> [!NOTE]
> Ceb, March 2024


### Material Design 1
+  The first principle of `Material Design` are `Material is the Metaphor`, is meaning that the Material is grounded in `Tactile Reality`, Surfaces and edges provides visual cues that are grounded in reality, creating the sense of touch with the combination of the fundamentals of light, surface and movement in how the objects move, reacts and exist in space[^1].
+  The second principle is `Bold, Graphic, Intentional`, where the fundamental elements, such as `Typography`, `Grid`, `Space`, `Color` give the hierarchy, meaning and focus that immerse the user in the experiance.
+  The last principle is `Motion Provides Meaning`, where this implies the `User` as the Prime Mover. Primary user actions initiate motion and transform the whole design. Motion is meaningful and appropriate, serving to focus attention and maintain continuity.
+  The material environment are belong in the 3D space, where each objects have `x,y,z` dimension with each of the Material occupies the a single position along the `Z`-axis and has the standard `1dp` of thickness[^2].
+ Material also depict the make shadow by the elevation between overlapping material[^3].
+ Objects in `Material Design` posses similar qualities to objects in the physical world[^4].
+ Elevation measurement of the relative depth, or distance, between two objects along the `Z`-axis.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/de6aeecf-141f-4b57-bae8-56c8eed0ceff" width="743px" alt="Elevation Concept">
    <p>Multiple elevation measurements for two objects</p>
</div>

+ All material objects, have the resting elevation or default elevation that does not chnage. If the objects changes elevation, it should be return to the resting position elevation as soon as possible.
    | Elevation (dp) 	| Component                                                                                                  	|
    |----------------	|------------------------------------------------------------------------------------------------------------	|
    | 24             	| Dialog Picker                                                                                              	|
    | 16             	| Nav drawer, Right drawer, Modal bottom Sheet                                                                 	|
    | 12             	| Floating action button (FAB - pressed)                                                                     	|
    | 9              	| Sub menu (+1dp for each sub menu)                                                                          	|
    | 8              	| Bottom navigation bar, Menu, Card (when picked up), Raised button (pressed state)                             |
    | 6              	| Floating action button (FAB - resting elevation), Snackbar                                                  	|
    | 4              	| App Bar                                                                                                    	|
    | 3              	| Refresh indicator, Quick entry / Search bar (scrolled state)                                                	|
    | 2              	| Card (resting elevation) * Raised button (resting elevation)* Quick entry / Search bar (resting elevation) 	|
    | 1              	| Switch                                                                                                     	|

+ Some component have responsive elevation, meaning that they change elevation in response to the user input (such as normal, focused and pressed) or system events. This often called as the `dynamic elevation offset`
+ To summary how the elevation works in the nutshell. Here's some following diagram compares about the `component` elevation changes offset.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/278cca51-c854-437b-976a-b86c36e0d046" width="743px" alt="Elevation Concept">
    <p>Multiple elevation measurements for two objects</p>
</div>

+ `Motions` shows an app is organized and what it can do. Basically, it provides a focus between views[^5].
+ The material environment draws inspiration from real world scenarios such as the `gravity` and `friction`.
+ These forces are reflected in the way the user input affects element on screen and how elements react to each other.
+ Basically, the material in motion has some following characteristic:

    | Responsive  | Materials is full of energy. It quickly responds to the user input                                                                                                |
    |------------ |-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Natural     | In the real world, an ability to speed up or slow quickly is affected by the friction and weight                                                                  |
    | Aware       | Material is aware of its surrounding, including the user and other material around it, it can be attracted to elements and respond appropriate to the user intent |
    | Intentional | Material in motion guides focus to the right spot at the right moment                                                                                             |

+ Here's some common duration based on the `Material Durations` based on

Mobile
General Transitions: Typically occur over 300ms.
Large, Complex, Full-Screen Transitions: May have longer durations, occurring over 375ms.
Elements Entering the Screen: Occur over 225ms.
Elements Leaving the Screen: Occur over 195ms.
Tablets
Durations on tablets should be about 30% longer than on mobile. For example, a 300ms mobile duration would increase to 390ms on tablets.
Wearables
Durations on wearables should be about 30% shorter than those on mobile. For example, a 300ms mobile duration would be 210ms on wearables.
Desktop
Desktop animations should be faster and simpler than their mobile counterparts. These animations should last 150ms to 200ms.



> Reference foot note:
> [^1]: https://m1.material.io/material-design/introduction.html#introduction-principles.
> [^2]: https://m1.material.io/material-design/environment.html#environment-3d-world
> [^3]: https://m1.material.io/material-design/elevation-shadows.html#elevation-shadows-elevation-android
> [^4]: https://m1.material.io/material-design/elevation-shadows.html
> [^5]: https://m1.material.io/motion/material-motion.html#material-motion-how-does-material-move
