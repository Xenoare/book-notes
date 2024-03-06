![image](https://github.com/Xenoare/book-notes/assets/67181778/8845577a-5ec5-4487-a6bb-18011837418c)# Dedicated Bangkit Notebook
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

### Material Design 2
+ `Material Studies` showcase the flexibility of `Material Theming` and components to create exprssive and unique apps.
+ The principles of the Material Studies are divided into dedicated pages[^14].

    | Expressive     | To highlight the capabilities, Material Theming has to offer, each Material study exprssed a different brand. |
    | ---------------|---------------------------------------------------------------------------------------------------------------|
    | Diverse        | To ensure that the Material Theming and component address as many product needs as possible.                  |
    | Reality-based  | To replicate real products as closely as possible. Each study is identifies user, display functional user flow and applies real-world restriction |

+ Material surface can behave in certain ways:

    | Rigid Surface      | Remain the same size through all interaction (one example is a card)                            |
    | -------------------|-------------------------------------------------------------------------------------------------|
    | Strechable Surface | Can grow and shrink along one or more edges up to size limit, then behave as rigid surface.     |
    | Pannable Surface   | remain the same size throughout interactions. They can display additional content upon scrolling within the area, until reaching a content limit. When this limit is reached, they behave as rigid surfaces in that scroll direction. (One obvious example is (maps on android) |

+ Elevation in Material Design is measured as the distance between Material Surfaces along the `z`-axis in `density-independent pixels` (dps) and depicted using `shadows`.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/f1165aa9-768b-4e1b-b73a-ed0f655844aa" width="743px" alt="Measuring Elevation">
    <p>One surface at 1dp elevation and 8dp elevation as viewed from front and side.</p>
</div>

+ Light sources and shadows are cast by a `key light` and `ambient light`. In Android or iOS, shadows occour when light sources are blocked by material surfaces along the `z`-axis

    | Shadow cast by Key Light (Don't 🚫) | Shadow cast by Ambient Light (Don't 🚫) | Combined Both       | 
    |-------------------------------------|------------------------------------------|---------------------|
    | ![image](https://github.com/Xenoare/book-notes/assets/67181778/f2616df8-c8dc-4647-a0b9-fd740d67e484) | ![image](https://github.com/Xenoare/book-notes/assets/67181778/ea46aec2-fa29-4c8e-8b3b-ee40f63b99a5)               |  ![image](https://github.com/Xenoare/book-notes/assets/67181778/b5936fef-64ed-41de-9cae-5c5623ea8bed)               | 

+ Density Independent Pixel `dp` or called (`DIPS`) are flexible unit that scale to have uniform dimension on any screen.
+ A `is` equal to one physical pixel on a screen with the density of 160[^15].
$$dp = \frac{\text{width in pixel} * 160}{\text{screen density}}$$

    | Screen physical width | Screen density | Screen width in pixels | Screen width in dps |
    |-----------------------|----------------|------------------------|---------------------|
    | 1.5 in 1.5 in 1.5 in  | 120 160 240    | 180 px 240 px 360 px   | 240 dp              |

+ The responsive layout grid is made out of three elements: `columns`, `gutters`, and `margins`[^16].
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/6ac07c23-dc36-4097-8d5d-6c4d39067bc8" width="743px" alt="Responsive layout">
    <p>1. Columns, 2. Gutters, 3. Margins</p>
</div>

+ Content is placed in the area of the screen that contains columns.
+ In the context of `responsive layout`, column `width` is defined with percentages, rather than fixed values.
+ The number of columns can be represent by the breakpoint range that correspond with mobile, table or other screen.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/e3accf2b-c69e-43ef-b89b-1f50375bf01a" width="743px" alt="Breakpoint of mobile">
    <p>On mobile with breakpoint of 360dp, this layout use 4 columns</p>
</div>

+ `Gutters`, in other hand are the space between the columns that seperate the content.
+ It should also increase in order for the larger screen.
+ Don't make gutters that's too `large` or have the `same` width as the columns.
+ `Margins` are the space between the content left and right.

+ Material Design provides responsive layout based on `4-columns`, `8-columns`, and `12-columns` grid.

    | Screen size         | Margin  | Body    | Layout columns |
    |---------------------|---------|---------|----------------|
    | Extra-small (phone) |         |         |                |
    | 0-599dp             | 16dp    | Scaling | 4              |
    | Small (tablet)      |         |         |                |
    | 600-904             | 32dp    | Scaling | 8              |
    | 905-1239            | Scaling | 840dp   | 12             |
    | Medium (laptop)     |         |         |                |
    | 1240-1439           | 200dp   | Scaling | 12             |
    | Large (desktop)     |         |         |                |
    | 1440+               | Scaling | 1040    | 12             |

+ A container is to hold the UI elements such as images, icon, or surfaces.
+ An aspect ratio is the proportion element's width to its height (correspond to `width:height`)
+ The following aspect ratios are recommended for use across your UI: `16:9; 3:2; 4:3; 1:1; 3:4; 2:3`
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/a187f4c1-83e1-45f3-884c-f0a6689f7a34" width="743px" alt="Aspect Ratio">
    <p>Common aspect ratio</p>
</div>

+ Lastly, `Touch Targets` apply to any device that receives both touch input and non-touch input.
+ To balance the `usability` and `density`. Touch targets should be at leaast `48`x`48` dp
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/cc5d5fe8-7d9c-49a1-aed6-74658ba5011c" width="743px" alt="Touch target minimum">
    <p>Touch target minimum of 48x48dp</p>
</div>

+ One thing to be noted is that how Component adaption describe the changes in `visual presentation` (padding, size, layout, or alignment) out of one component to better suited with the `device size` and the `use case`[^17].
+  Here's some functionally-equivalent component group are defined below.

    | Component type | Mobile option           | Tablet option           | Laptop option               |
    |----------------|-------------------------|-------------------------|-----------------------------|
    | Navigation     | Bottom navigation       | Navigation rail         | Navigation drawer           |
    | Navigation     | Modal navigation drawer | Modal navigation drawer | Permanent navigation drawer |
    | Communication  | Full-screen dialog      | Simple dialog           | Simple dialog               |
    | Action         | Bottom sheet            | Menu                    | Menu                        |

+ Navigation is act to moving between screen of an app to complete task.
+ Based on your app information architecture, an `user` can move in `one` of `three` navigation directions[^18].

    | Lateral Navigation | Moving between screen that are the same level of hierarchy. This can be done usually by the Primary Navigation Component to give access to all destination                            |
    | -------------------|-------------------------------------------------------------------------------------------------|
    | Forward Navigation | Refers to moving in the consecutive level of hierarychy, steps in a flow, or accross the app. Forward navigation behaviour into container (such as card, lists, images), buttons, or by search |
    | Reverse Navigation | Refers to moving backwards through screens, either chronologically (within one app or across an app) or hierarchically (wihin an app) |

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/1194bd29-69c9-4def-9070-9e73b9e2e591" width="743px" alt="Example of Lateral Navigation">
    <p>Lateral navigation allows up to move at the top-level screens of this songs's app</p>
</div>

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/f93d03f7-f2ee-486a-aeff-306a54f14f7b" width="743px" alt="Forward Navigation of accessing songs">
    <p>User of this music app can use Forward Navigation to access songs by 2 ways. Either directly from the searching a songs, or from the albums menu</p>
</div>

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/0bfa90de-4f9e-445f-b93f-7c686c0aaeb9" width="743px" alt="Reverse Navigation within Music app">
    <p>From the screen songs, user can reverse navigate in two ways, of either back to search or back to albums.</p>
</div>

+ So normally, the `Lateral Navigation` are being used for the Primary Drawer such as Menu, Navigation bar and more to give and access to navigate to other screens[^19].

    | Component             | Use for                | # destinations | Devices                 |
    |-----------------------|------------------------|----------------|-------------------------|
    | Navigation drawer     | Top-level destinations | 5+             | Mobile, Tablet, Desktop |
    | Bottom navigation bar | Top-level destinations | 3-5            | Mobile                  |
    | Tabs                  | Any level of hierarchy | 2+             | Mobile, Tablet, Desktop |

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/14363975-dbd6-4da8-90fd-00ecdcb16a6f" width="743px" alt="Bottom Navigation Bar Example as Primary Navigation">
    <p>Bottom navigation bars provide access to 3-5 top-level destinations on mobile devices. Their location, visibility, and persistence across screens allow quick pivoting between destinations. </p>
</div>

+ The `Forward Navigation` refers to one of three types of movement between screen when accomplish a task. It usually are in these forms:

    | Downward       | Form of Navigation that navigate from the parent screens (Higher level) to deeper (child screen)           |
    | ---------------|------------------------------------------------------------------------------------------------------------|
    | Sequential     | In a form of steps / flow on a ordered sequence of process, such as checkout process.                      |
    | Directly       | from one screen to any other in the app, such as from a home screen to a screen deep in an app's hierarchy |

+ Forward Navigation can be implemented by such example like by `content containers`, such as lists / image. Also it can be implemented by `Button` that can advance to another screens, and in-app search on one or more screens.
+ The `Reverse Navigation` are usually implemented by `Back Button` to navigate in reverse
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/a7046d72-2b66-4867-8ba4-4696805e2ab1" width="743px" alt="Reverse Navigation">
    <p>The Back button allows users to navigate recently viewed screens in reverse chronological order. </p>
</div>

+ Search is allows user to quickly access content accross the app.
+ Use persistent search when search is the primary focus of your app. The search text field is presented inside of a search bar, ready to receive focus. Optionally you can put the historical search suggestion
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/161bdcf7-0702-4e5b-9613-c5dcea9f3d37" width="743px" alt="Persistant Search">
    <p>Persistent search field receiving focus, loading results, and returning to an unfocused state.</p>
</div>

+ Use expandable search when search is not the primary focus of your app. Expandable search displays a search icon in the toolbar, instead of an open search text box.

<div align="center">
    <video width="630" src="https://github.com/Xenoare/book-notes/assets/67181778/0a91cc93-a0fb-4bc3-859f-a3abb6e5e4eb"></video>
</div>

+ One tool is to set up the colors and theming are [Material Design Pallete Pool](https://m2.material.io/design/color/the-color-system.html#color-theme-creation)
+ The principles of the Color System are:

    | Hierarchical   | Color indicates which elements are interactive, how they relate to other elements, and their level of prominence. Important elements should stand out the most.           |
    | ---------------|------------------------------------------------------------------------------------------------------------------|
    | Legible        | Text and important elements, like icons, should meet legibility standards when appearing on colored backgrounds. |
    | Expressive     | Show brand colors at memorable moments that reinforce your brand’s style.                                        |

+ Material design comes with a built in baseline themes that can be used as-is. Normally the includes this includes default colors for[^20].
    + Primary and secondary colors
    + Variants of primary and secondary colors
    + Additional UI colors, such as colors for backgrounds, surfaces, errors, typography, and iconography.

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/895aef6d-3d1e-401e-a19c-22c1a6694863" width="743px" alt="Color Creation">
    <p>The baseline Material color theme.</p>
</div>

+ Your primary color can be used to make the `light` or `dark` variant of the primary color.
+ To create the contrast between `UI` elements, such as from the top app bar to the system bar, you can use the `light` or `dark` variants of your primary color.
<div align="center">
    <video width="630" src="https://github.com/Xenoare/book-notes/assets/67181778/d71b580a-3a66-45ea-bf09-6929baca09e4"></video>
</div>

+ A secondary color provides more ways to accent and distinguish your product. Having a secondary color is optional, and should be applied sparingly to accent select parts of your UI.
+ Surface, background, and error colors typically don’t represent brand:
    + `Surface` colors affect surfaces of components, such as cards, sheets, and menus.
    + The `background color` appears behind scrollable content. The baseline background and surface color is #FFFFFF.
    + `Error color` indicates errors in components, such as invalid text in a text field. The baseline error color is #B00020.

<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/b6ff53a0-e6ef-419b-abc5-2f9fa6ba9a64" width="743px" alt="Surface Color">
    <p>A UI showcasing the baseline colors for background, surface, and error color:</p>
</div>

+ The principles when applying the Color to the UI are[^21].

    | Consistent     | The color should be used consistenly and be compitable with the brand it represents.                          | 
    | ---------------|---------------------------------------------------------------------------------------------------------------|
    | Distinct       | Color should bring some distinct to the elements, within sufficient contrast between them.                    |
    | Intentional    | Color should be applied purposefully as it can convey meaning in multiple ways, such as relationships between elements and degrees of hierarchy.                                                                                                    |

+ For the `identifying` the app bar. The top and bottom bar should be use with app's primary color. System bar can be use a `dark` / `light` variant to distinguish between them.
+ To emphesize the difference between app bar and other surface components, use the `secondary color` just like the case of `floating app button (FAB)`
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/7e6624de-4907-49e0-9ddb-e0f9d30d6a9e" width="743px" alt="The usage of Primary and Secondary Color">
    <p>The primary color (blue 700) is being used for the app bar, and the secondary color (orange 500) being used for FAB</p>
</div>

+ The baseline colors for sheets and surfaces, such as bottom sheets, navigation drawers, menus, dialogs and cards are `white`[^22].
+ Use contrasting colors on the surfaces that appear on the screen temporarily, such as `navigation drawer` / `dialog button`.
+ Usually this surfaces are white, but you can use your app's primary or secondary color.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/9b3654b1-7b08-4286-be1c-98a85b959700" width="743px" alt="Example of using constrasting color">
    <p>This app uses its primary color blue (blue 700) on the bottom navigation drawer, a primary dark variant (blue 800) for the account switcher, and a secondary color (orange 500) for selection. </p>
</div>

+ Buttons, chips and selection controls can be emphasized by applying your primary or secondary color to them.
    + The baseline color for contained, text and outlined buttons is your primary color.
    + The baseline color for floating action buttons and extended floating action buttons is your secondary color.
    + The baseline color for selection controls is your secondary color.
      
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/f5be9acf-cae6-48a2-91a8-d4df8f4b99af" width="743px" alt="Button, chip, selection control colors">
    <p>This app using primary color (purple 500) and its dark variant (purple 600) for the app bar with secondary color (teal 200) to be his floating-action-button color andselection control color</p>
</div>

+ Instead of using `grey text`, it's better to create better contrast by displaying white or black text with reduced opacity.
+ For example, black text displayed at `75%` opacity on a green background gives the text an appearance of black, with a hint of green.
<div style="display: block; margin: auto; text-align: center;" align="center">
    <img src="https://github.com/Xenoare/book-notes/assets/67181778/54fd7348-c92d-4f12-8e6c-7eca6aec9fa9" width="743px" alt="Using text opacity">
    <p>Use a transparent version of black on a colored surface to preserve legibility.</p>
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
> [^14]: https://m2.material.io/design/material-studies/about-our-material-studies.html#about-material-studies
> [^15]: https://m2.material.io/design/layout/pixel-density.html#pixel-density-on-android
> [^16]: https://m2.material.io/design/layout/responsive-layout-grid.html#columns-gutters-and-margins
> [^17]: https://m2.material.io/design/layout/component-behavior.html#component-adaptation
> [^18]: https://m2.material.io/design/navigation/understanding-navigation.html#types-of-navigation
> [^19]: https://m2.material.io/design/navigation/understanding-navigation.html#lateral-navigation
> [^20]: https://m2.material.io/design/color/the-color-system.html#color-theme-creation
> [^21]: https://m2.material.io/design/color/applying-color-to-ui.html#top-and-bottom-app-bars
> [^22]: https://m2.material.io/design/color/applying-color-to-ui.html#sheets-and-surfaces
