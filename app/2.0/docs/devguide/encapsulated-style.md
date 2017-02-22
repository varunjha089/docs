---
title: Encapsulated style with Polymer 2.0 and shadow DOM v1
---

<!-- toc -->

Polymer supports DOM templating and the shadow DOM API. When you use the <dom-module> and <template> blocks to template your custom element, Polymer attaches a shadow root to instances of this element. Polymer then copies in the contents of the template you provided for your element.

```html
<dom-module id="my-element">
	<template>
		<h1>Heading!</h1>
		<p>We will be elements in local DOM.</p>
	</template>
</dom-module>
...
<script>
	class MyElement extends Polymer.Element {
		static get is(){
			return 'my-element'
		}
	}
	customElements.define(MyElement.is, MyElement)
</script>

The HTML elements in your template become children within your custom element's shadow DOM. Shadow DOM provides a mechanism for encapsulation, meaning that elements in side the shadow DOM are not accessible to styling rules external to the shadow DOM. 

Likewise, styling rules in side the shadow DOM can't "leak" out to affect elements outside the shadow DOM.

Shadow DOM permits encapsulation of styling rules for custom elements. You can freely define styling information for your elements, such as fonts, text colors, and classes, without fear of the styles applying outside the scope of your element.

```html
<style>
	.myclass {
		color:blue;
	}
</style>
<dom-module id="x-foo">
<template>
	<style>
		p {
			color:green;
		}
		.myclass {
			color:red;
		}
	</style>
	<p>I'm a shadow DOM child element of x-foo.</p>
</template>
</dom-module>
<script>
	class XFoo extends Polymer.Element {
		static get is(){
			return 'x-foo'
		}
	}
	customElements.define(XFoo.is, XFoo)
</script>
<p class="myclass">I have nothing to do with x-foo. Because of encapsulation, x-foo's styles won't leak to me.</p>

For a detailed explanation of shadowDOM as it applies to Polymer, see [arthur's article]().

For an exploration of the shadow DOM v1 API, see [Shadow DOM v1: Self-Contained Web Components](https://developers.google.com/web/fundamentals/getting-started/primers/shadowdom).

When used in an HTML document, your element will still inherit any styling information that applies to its parent element:

```html
<head>
	<style>
	p {
		font-family: sans-serif;
		color:blue;
	}
	</style>
</head>
</body>
	<dom-module id="x-foo">
		<template>
			<div>I inherit styles from x-foo's parent in the light DOM. I'm also sans-serif and blue.</div>
		</template>
	</dom-module>
	<script>
	class XFoo extends Polymer.Element {
		static get is(){
			return 'x-foo'
		}
	}
	customElements.define(XFoo.is, XFoo)
	</script>
	<p>I'm sans-serif and blue.</p>
	<p><x-foo></x-foo></p>
</body>
```

Styles declared in side shadow DOM will override styles declared outside of it:

```html
<style>
	p { 
		font-family: sans-serif;
		color:blue;
    }
</style>
</head>
<body>
	<dom-module id="x-foo">
	<template>
		<style>
		p {
			font-family: sans-serif;
			color:green;
		}
		</style>
		<p>I'm green.</p>
	</template>
	</dom-module>
	<p>I'm blue.</p>
	<p><x-foo></x-foo></p>    
	</body>
	<script>
	class XFoo extends Polymer.Element {
		static get is(){
			return 'x-foo'
		}
	}
	customElements.define(XFoo.is, XFoo)
	</script>
</body>
```

# Style the host element

The element to which shadow DOM is attached is known as the host. To style the host, use the `:host` selector.

Inheritable properties of the host element will inherit down the shadow tree, where they apply to the shadow children.

```html
<dom-module id="x-foo">
	<template>
		<style>
		:host {
			font-family: sans-serif;
			color:green;
			display: block;
			border: 1px solid;
		}	
	</style>
	<p>I'm green.</p>
	<div>I'm green too.</div>
	<span>We're all green...</span>
	</template>
</dom-module>
<x-foo></x-foo>    
```

You can also style the host element from outside - for example, using a type selector:

```html
x-foo {
	background-color:blue;
}
```

You can use CSS selectors to determine when and how to style the host:

```html
<dom-module id="x-foo">
	<template>
		<style>
			:host { font-family: sans-serif; }
			:host(.blue) {color: blue;}
			:host(.red) {color: red;}
			:host(:hover) {color: green;}
		</style>
		<p>Hi, from x-foo!</p>
	</template>
</dom-module>
<x-foo class="blue"></x-foo>
<x-foo class="red"></x-foo>
<x-foo></x-foo>
```

Descendant selectors after `:host` match elements in the shadow tree. In this example, the CSS selector applies to any `p` element in the shadow tree if the host has class "warning":

```html
<dom-module id="x-foo">
	<template>
		<style>
		:host(.warning) p {
			color:red;
		}
		</style>
		<p>Hi, from x-foo!</p>
		<div>:D</div>
	</template>
</dom-module>
<x-foo class="warning"></x-foo>
```

Styling with the `:host` selector is one of two instances where rules inside a shadow tree can affect an element outside a shadow tree. The second instance uses the ::slotted() syntax to apply styling rules to content populated from the main DOM at runtime.

# Style slotted content

You can create slots in an element's template that are populated at runtime using this syntax:

```html
<dom-module id="x-foo">
    <template>
        <h1>
            <slot name='heading1'></slot>
        </h1>
        <p>
            <slot name='para'></slot>
        </p>
    </template>
</dom-module>

<x-foo>
    <div slot="heading1">Heading 1</div>
    <div slot="para">Paragraph text</div>
</x-foo>
```

To style slotted content, use the ::slotted() syntax.
::slotted(*) selects all slotted content:

```html
<dom-module id="x-foo">
    <template>
      <style>
        ::slotted(*) {
          font-family: sans-serif;
          color:green;
        }
      </style>
        <h1>
            <div><slot name='heading1'></slot></div>
        </h1>
        <p>
            <slot name='para'></slot>
        </p>
    </template>
</dom-module>
<x-foo>
    <div slot="heading1">Heading 1. I'm green.</div>
    <div slot="para">Paragraph text. I'm green too.</div>
</x-foo>   
```

You can select by element type:

```
<dom-module id="x-foo">
	<template>
		<style>
		::slotted(h1) {
			font-family: sans-serif;
			color:green;
		}
		::slotted(p) { 
			font-family: sans-serif;
          color:blue;
      }
      </style>    
            <slot name='heading1'></slot>
            <slot name='para'></slot>
    </template>
</dom-module>
<x-foo>
    <h1 slot="heading1">Heading 1. I'm green.</h1>
    <p slot="para">Paragraph text. I'm blue.</p>
</x-foo>
```


  You can select by class:
<dom-module id="x-foo">
    <template>
      <style>
        ::slotted(.green) {
          color:green;
        }
      </style>
        <p>
            <slot name='para1'></slot>
        </p>
        <p>
            <slot name='para2'></slot>
        </p>
    </template>
</dom-module>

<x-foo>
    <div slot="para1" class="green">I'm green!</div>
    <div slot="para1">I'm not green.</div>
    <div slot="para2" class="green">I'm green too.</div>
    <div slot="para2">I'm not green.</div>
</x-foo> 
And you can select by slot name:
<dom-module id="x-foo">
    <template>
      <style>
        slot[name='para1']::slotted(*) {
          color:green;
        }
      </style>
        <p>
            <slot name='para1'></slot>
        </p>
        <p>
            <slot name='para2'></slot>
        </p>
    </template>
</dom-module>

<x-foo>
    <div slot="para1">I'm green!</div>
    <div slot="para2">I'm not green.</div>
</x-foo> 
For more examples, see Rob Dodson's Shadow DOM CSS Cheat Sheet.