---
title: "Window: getDefaultComputedStyle() method"
short-title: getDefaultComputedStyle()
slug: Web/API/Window/getDefaultComputedStyle
page-type: web-api-instance-method
status:
  - non-standard
browser-compat: api.Window.getDefaultComputedStyle
---

{{APIRef("CSSOM")}}{{Non-standard_Header}}

The **`getDefaultComputedStyle()`** method gives the default [computed values](/en-US/docs/Web/CSS/CSS_cascade/Value_processing#computed_value) of all the CSS
properties of an element, ignoring author styling. That is, only user-agent and user
styles are taken into account.

## Syntax

```js-nolint
getDefaultComputedStyle(element)
getDefaultComputedStyle(element, pseudoElt)
```

### Parameters

- `element`
  - : The {{domxref("Element")}} for which to get the computed style.
- `pseudoElt` {{optional_inline}}
  - : A string specifying the pseudo-element to match. Must be `null` (or not
    specified) for regular elements.

### Return value

The returned `style` is a [`CSSStyleDeclaration`](/en-US/docs/Web/API/CSSStyleDeclaration)
object. The object is of the same type as the object returned by
{{domxref("Window.getComputedStyle()")}}, but only takes into account user-agent and
user rules.

## Examples

### Simple example

```js
const elem = document.getElementById("elemId");
const style = getDefaultComputedStyle(elem);
```

### Longer example

```html
<div id="elem-container">dummy</div>
<div id="output"></div>
```

```css
#elem-container {
  position: absolute;
  left: 100px;
  top: 200px;
  height: 100px;
}
```

```js
const elem = document.getElementById("elem-container");
const theCSSprop = getDefaultComputedStyle(elem).position;
document.getElementById("output").textContent = theCSSprop; // outputs "static"
```

### Use with pseudo-elements

The `getDefaultComputedStyle()` method can pull style info from
pseudo-elements (e.g., {{cssxref("::before")}} or {{cssxref("::after")}}).

```html
<h3>generated content</h3>
```

```css
h3::after {
  content: " rocks!";
}
```

```js
const h3 = document.querySelector("h3");
const result = getDefaultComputedStyle(h3, "::after").content;

console.log("the generated content is: ", result); // returns 'none'
```

## Notes

The returned value is, in certain known cases, expressly incorrect by deliberate
intent. In particular, to avoid the so called CSS History Leak security issue, browsers
may expressly "lie" about the used value for a link and always return values as if a
user has never visited the linked site, and/or limit the styles that can be applied
using the `:visited` pseudo-selector. See <https://blog.mozilla.org/security/2010/03/31/plugging-the-css-history-leak/>
and <https://hacks.mozilla.org/2010/03/privacy-related-changes-coming-to-css-vistited/>
for details of the examples of how this is implemented.

## Specifications

Proposed to the CSS working group.

## Browser compatibility

{{Compat}}
