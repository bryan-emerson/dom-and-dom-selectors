[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# The DOM & JavaScript

In the Objects & Context lesson, you learned about objects as data structures
and how we can use them to store data and methods. Today, we will learn about
how JavaScript uses objects to represent what you see in the browser. Remember,
everything is an object!

## Prerequisites

- JavaScript
- HTML & CSS

## Objectives

By the end of this, developers should be able to:

- Explain what the DOM is and how it is structured
- Target DOM elements using JavaScript selectors
- Create, read, update, and delete DOM elements
- Change the attributes or content of a DOM element
- Explore JavaScript methods for DOM manipulation and traversal

## Introduction

The
[Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction),
commonly referred to as the "DOM", is a programming interface for HTML. When you
load HTML into the browser, it gets converted into a dynamic object-based
structure. The [visual representation](https://css-tricks.com/dom/) of this is
what you see when you open up Developer Tools in the browser.

The DOM is available for us to manipulate as an object, and this object is
structured and stored like an upside down tree, like this:

![lxf118 tut_grease diagram](https://git.generalassemb.ly/storage/user/6376/files/1035f642-6263-11e7-9a38-4db66c999724)

Or this:

```
html
└── head
│   ├──title
│   ├──meta
│   ├──link[rel="stylesheet"]
|   └──script[type="text/javascript"]
|
└── body
    ├── header
    │   ├── h1
    │   └── nav
    └── section.simplicity
    |   └── h2
    │   └── article
    ├── section.life
    |   └── h2
    │   └── article
    │       └── block_quote
    │       └── block_quote
    └── footer
```

## The Document Object

Each web page loaded in the browser has its own `document` object. The
`document` interface serves as an entry point to the web page's content. The
document is an example of a **host object**--that is, a JavaScript object
provided by and unique to the browser environment.

### Nodes

Everything in the DOM exists as a **node**. HTML elements are called **element
nodes**, attributes are called **attribute nodes**, the text inside elements are
called **text nodes**. There are even comment nodes for
`<!-- html comments like this one --->`.

The document itself is called a document node.

You also can refer to nodes by their relationships to each other. For example,
in the graphic above, you would say that the body element is the "parent" to the
two `div` elements contained inside it, which are called child nodes. The two
divs are also "siblings" to one another because they are on the same level in
the tree structure.


## Basics of Working with the DOM

Understanding the DOM is central to working in JavaScript. JavaScript uses the
DOM to create dynamic HTML. This includes adding new HTML elements and
attributes, changing CSS styles in a page, removing existing elements and
attributes, and [many more things](https://www.w3.org/TR/DOM-Level-2-Core/introduction.html).

Most of what you do with client-side JavaScript is going to revolve around
manipulating the DOM.

## Getting Data from the DOM

There are two groups of methods you can use to get elements from the DOM. We'll
start with the oldest and end with the ones we recommend.

### `getElement(s)By`

Each of these methods follows the same general naming convention:

| Method Name                 | Description                                           |
| --------------------------- | ----------------------------------------------------- |
| `.getElementById()`         | Gets a single element by an ID selector               |
| `.getElementsByClassName()` | Gets a list of elements with a class selector         |
| `.getElementsByTagName()`   | Gets a list of elements with a tag (element) selector |

Each of these three methods are part of the `document` object. We'll walk
through each individually:

**`getElementById()`**

To use the `getElementById` method, we first need to reference the `document`
object (where the method lives). Then, we pass in a string that matches the ID
of an element in our HTML

```js
let titleElement = document.getElementById("title");
```

The above code will start at the document (top of the tree), and look for an
element with an id called `title` and save it in the variable `titleElement`

**`getElementsByClassName`**

The `getElementById` method returns a single Node item; the
`getElementsByClassName` returns a NodeList, which is like an Array of Nodes.

```js
let paragraphElements = document.getElementsByClassName("paragraph");
```

The above code snippet returns a NodeList (like an Array) of every element with
a class of 'paragraph' and saves it to the `paragraphElements` variable. Notice
that `Elements` in the method name is plural here, where as in `getElementById`
it's singular? This is to tell us that `getElementByID` only returns one Node
while `getElementsByClassName` returns a list of Nodes.

**`getElementsByTagName`**

The `getElementsByTagName` is a hand way of retrieving elements by their html
tag (`h1`, `span`, `a`, `li`, etc). `Elements` is plural in the method name,
meaning it too returns a list of Nodes.

```js
let spanElements = document.getElementsByTagName("span");
```

The above snippet returns every `span` element on the page and saves it to the
`spanElements` variable.

#### I Do: [JS DOM Practice Part 1](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and watch as I demonstrate using the
`getElement(s)` methods.

#### You Do: [JS DOM Practice Part 1](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and work through the prompts in the
`getelements.js` file.

### `querySelector` 

There are only two methods in this group: `querySelector` and
`querySelectorAll`. Unlike the `getElement(s)By` group, these are simpler to
understand - querySelector returns a single value, and querySelectorAll
returns...well...everything that it can find. You can even select multiple IDs
this way.

We'll walk through both `querySelector` and `querySelectorAll`, but first a note
about selectors:

#### Selectors

Unlike with the `getElement(s)By` family of methods, we need to pass a complete
selector to both `querySelector` and `querySelectorAll` - it's in the name!
What's a selector? A selector is a way of targeting a particular element,
something we learned about when we first covered CSS.

The following is a list of CSS selectors and the JavaScript equivalents you
would use with `querySelector`:

| CSS Selector  | JS Selector   |
| ------------- | ------------- |
| `.class-name` | `.class-name` |
| `#some-id`    | `#some-id`    |
| `h1`          | `h1`          |

They're the same! Phew, that's lucky!

The `querySelector` methods were designed to mimic the way we target elements in
CSS, so the selector we pass in is the same we'd use to style that element!

**`querySelector`**

With `querySelector`, we'll pass in a selector for the element we want to
retrieve from the DOM. The element that we get back will be the first element
that matches that selector.

```js
let title = document.querySelector(".title");
```

We'll only get one element back and it will always be the first element that
matches the selector (in this case, `.title`). If we have more than one element
in the page with that selector and we want to retrieve them all, then we'd use
`querySelectorAll`

**`querySelectorAll`**

With `querySelectorAll`, we'll get back all elements on the page that match the
selector we pass in.

```js
let title = document.querySelectorAll("h2");
```

The above code snippet would return a list of all `h2` elements on the page.

#### I Do: [JS DOM Practice Part 2](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and watch as I demonstrate using the
`querySelector` and `querySelectorAll` methods.

#### You Do: [JS DOM Practice Part 2](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and work through the prompts in the
`queryselector.js` file.

## Setting Data in the DOM

Now that we know how to get elements from the DOM, it'd probably be helpful to
learn what we can do with them. We'll soon learn about adding event listeners to
DOM elements - a way for us to listen for when some event happens to a node
(like it gets clicked) and then perform some response. But there are many other
things we can do with nodes!

Toggle, add, or remove classes, change their styling, animate them, move them
from one part of the page to another, replace their content with new content,
etc. The list goes on!

We're going to focus on three common and helpful ways of working with DOM nodes:

1. Changing the content of a node
1. Updating the class list on an element
1. Getting data from a node

### 1. Content

We'll sometimes have an element and want to change the text or html contained
within that element. This is commonly called _templating_ and there are
libraries that will make it a little easier. But with the new template literal
syntax in ES6, we can often get away without a templating library. We could just
use the list of properties below to reset the html or text of an element and
interpolate data in to it.

Every DOM node has the following properties:

- `innerHTML` / `outerHTML`
- `innerText` / 
- `textContent`

#### What about `outerText`?
There's also a [non-standard `outerText`property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/outerText). It is not implemented consistently across browsers and should be avoided!


#### I Do: [JS DOM Practice Part 3](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and watch as I demonstrate updating the content of
a DOM node.

#### You Do: [JS DOM Practice Part 3](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and work through the prompts in the
`dom_content.js` file.

### 2. Class list API

A very common task in JavaScript is toggling CSS classes. This is way more
common than you think! Whenever something is hidden or shown to the user, it's
likely being handled by adding or removing a class from the element with
JavaScript.

In fact, most transitions, animations, or other UI updates are handled in this
way: using JavaScript to add or remove a CSS class.

We'll remove a `.is-hidden` class when the user clicks on something or we'll add
an `is-active` class a navigation element when someone clicks on a hamburger
menu.

The way we get and set classes on nodes is with the `classList` API. The
`classList` API has three key methods we need to learn:

| Method | Description |
| --- | --- |
| `add` | Add a class |
| `remove` | Remove a class |
| `toggle` | toggle a class |

#### I Do: [JS DOM Practice Part 4](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and watch as I demonstrate adding, removing, and
toggling classes with JavaScript

#### You Do: [JS DOM Practice Part 4](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and work through the prompts in the
`classlist.js` file.

### 3. Dataset

Part of HTML5 includes the `data-*` attribute: a way for us to attach arbitrary
data to an element.

If we define a `div` element with a `data-name="A Great Div"` attribute, then
our `dataset` property inside our node will be an object with a `name` key
holding the string `"A Great Div"`.

```html
<div id="great" data-name="A Great Div"></div>

let div = document.getElementById('great') console.log(div.dataset)
```

This doesn't seem immediately useful, but it functions as a bit of a catch-all
for whenever we need to include data to describe a DOM node.

#### I Do: [JS DOM Practice Part 5](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and watch as I demonstrate getting a data
attribute from an element.

#### You Do: [JS DOM Practice Part 5](https://git.generalassemb.ly/dc-wdi-fundamentals/js-dom-practice) 

Open up the practice exercise and work through the prompts in the
`data-attribute.js` file.

## Additional Resources

- [Document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelector)
- [Document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
- [Document.getElementById()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById)
- [Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
- [Document.getElementsByTagName()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName)

## [License](LICENSE)

1. All content is licensed under a CC­BY­NC­SA 4.0 license.
1. All software code is licensed under GNU GPLv3. For commercial use or
   alternative licensing, please contact legal@ga.co.
