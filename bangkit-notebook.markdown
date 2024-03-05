# Dedicated Bangkit Notebook
This page is dedicated for any note taking about material about mobile development, machine learning and cloud computing as long as myself in Bangkit Periode.

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
  
    | Mobile                                                                                     |
    |--------------------------------------------------------------------------------------------|
    |1. General Transitions: Typically occur over 300ms.                                         |
    |2. Large, Complex, Full-Screen Transitions: May have longer durations, occurring over 375ms.|
    |3. Elements Entering the Screen: Occur over 225ms.                                          |
    |4. Elements Leaving the Screen: Occur over 195ms.                                           |
    
    | Tablets                                                                                                                          |
    |----------------------------------------------------------------------------------------------------------------------------------|
    |1. Durations on tablets should be about 30% longer than on mobile. For example, a 300ms mobile duration would increase to 390ms on tablets.|
       
    | Wearables                                                                                                                         |
    |-----------------------------------------------------------------------------------------------------------------------------------|
    |1. Durations on wearables should be about 30% shorter than those on mobile. For example, a 300ms mobile duration would be 210ms on wearables.|
       
    | Desktop                                                                                                                           |
    |-----------------------------------------------------------------------------------------------------------------------------------|
    |1. Desktop animations should be faster and simpler than their mobile counterparts. These animations should last 150ms to 200ms.    |

+ Material in motion abides by forces similar to those in the real world, like gravity. There are two different movement like `On-screen-movement` and `in-and-out-screen movement`
+ For the movement wihin the on-screen, it must follow the standard `curve` movement like the `Arc-upward` to represent the element that rising up against the gravity[^6].
+ `Arc-downward` represnts the falling elements in the real world that got accelerated by the gravity.
+ The element that moving along the a single axis (either horizontally, or vertically) do not follow an arc.
+ Element that entering and exisiting the screen are referred to as an independent element as they don't affect the position on the screen.
+ One such example is that the entering the screen it will be on the `deceleration curve`, and `acceleration curve` to speed up the items as leaving the screen.
+ When material changes shape and size, its width and height change asyncronously along the motion curve[^7].
+ Lastly, `Radial Transformation` are symetrical. Radial transformation should be used on `Circular surfaces` that morph into rectangular surfaces, or for creating new surfaces from the point of input (One obvious example is that a `Floating Action Button`).
+ In `Material Design`, a `Primary Color` refers to a color that appears most frequently in the app[^8].
+ To create a contrast between elements, you can use the lighter or darker tones of your primary color. The constrast between the surfaces, such as between the status bar and a toolbar.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/66a42d75-7fe7-4bb8-8fa4-10cab23ec7bc" width="743px" alt="Primary Color">
    <p>Color scheme contains different tones of the primary color, for when the ligther and darker contrast is needed.</p>
</div>

+ A `Secondary Color` is being used to accent parts of your UI. It should be constrast with the elements that surround it can be applied sparingly as an accent. Secondary color are great to use for
  
    | Buttons, floating action button (FAB), and button text |
    | -------------------------------------------------------|
    | Text fields, cursorm and text selection                |
    | Progress bar                                           |
    | Selection control, button and slider                   |
    | links                                                  |
    | Headlines                                              |
  
<div style="display: block; margin: auto; text-align=center" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/78abfa01-6525-47a0-944d-eb9fd8b802b7" width="743px" alt="Primary Color">
    <p>Secondary color schemes don't need to be colorful. They only need to contrast with surrounding elements and used sparingly for the UI</p>
</div>

+ Larger UI areas and elements should be colored with your `primary color`. A secondary color can be used to accent small areas.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/c1a8fd2b-4aa4-45e0-9bcd-f91ab80ccc76" width="743px" alt="Primary Color">
    <p>The floating action button is accented using the secondary color, while the phone icon uses the primary color.</p>
</div>

+ Text should be legible on the background on which it appears. It is recommend that.

    | Dark grey text are used in the light background       |
    | ------------------------------------------------------|
    | Light gray text are being used on the dark background |

+ There are rules for the dark, light text in a background related to the `opacity levels`.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/56610c13-ff83-4603-ad61-35a8c6e4dfdc" width="743px" alt="Dark Text on Light Background">
    <p>Dark text in light background opacity</p>
</div>

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/8c7b15e9-0d78-459f-84ce-1b7c7a959d59" width="743px" alt="Light Text on Dark Background">
    <p>Light text in dark background opacity</p>
</div>

+ Elements and other icons benefit having a hex value of black or white at `38%` opacity so they work on background of any color
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/4a0b68ae-edb3-4c83-a165-7f74f99d6468" width="743px" alt="Icon and other elements">
    <p>Icon and elements opacity opacity</p>
</div>

+ Product icon design is inspired by the tactile and the physical quality material. Each icon is cut, folded, and lit as paper would be, but represnted by simple graphic elements[^9].

    |Physical Prototype         | Lighting Study             | Material Prototype   | Color Study |
    |---------------------------|-------------------------   | -----------------    |-------------|
    | ![image](https://github.com/Xenoare/book-notes/assets/67181778/ee115682-ddd6-4e77-9f16-dc0a7034ca98) | ![image](https://github.com/Xenoare/book-notes/assets/67181778/5bc13c89-ee82-4624-b7d4-0b0f85ac2c9d)               | ![image](https://github.com/Xenoare/book-notes/assets/67181778/1a6ca986-5979-4624-9854-934642f7546c)               | ![image](https://github.com/Xenoare/book-notes/assets/67181778/ab00de0d-c755-44e9-850b-60e3a3060707)               |

+ Android expects product icon to be provided at `48dp`, with edges at `1dp`.
+ When you create the icon, maintain the `48-unit` measure, but scale up to`400%` at `192 x 192dp` (the edge becomes `4dp`).
    |1.1 Unit Grid | 4:1 Unit Grid |
    |--------------|---------------|
    | ![image](https://github.com/Xenoare/book-notes/assets/67181778/58ef9677-49f7-4a8d-900f-f06d6f22576e) | ![image](https://github.com/Xenoare/book-notes/assets/67181778/14bb4acb-93c7-431e-9887-90f4feaf2902)               |

+ Product icon anatomy describe the graphic element that makes up the product icon. It consist of several things such as
    + Finish
    + Material Background
    + Material Foreground
    + Color
    + Shadow

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/27eae0ab-1d1a-4ef2-b5df-997bd0679523" width="743px" alt="Construction Perspective">
    <p>An exploded perspective example illustrating the context of each component of the logo construction.</p>
</div>

+ When using illustration and photography to enhance the user experience, consider this following rule[^10].

    | Personal Reference | Imaginary can reflect the context and the world the user inhabits                              |
    | -------------------| -----------------------------------------------------------------------------------------------|
    | Information        | Images can convey specific information that makes comprehension easy and immediate             |
    | Delight            | Portraying context with aesthetic beauty will make the product unique and add the user delight |

+ Stay away from stock photos, strive for images that represent genuine stories[^11]
+ By default, `Roboto` is the standard typeface on Android. `Noto` is the standard alternative that is not covered by `Roboto`.
+ Google has categorized languages into three categories: `English` and `English-like`, `Tall`, and `Dense`[^12].

    | English & English-like | All latin (except Vietnamese), Greek, Cyrilic, Hebrew, Armenian and Georgian                     |
    | ---------------------- | -------------------------------------------------------------------------------------------------|
    | Tall                   | Language scripts that require extra line height to accommodate larger glyphs, including South and Southeast Asian and Middle Eastern languages, like Arabic, Hindi, Telugu, Thai, Vietnamese.                                     |
    | Dense                  | Language scripts that require extra line height to accommodate larger glyphs but have different metrics from tall scripts. Includes Chinese, Japanese, and Korean.                                                                      |

+ Text should be simple, concise and direct.
+ Use the `First` person perspective (`I / My`) to emphasize the user's ownership of some items or actions (`My Account`, `I agree on..`)[^13].
+ Use th `Second` person perspective (`You / Your`) to represent the conversitional style for most situation. (`Your Favorite`).
+ Avoid the usage of the pronoun `We`. Focus on the user and what they can do with your app. 
+ Write in the `Present Tense` to describe the product behaviour. When you need to write in the `past` or the `future`, use the simple verb forms.
+ Input focus should follow the order of the visual layout, from the `top` to the `bottom` of the screen. It should traverse from the most important to the least important item.
+ Determine the following focus points and movements:
    + The order in which elements receive focus.
    + The way in which elements are groupped.
    + Where the focus moves when the element focus disappears.

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/6766e60a-1f04-48cf-8c4d-c5a1a80657d0" width="743px" alt="Order of Focus">
    <p>The green circles indicate the order in which onscreen elements should receive focus.</p>
</div>

> Reference foot note:
> [^1]: https://m1.material.io/material-design/introduction.html#introduction-principles.
> [^2]: https://m1.material.io/material-design/environment.html#environment-3d-world
> [^3]: https://m1.material.io/material-design/elevation-shadows.html#elevation-shadows-elevation-android
> [^4]: https://m1.material.io/material-design/elevation-shadows.html
> [^5]: https://m1.material.io/motion/material-motion.html#material-motion-how-does-material-move
> [^6]: https://m1.material.io/motion/transforming-material.html#
> [^7]: https://m1.material.io/motion/transforming-material.html#
> [^8]: https://m1.material.io/style/color.html#color-color-system
> [^9]: https://m1.material.io/style/icons.html#icons-product-icons
> [^10]: https://m1.material.io/style/imagery.html#imagery-principles
> [^11]: https://m1.material.io/style/imagery.html#imagery-best-practices
> [^12]: https://m1.material.io/style/typography.html#typography-language-categories-reference
> [^13]: https://m1.material.io/style/writing.html#writing-language
