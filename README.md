# Domm

> A functional DOM traversal and manipulation library for modern browsers

[![Build Status](https://travis-ci.org/kasperisager/doem.svg?branch=master)](https://travis-ci.org/kasperisager/doem) [![Inline docs](http://inch-ci.org/github/kasperisager/doem.svg?branch=master)](http://inch-ci.org/github/kasperisager/doem)

Døm was born out of the need of a minimal set of functional-style DOM utilities that could replace core jQuery in [modern browsers](#browser-support). It relies only on the latest native browser APIs, making the library light-weight and fast. Much inspiration was taken from [You Don't Need jQuery](https://github.com/oneuijs/You-Dont-Need-jQuery).

## Contents

- [Installation](#installation)
- [Usage](#usage)
- [API](#api)
- [Browser support](#browser-support)
- [License](#license)

## Installation

```sh
$ npm i @ver5/domm
```

## Usage

[<img src="https://www.npmjs.com/static/images/runkit.svg" width=24 align=top> __Try out Døm in your browser__](https://runkit.com/npm/doem)

```js
import {find, html, [...]} from '@ver5/domm';

const el = find(document, '.foo');
html(el, 'Hello World!');
```

## API

### addClass

Add a class to an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to add the class to.
-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The name of the class to add.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
addClass(element, 'foo');
```

```html
<p class=foo>Lorem ipsum</p>
```

### after

Insert HTML after an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to insert the HTML after.
-   `html` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The HTML to insert after the element.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
after(element, '<p>Dolor sit amet</p>');
```

```html
<p>Lorem ipsum</p><p>Dolor sit amet</p>
```

### append

Insert HTML at the end of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to insert the HTML at the end of.
-   `html` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The HTML to insert at the end of the element.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
append(element, '<b>dolor sit amet</b>');
```

```html
<p>Lorem ipsum<b>dolor sit amet</b></p>
```

### attr

Get or set the value of an attribute of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose attribute to get or set.
-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The name of the attribute to get or set.
-   `value` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)=** The value of the attribute if setting.

**Examples**

```html
<img title="Lorem ipsum">
```

```js
const element = find(document, 'img');
attr(element, 'title');
// => 'Lorem ipsum'
attr(element, 'title', 'Dolor sit amet')
```

```html
<img title="Dolor sit amet">
```

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The value of the attribute if getting.

### before

Insert HTML before an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to insert the HTML before.
-   `html` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The HTML to insert before the element.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
before(element, '<p>Dolor sit amet</p>');
```

```html
<p>Dolor sit amet</p><p>Lorem ipsum</p>
```

### children

Get all the children of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose children to get.

**Examples**

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

```js
const element = find(document, 'ul');
children(element);
// => [<li>Item 1</li>, <li>Item 2</li>]
```

Returns **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).&lt;[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)>** The children of the element.

### clone

Create a deep copy on an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to copy.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
element !== clone(element);
// => true
```

Returns **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The copy of the element.

### closest

Get the closest matching descendant of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose descendant to get.
-   `selector` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The selector to match against.

**Examples**

```html
<ul class="lvl-1">
  <li class="item-1">Item 1
    <ul class="lvl-2">
      <li class="item-2">Item 2</li>
    </ul>
  </li>
</ul>
```

```js
const element = find(document, '.item-2');
closest(element, 'ul');
// => <ul class="lvl-2">...</ul>
```

Returns **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The closest matching descendant if found.

### contains

Check if an element is a descendant of another element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The parent element to check against.
-   `child` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The child element to check for.

**Examples**

```html
<div class=foo>
  <div class=bar></div>
</div>
```

```js
const foo = find(document, '.foo');
const bar = find(document, '.bar');
contains(foo, bar);
// => true
```

Returns **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** True if the child is a descendant of the parent.

### css

Get or set the value of a CSS property of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose CSS property to get or set.
-   `property` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The CSS property to get or set.
-   `value` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)=** The value of the CSS property if setting.

**Examples**

```css
p {
  color: red;
}
```

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
css(element, 'color');
// => rgb(255, 0, 0)
css(element, 'color', 'blue');
```

```html
<p style="color: blue;">Lorem ipsum</p>
```

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The value of the CSS property if getting.

### data

Get or set the value of a data attribute of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose data attribute to get or set.
-   `key` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The key of the data attribute to get or set.
-   `value` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)=** The value of the data attribute if setting.

**Examples**

```html
<p data-foo=bar>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
data(element, 'foo');
// => 'bar'
data(element, 'foo', 'baz')
```

```html
<p data-foo=baz>Lorem ipsum</p>
```

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The value of the data attribute if getting.

### empty

Remove all children (including text) from an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose children to remove.

**Examples**

```html
<p>Lorem <b>ipsum</b></p>
```

```js
const element = find(document, 'p');
empty(element);
```

```html
<p></p>
```

### find

Find the first element matching a query.

**Parameters**

-   `scope` **([Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)\|[Document](https://developer.mozilla.org/en-US/docs/Web/JavaScript))** The scope to look through.
-   `query` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The query to use for looking up the element.

**Examples**

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

```js
find(document, 'li');
// => <li>Item 1</li>
```

Returns **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element if found.

### findAll

Find all elements matching a query.

**Parameters**

-   `scope` **([Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)\|[Document](https://developer.mozilla.org/en-US/docs/Web/JavaScript))** The scope to look through.
-   `query` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The query to use for looking up the elements.

**Examples**

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

```html
findAll(document, 'li');
// => [<li>Item 1</li>, <li>Item 2</li>]
```

Returns **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).&lt;[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)>** The elements if found.

### has

Check if an element has a descendant matching a selector.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to check.
-   `selector` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The selector to match against.

**Examples**

```html
<div class=foo>
  <div class=bar></div>
</div>
```

```js
const element = find(document, '.foo');
has(element, '.bar');
// => true
```

Returns **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** True if the element has a descendant matching the selector.

### hasClass

Check if an element has a class.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to check.
-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The name of the class to check for.

**Examples**

```html
<p class=foo>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
hasClass(element, 'foo');
// => true
```

Returns **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** True if the element has the class.

### height

Get the computed height of a node.

**Parameters**

-   `node` **([Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)\|[Document](https://developer.mozilla.org/en-US/docs/Web/JavaScript)\|[Window](https://developer.mozilla.org/en-US/docs/Web/API/Window))** The node whose computed height to get.

**Examples**

```css
div {
  padding: 10px 0 5px;
}
p {
  line-height: 20px;
}
```

```html
<div>
  <p>Lorem ipsum</p>
</div>
```

```js
const element = find(document, 'div');
height(element);
// => 35
```

Returns **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** The computed height of the node.

### html

Get or set the inner HTML of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose inner HTML to get or set.
-   `content` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The content of the inner HTML if setting.

**Examples**

```html
<p>Lorem <b>ipsum</b></p>
```

```js
const element = find(document, 'p');
html(element);
// => 'Lorem <b>ipsum</b>''
html(element, 'Dolor sit <b>amet</b>');
```

```html
<p>Dolor sit <b>amet</b></p>
```

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The inner HTML of the element if getting.

### matches

Check if an element matches a selector.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to check.
-   `selector` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The selector to check against.

**Examples**

```html
<p class=foo>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
matches(element, 'div.foo');
// => true
```

Returns **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** True if the element matches the selector.

### next

Get the next sibling of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose sibling to get.

**Examples**

```html
<p class=foo>Lorem ipsum</p>
<p>Dolor sit amet</p>
```

```js
const element = find(document, '.foo');
next(element);
// => <p>Dolor sit amet</p>
```

Returns **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The sibling of the element if found.

### offset

Get the current coordinates of an element relative to its document

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose coordinates to get.

**Examples**

```css
div {
  margin-lef: 10px;
  line-height: 20px;
}
```

```html
<div>Lorem ipsum</div>
<div class=foo>Dolor sit amet</div>
```

```js
const element = find(document, '.foo');
offset(element);
// => {top: 20, left: 10}
```

Returns **{top: [number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number), left: [number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)}** The current coordinates of the element.

### parent

Get the parent of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose parent to get.

**Examples**

```html
<div>
  <p>Lorem ipsum</p>
</div>
```

```js
const element = find(document, 'p');
parent(element);
// => <div>...</div>
```

Returns **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The parent element if found.

### parents

Get all the parents of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose parents to get.

**Examples**

```html
<div>
  <p>Lorem <b>ipsum</b></p>
</div>
```

```js
const element = find(document, 'b');
parents(element);
// => [<p>...</p>, <div>...</div>]
```

Returns **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).&lt;[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)>** The parents of the element.

### position

Get the current coordinates of an element relative to its offset parent.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose coordinates to get.

**Examples**

```css
div {
  padding: 20px 10px;
}
```

```html
<div>
  <span>Lorem ipsum</span>
</div>
```

```js
const element = find(document, 'span');
position(element);
// => {top: 20, left: 10}
```

Returns **{top: [number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number), left: [number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)}** The current coordinates of the element.

### prepend

Insert HTML at the beginnig of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to insert the HTML at the beginning of.
-   `html` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The HTML to insert at the beginning of the element.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
append(element, '<b>Dolor sit amet</b>');
```

```html
<p><b>Dolor sit amet</b>Lorem ipsum</p>
```

### prev

Get the previous sibling of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose sibling to get.

**Examples**

```html
<p>Lorem ipsum</p>
<p class=foo>Dolor sit amet</p>
```

```js
const element = find(document, '.foo');
prev(element);
// => <p>Lorem ipsum</p>
```

Returns **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The sibling of the element if found.

### remove

Remove an element from its parent.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to remove.

**Examples**

```html
<p>Lorem <b>ipsum</b></p>
```

```js
const element = find(document, 'b');
remove(element);
```

```html
<p>Lorem </p>
```

### removeAttr

Remove an attribute from an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose attribute to remove.
-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The name of the attribute to remove.

**Examples**

```html
<img title="Lorem ipsum">
```

```js
const element = find(document, 'img');
removeAttr(element, 'title');
```

```html
<img>
```

### removeClass

Remove a class from an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to remove the class from.
-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The name of the class to remove.

**Examples**

```js
<p class="foo bar">Lorem ipsum</p>
```

```js
const element = find(document, 'p');
removeClass(element, 'foo');
```

```html
<p class=bar>Lorem ipsum</p>
```

### removeData

Remove a data attribute from an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose data attribute to remove.
-   `key` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The key of the data attribute to remove.

**Examples**

```html
<p data-foo=bar>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
removeData(element, 'foo');
```

```html
<p>Lorem ipsum</p>
```

### replace

Replace an element with HTML.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to replace with HTML.
-   `html` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The HTML to replace the element with.

**Examples**

```html
<p>Lorem <b>ipsum<b></p>
```

```js
const element = find(document, 'b');
replace(element, '<i>ipsum</i>');
```

```html
<p>Lorem <i>ipsum<i></p>
```

### siblings

Get all the siblings of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose siblings to get.

**Examples**

```html
<ul>
  <li>Item 1</li>
  <li class=foo>Item 2</li>
  <li>Item 3</li>
</ul>
```

```js
const element = find(document, '.foo');
siblings(element);
// => [<li>Item 1</li>, <li>Item 2</li>]
```

Returns **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).&lt;[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)>** The siblings of the element.

### style

Get the computed style of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose computed style to get.

**Examples**

```css
p {
  color: red;
}
```

```html
<p style="float: right;">Lorem ipsum</p>
```

```js
const element = find(document, 'p');
style(element);
// => CSSStyleDeclaration { color: 'rgb(255, 0, 0)', float: 'right', ... }
```

Returns **CSSStyleDeclaration** The computed style of the element.

### tag

Get the tag name of the element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose tag name to get.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
tag(element);
// => 'p'
```

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The tag name of the element.

### text

Get or set the text content of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose text content to get or set.
-   `content` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)=** The text content if setting.

**Examples**

```html
<p>Lorem <b>ipsum</b></p>
```

```js
const element = find(document, 'p');
text(element);
// => 'Lorem ipsum'
text(element, 'Lorem ipsum');
```

```html
<p>Lorem ipsum</p>
```

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The text content if getting.

### toggleClass

Toggle a class on an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to toggle the class on.
-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The name of the class to toggle.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
toggleClass(element, 'foo');
```

```html
<p class=foo>Lorem ipsum</p>
```

```js
toggleClass(element, 'foo');
```

```html
<p>Lorem ipsum</p>
```

### unwrap

Remove the parent of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose parent to remove.

**Examples**

```html
<div>
  <p class=foo>Lorem ipsum</p>
  <p>Dolor sit amet</p>
</div>
```

```js
const element = find(document, '.foo');
unwrap(element);
```

```html
<p class=foo>Lorem ipsum</p>
<p>Dolor sit amet</p>
```

### val

Get or set the value of an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element whose value to get or set.
-   `value` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)=** The value of the element if setting.

**Examples**

```html
<input value=foo></input>
```

```js
const element = find(document, 'input');
val(element);
// => 'foo'
val(element, 'bar');
```

```html
<input value=bar></input>
```

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The value of the element if getting.

### width

Get the computed width of a node.

**Parameters**

-   `node` **([Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)\|[Document](https://developer.mozilla.org/en-US/docs/Web/JavaScript)\|[Window](https://developer.mozilla.org/en-US/docs/Web/API/Window))** The node whose computed width to get.

**Examples**

```css
div {
  padding: 0 10px;
}
p {
  width: 40px;
}
```

```html
<div>
  <p>Lorem ipsum</p>
</div>
```

```js
const element = find(document, 'div');
width(element);
// => 60
```

Returns **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** The computed width of the node.

### wrap

Wrap an HTML structure around an element.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** The element to wrap the HTML structure around.
-   `html` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The HTML structure to wrap around the element.

**Examples**

```html
<p>Lorem ipsum</p>
```

```js
const element = find(document, 'p');
wrap(element, '<div></div>');
```

```html
<div>
  <p>Lorem ipsum</p>
</div>
```

## Browser support

<img alt=Chrome width=64 src=https://raw.github.com/alrra/browser-logos/39.0.0/src/chrome/chrome_128x128.png> | <img alt=Firefox width=64 src=https://raw.github.com/alrra/browser-logos/39.0.0/src/firefox/firefox_128x128.png> | <img alt=IE width=64 src=https://raw.github.com/alrra/browser-logos/39.0.0/src/archive/internet-explorer_9-11/internet-explorer_9-11_128x128.png> | <img alt=Opera width=64 src=https://raw.github.com/alrra/browser-logos/39.0.0/src/opera/opera_128x128.png> | <img alt=Safari width=64 src=https://raw.github.com/alrra/browser-logos/39.0.0/src/safari/safari_128x128.png>
:---: | :---: | :---: | :---: | :---:
Latest ✔ | Latest ✔ | 11+ ✔ | Latest ✔ | 6.1+ ✔

## License

Copyright &copy; 2016 [Kasper Kronborg Isager](https://github.com/kasperisager). Licensed under the terms of the [MIT license](LICENSE.md).
