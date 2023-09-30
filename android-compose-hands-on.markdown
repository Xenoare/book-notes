## Thinking in Compose

### Declarative Programming Paradigm
With Views, the way to updating the UI is to walk the tree of UI widgets such as defining UI in XML, finding views from XML in code, and then calling the setter function (such as using function `findViewById()` and changes nodes by calling methods such as `button.setText(String)` to get UI like you want. 

Manipulating views manually can increase the likelihood of errors, such as if a pice of data is rendered in multiple places. In general, the software maintenance complexity grows with the number of views that require updating.

### Simple composable funtion
