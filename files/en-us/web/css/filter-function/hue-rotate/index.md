---
title: hue-rotate()
slug: Web/CSS/filter-function/hue-rotate
page-type: css-function
browser-compat: css.types.filter-function.hue-rotate
sidebar: cssref
---

The **`hue-rotate()`** [CSS](/en-US/docs/Web/CSS) [function](/en-US/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) rotates the [hue](https://en.wikipedia.org/wiki/Hue) of an element and its contents. Its result is a {{cssxref("&lt;filter-function&gt;")}}.

> [!NOTE]
> `hue-rotate()` is specified as a matrix operation on the RGB color. It does not actually convert the color to the HSL model, which is a non-linear operation. Therefore, it may not preserve the saturation or lightness of the original color, especially for saturated colors.

{{InteractiveExample("CSS Demo: hue-rotate()")}}

```css interactive-example-choice
filter: hue-rotate(0);
```

```css interactive-example-choice
filter: hue-rotate(90deg);
```

```css interactive-example-choice
filter: hue-rotate(-0.25turn);
```

```css interactive-example-choice
filter: hue-rotate(3.142rad);
```

```html interactive-example
<section id="default-example">
  <img
    class="transition-all"
    id="example-element"
    src="/shared-assets/images/examples/firefox-logo.svg"
    width="200" />
</section>
```

## Syntax

```css
hue-rotate(angle)
```

### Values

- `angle` {{Optional_Inline}}
  - : The relative change in hue of the input sample, specified as an {{cssxref("&lt;angle&gt;")}}. A value of `0deg` leaves the input unchanged. A positive hue rotation increases the hue value, while a negative rotation decreases the hue value. The initial value for {{Glossary("interpolation")}} is `0`. There is no minimum or maximum value. The effect of values above `360deg` are, given `hue-rotate(Ndeg)`, evaluates to `N` modulo 360. The default value is `0deg`.

The `<angle>` CSS data type represents an angle value expressed in degrees, gradians, radians, or turns. The following are equivalent:

```css
hue-rotate(-180deg)
hue-rotate(540deg)
hue-rotate(200grad)
hue-rotate(3.14159rad)
hue-rotate(0.5turn)
```

## Formal syntax

{{CSSSyntax}}

## Examples

### With the backdrop-filter property

This example applies a `hue-rotate()` filter via the `backdrop-filter` CSS property to the paragraph, color shifting to the area behind the `<p>`.

```css
.container {
  background: url("/shared-assets/images/examples/listen_to_black_women.jpg")
    no-repeat left / contain #011296;
}
p {
  backdrop-filter: hue-rotate(240deg);
  text-shadow: 2px 2px #011296;
}
```

```css hidden
.container {
  padding: 3rem;
  width: 30rem;
}
p {
  padding: 0.5rem;
  color: #ffffff;
  font-size: 2rem;
  font-family: sans-serif;
}
```

```html hidden
<div class="container">
  <p>
    Text on images can be illegible and inaccessible even with a drop shadow.
  </p>
</div>
```

{{EmbedLiveSample('With_the_backdrop-filter_property','100%','280')}}

### With the filter property

This example applies a `hue-rotate()` filter via the `filter` CSS property adding the color shift to the entire element, including content, border, and background image.

```css
p {
  filter: hue-rotate(-60deg);
  text-shadow: 2px 2px blue;
  background-color: magenta;
  color: goldenrod;
  border: 1em solid rebeccapurple;
  box-shadow:
    inset -5px -5px red,
    5px 5px yellow;
}
```

```css hidden
p {
  padding: 0.5rem;
  font-size: 2rem;
  font-family: sans-serif;
  width: 85vw;
}
```

```html hidden
<p>The person who wrote this example is not a designer, fortunately.</p>
```

{{EmbedLiveSample('With_the_filter_property','100%','220')}}

### With url() and the SVG hue-rotate filter

The SVG {{SVGElement("filter")}} element is used to define custom filter effects that can then be referenced by [`id`](/en-US/docs/Web/HTML/Reference/Global_attributes/id). The `<filter>`'s {{SVGElement("feColorMatrix")}} primitive `hueRotate` type provides the same effect. Given the following:

```html live-sample___svg_filter
<svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 220 220"
  color-interpolation-filters="sRGB"
  height="220"
  width="220">
  <filter id="hue-rotate">
    <feColorMatrix type="hueRotate" values="90" />
  </filter>
</svg>
```

These values produce the same results:

```css
filter: hue-rotate(90deg); /* 90deg rotation */
filter: url("#hue-rotate"); /* with embedded SVG */
filter: url("folder/fileName.svg#hue-rotate"); /* external svg filter definition */
```

This example shows three images: the image with a `hue-rotate()` filter function applied, the image with an equivalent `url()` filter applied, and the original images for comparison:

```html hidden live-sample___svg_filter
<table cellpadding="5">
  <thead>
    <tr>
      <th><code>hue-rotate()</code></th>
      <th><code>url()</code></th>
      <th>Original image</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <img
          class="css-filter"
          src="https://mdn.github.io/shared-assets/images/examples/progress-pride-flag.jpg"
          alt="Pride flag with rotated colors" />
      </td>
      <td>
        <img
          class="svg-filter"
          src="https://mdn.github.io/shared-assets/images/examples/progress-pride-flag.jpg"
          alt="Pride flag with rotated colors" />
      </td>
      <td>
        <img
          src="https://mdn.github.io/shared-assets/images/examples/progress-pride-flag.jpg"
          alt="Pride flag" />
      </td>
    </tr>
  </tbody>
</table>
```

```css hidden live-sample___svg_filter
.css-filter {
  filter: hue-rotate(90deg);
}
.svg-filter {
  filter: url("#hue-rotate");
}
svg:not(:root) {
  display: none;
}
```

{{EmbedLiveSample('svg_filter','100%','280')}}

### hue-rotate() does not preserve saturation or lightness

The diagram below compares two color gradients starting with red: the first is generated using `hue-rotate()`, and the second uses actual HSL color values. Note how the `hue-rotate()` gradient shows obvious differences in saturation and lightness in the middle.

```html
<div>
  <p>Using <code>hue-rotate()</code></p>
  <div id="hue-rotate"></div>
</div>
<div>
  <p>Using <code>hsl()</code></p>
  <div id="hsl"></div>
</div>
```

```css hidden
#hue-rotate,
#hsl {
  display: flex;
  margin: 1em 0;
}

#hue-rotate div,
#hsl div {
  width: 2px;
  height: 100px;
}
```

```js
const hueRotate = document.getElementById("hue-rotate");
const hsl = document.getElementById("hsl");

for (let i = 0; i < 360; i++) {
  const div1 = document.createElement("div");
  div1.style.backgroundColor = `hsl(${i}, 100%, 50%)`;
  hsl.appendChild(div1);

  const div2 = document.createElement("div");
  div2.style.backgroundColor = "red";
  div2.style.filter = `hue-rotate(${i}deg)`;
  hueRotate.appendChild(div2);
}
```

{{EmbedLiveSample('hue-rotate_does_not_preserve_saturation_or_lightness','100%','350')}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [CSS filter effects](/en-US/docs/Web/CSS/CSS_filter_effects) module
- The other {{cssxref("&lt;filter-function&gt;")}} functions available to be used in values of the {{cssxref("filter")}} and {{cssxref("backdrop-filter")}} properties include:
  - {{cssxref("filter-function/blur", "blur()")}}
  - {{cssxref("filter-function/brightness", "brightness()")}}
  - {{cssxref("filter-function/contrast", "contrast()")}}
  - {{cssxref("filter-function/drop-shadow", "drop-shadow()")}}
  - {{cssxref("filter-function/grayscale", "grayscale()")}}
  - {{cssxref("filter-function/invert", "invert()")}}
  - {{cssxref("filter-function/opacity", "opacity()")}}
  - {{cssxref("filter-function/saturate", "saturate()")}}
  - {{cssxref("filter-function/sepia", "sepia()")}}
