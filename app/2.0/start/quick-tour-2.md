---
title: Try Polymer
---

<!-- toc -->

Polymer makes it simple to create web components, declaratively.

New web developers can simply add custom HTML elements on a web page with markdown. It’s just like using the HTML tags you’re already familiar with:

```
<h1>A heading!</h1>
```

```
<fancy-thing>A fancy thing!</fancy-thing>
```

Experienced web developers can use Polymer's special features to reduce setup code
and make it even easier to build complex, interactive elements. In this tour, you'll learn how to:

- Register elements
- Use lifecycle callbacks
- Observe properties
- Create shadow DOM with templates
- Use data binding

In this section you can play with features of the Polymer library,
without installing anything. Click on a code sample to edit it, and see the results instantly.

Tap the buttons following each feature to learn more.

### Drop a custom element on your page

An **HTML element** is a component of a web page, represented as a tag. **Custom elements** are new HTML components, represented by new tags. You can make your own, or use ones that other developers have already made. Chances are, if you need to do something on your web page, there’s an element for that! 

For example, you can include <a href="https://www.webcomponents.org/element/PolymerElements/paper-button" >`<paper-button>`</a> on your page like this:

<live-demo-tabs selected="0" height="60" src="http://localhost:3000">
  <live-demo-tab tab-name="index.html">
    <div slot="heading">
      index.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/drop-element/index.html')}}}</template>
  </live-demo-tab>
</live-demo-tabs>


Try it out! 

* Edit the text inside any of these buttons to see changes.
* Change the class of any button to see easy-to-use color schemes.


### Register an element {#register}

To register a new element, create an ES6, or JavaScript, class that extends
`Polymer.Element`, then call the `customElements.define` method, which
_registers_ a new element with the browser. Registering an element associates
an element name with a class, so you can add properties and methods to your custom
element. The custom element's name **must start with an ASCII letter and
contain a dash (-)**.

<live-demo-tabs selected="0" height="40" src="http://localhost:3000">
  <live-demo-tab tab-name="custom-element.html">
    <div slot="heading">
      custom-element.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/custom-element/custom-element.html')}}}</template>
  </live-demo-tab>
  <live-demo-tab tab-name="index.html">
    <div slot="heading">
      index.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/custom-element/index.html')}}}</template>
  </live-demo-tab>
</live-demo-tabs>


Try it out!

* Try modifying the contents of `this.textContent`. 
* If you’re familiar with your browser’s developer tools, try printing the
  custom element’s `tagName` property to the console. 
  Hint: add `console.log(this.tagName);` to the constructor method!


This sample uses a lifecycle callback
to add contents to the `<custom-element>` when it's initialized.
When a custom element finishes its initialization, the `ready` lifecycle callback is called.
You can use the `ready` callback for one-time initialization work after the element is created.

<p><a href="/{{{polymer_version_dir}}}/docs/devguide/registering-elements" class="blue-button">
  Learn more: element registration
</a></p>

<p><a href="/{{{polymer_version_dir}}}/docs/devguide/registering-elements#lifecycle-callbacks" class="blue-button">
  Learn more: lifecycle callbacks
</a></p>

### Add shadow DOM

Many elements include some internal DOM nodes to implement the element's UI and behavior.
You can use Polymer's DOM templating to create a shadow DOM tree for your element.

<live-demo-tabs selected="0"  height="40" src="http://localhost:3000">
  <live-demo-tab tab-name="dom-element.html">
    <div slot="heading">
      dom-element.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/dom-element/dom-element.html')}}}</template>
  </live-demo-tab>
  <live-demo-tab tab-name="index.html">
    <div slot="heading">
      index.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/dom-element/index.html')}}}</template>
  </live-demo-tab>
</live-demo-tabs>


Try it out!

* Try adding some other html elements inside the <template></template> block. For example, add `<h1>A heading!</h1>` or `<a href=”stuff.html”>A link!</a>`

Shadow DOM is encapsulated inside the element.

<p><a href="/{{{polymer_version_dir}}}/docs/devguide/dom-template" class="blue-button">Learn more: DOM templating</a></p>

### Compose with shadow DOM

Shadow DOM lets you control _composition_. The element's children can be _distributed_
so they render as if they were inserted into the shadow DOM tree.

This example creates a simple tag that decorates an image by wrapping it
with a styled `<div>` tag.

<live-demo-tabs selected="0" height="60" src="http://localhost:3000">
  <live-demo-tab tab-name="picture-frame.html">
    <div slot="heading">
      picture-frame.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/picture-frame/picture-frame.html')}}}</template>
  </live-demo-tab>
  <live-demo-tab tab-name="index.html">
    <div slot="heading">
      index.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/picture-frame/index.html')}}}</template>
  </live-demo-tab>
</live-demo-tabs>


Try it out!

* Try adding divs in index.html to observe how they are unaffected by the styles applied to the divs in picture-frame’s shadow DOM.
* Try adding other HTML elements to the DOM template to see how they are positioned relative to the distributed child nodes.


**Note:** The CSS styles defined inside the `<dom-module>` are _scoped_ to the element's shadow DOM.
So the `div` rule here only affects `<div>` tags inside `<picture-frame>`.
{: .alert .alert-info }

<p><a href="/2.0/docs/devguide/shadow-dom#shadow-dom-and-composition" class="blue-button">
Learn more: Composition & distribution</a></p>

### Use data binding

Of course, it's not enough to have static shadow DOM. You usually want to have your element update
its shadow DOM dynamically.

Data binding is a great way to quickly propagate changes in your element and reduce boilerplate code.
You can bind properties in your component using the "double-mustache" syntax (`{%raw%}{{}}{%endraw%}`).
The `{%raw%}{{}}{%endraw%}` is replaced by the value of the property referenced between the brackets.

<live-demo-tabs selected="0" height="40" src="http://localhost:3000">
  <live-demo-tab tab-name="name-tag.html">
    <div slot="heading">
      name-tag.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/name-tag/name-tag.html')}}}</template>
  </live-demo-tab>
  <live-demo-tab tab-name="index.html">
    <div slot="heading">
      index.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/name-tag/index.html')}}}</template>
  </live-demo-tab>
</live-demo-tabs>

Try it out!

* Try editing the value of the `owner` property.
* Try adding another property and binding it in your component. 
  Hint: Add `this.propertyName = "Property contents";` to the constructor
  and add {{propertyName}} to the element’s shadow DOM.  

<p><a href="/2.0/docs/devguide/data-binding" class="blue-button">
Learn more: data binding</a></p>

### Declare a property

Properties are an important part of an element's public API. Polymer
_declared properties_ support a number of common patterns for properties—setting default
values, configuring properties from markup, observing property changes, and more.

The following example declares the `owner` property from the last example.
It also shows configuring the owner property from markup in `index.html`.

<live-demo-tabs selected="0" height="40" src="http://localhost:3000">
  <live-demo-tab tab-name="configurable-name-tag.html">
    <div slot="heading">
      configurable-name-tag.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/configurable-name-tag/configurable-name-tag.html')}}}</template>
  </live-demo-tab>
  <live-demo-tab tab-name="index.html">
    <div slot="heading">
      index.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/configurable-name-tag/index.html')}}}</template>
  </live-demo-tab>
</live-demo-tabs>

Try it out!

* Try editing the initial value of `owner` in index.html. Observe how this sets the property directly from your HTML.

<p><a href="/2.0/docs/devguide/properties" class="blue-button">
Learn more: declared properties</a></p>

### Bind to a property

In addition to text content, you can bind to an element's _properties_ (using
`property-name="[[binding]]"`). Polymer properties
can optionally support two-way binding, using curly braces (`property-name="{{binding}}"`).

This example uses two-way binding: binding the value of a custom input element (`iron-input`)
to the element's `owner` property, so it's updated as the user types.

<live-demo-tabs selected="0" height="100" src="http://localhost:3000">
  <live-demo-tab tab-name="editable-name-tag.html">
    <div slot="heading">
      editable-name-tag.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/editable-name-tag/editable-name-tag.html')}}}</template>
  </live-demo-tab>
  <live-demo-tab tab-name="index.html">
    <div slot="heading">
      index.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/editable-name-tag/index.html')}}}</template>
  </live-demo-tab>
</live-demo-tabs>

Try it out!

* Edit the placeholder text to see two-way data binding at work. (Note: You will only see the placeholder text if the `input` element is empty.)

**Note:** The `<iron-input>` element wraps a native `<input>` element and provides two-way
data binding and input validation.
{: .alert .alert-info }

### Using `<dom-repeat>` for template repeating

The template repeater (`dom-repeat`) is a specialized template that binds to an array. It creates one instance of the template's contents for each item in the array.

<live-demo-tabs selected="0" src="http://localhost:3000">
  <live-demo-tab tab-name="employee-list.html">
    <div slot="heading">
      employee-list.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/employee-list/employee-list.html')}}}</template>
  </live-demo-tab>
  <live-demo-tab tab-name="index.html">
    <div slot="heading">
      index.html
    </div>
    <template slot="html-content">{{{include_file_raw('2.0/start/samples/employee-list/index.html')}}}</template>
  </live-demo-tab>
</live-demo-tabs>

Try it out!

* Change the first and last names inside this.employees
* Add another employee by inserting this text into the array definition after employee Tony Morelli ({%raw%}{first: 'Tony', last: 'Morelli'}{%endraw%}):<br>
  `,`<br>
  `{%raw%}{first: 'Shawna', last: 'Williams'} {%endraw%}`

<p><a href="/2.0/docs/devguide/templates" class="blue-button">
Learn more: Template repeater</a></p>

## Next steps

Now that you understand these fundamental Polymer concepts, you can [build an app with App Toolbox](/2.0/start/toolbox/set-up) or see a [feature overview of the Polymer library](/2.0/docs/devguide/feature-overview).

## Help us out!
We appreciate you reviewing this page for us. Please take a moment to fill out <a href="https://goo.gl/forms/dFVMgjwYWEMtTVN52" target="_blank">this form</a>. 