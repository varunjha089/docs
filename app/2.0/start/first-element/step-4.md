---
title: "Step 4: React to input"
subtitle: "Build your first Polymer element"
---

Of course, a button isn't a button if you can't click it.

With annotated event listeners, Polymer gives us an easy way to listen to events. See the [documentation on handling and firing events](/{{{polymer_version_dir}}}/docs/devguide/events) for more information. 

To toggle the button, all we need to do is write a method to toggle the `pressed` property when the button is pressed, and use an annotation to make sure that the method is called when the button is pressed. Polymer will take care of creating and removing the event listener, so you don't need to use `addEventListener`.

To make the button respond to a tap or click:

1. Place a method called `toggle` inside the class definition for `IconToggle`, after the constructor:
   
   icon-toggle.html { .caption }

   ```html
       toggle() {
         this.pressed = !this.pressed;
       }
   ```

2. Add `on-click="toggle"` to the opening tag of your `<iron-icon>` element: 
   
   ```html
   <iron-icon icon="[[toggleIcon]]" on-click="toggle"></iron-icon>
   ```

Your code should now look something like this:

icon-toggle.html { .caption }

```html
<script>
  class IconToggle extends Polymer.Element {
    static get is() {
      return "icon-toggle";
    }
    static get properties() {
      return {
        pressed: {
          type: Boolean,
          notify: true,
          reflectToAttribute: true,
          value: false
        },
        toggleIcon: {
          type: String
        }
      }
    }
    constructor() {
      super();
    }
    toggle() {
      this.pressed = !this.pressed;
    }
  }
    
  customElements.define(IconToggle.is, IconToggle);
</script>
```

Key information:

*   When you use an annotated event listener, Polymer creates and removes event listeners for you. 

*   You can still use the standard `addEventListener` method to add event listeners imperatively.

Save the `icon-toggle.html` file and look at the demo again. You should be able to press the button and see it
toggle between its pressed and unpressed states.

<img src="/images/2.0/first-element/databound-toggles.png" alt="Demo showing icon toggles with star and heart icons.">

**Learn more: data binding.** To see how the demo works, open `demo-element.html`
and take a look around (if you downloaded the code, you'll find this file in the `demo` folder.)
Yes, the demo for this element is _also_ an element. The
element uses <a href="/2.0/docs/devguide/data-binding#two-way-bindings">two-way
data binding</a> and a <a href="/2.0/docs/devguide/data-binding#annotated-computed">computed
binding</a> to change the string displayed when you toggle the button.
{ .alert .alert-info }

<a class="blue-button" href="step-3">
  Previous step: Use data binding and properties
</a>

<a class="blue-button" href="step-5">
  Next step: Theming with custom CSS properties
</a>
