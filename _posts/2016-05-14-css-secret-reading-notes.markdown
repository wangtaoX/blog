---
title: '"CSS secrets" Reading Notes'
layout: post
tags:
    - css
---

### currentColor

In css3, we got a special new color keyword **currentColor**, which always resolves to the value of the **color** property, make it **the first ever variable** in css.

```CSS
.dont-do-this {
  height: 2em;
  width: 1em;
  background: currentColor;
}
```
It will become even more useful when we get functions to manipulate colors in native css.

### Use shorthands wisely

```CSS
.positive-bg {
  background: blue;
  /*background-color: blue;*/
}
```
It is good defensive coding and future-proofing to use them, unless we intentionally want to use cascaded properties.

### background-clip

```CSS
.photo-box {
  border: .4em solid rgba(255, 255, 255, .5);
  border-radius: .4em;
  font-size: 120%;
  line-height: 1.5;
  width: 720px;
  background: rgba(255, 255, 255);
  background-clip: padding-box;
}
```

### outline

**outline** do not fellow the elements’s rounding but **box-shadow** do

```css
.box {
  background: blue;
  border-radius: .8em;
  padding: 1em;
  box-shadow: 0 0 0 .8em red;
  outline: .8em solid red;
}
```

### linear-gradient

```css
.bg {
  background: linear-gradient(red 20%, blue 80%);
  ....
  /* 80% － 20% is the length of gradient area */
}
```

If we set the color position at 0, it means its position is set to where the previous one stop.

### box-shadow

```css
.box {
  box-shadow: 0 0 10px blue;
}
```

### z-index

First of all, z-index only works on positioned elements. If you try to set a z-index on an element with no position specified, it will do nothing. Secondly, z-index values can create stacking contexts.

Every stacking context has a single HTML element as its root element. When a new stacking context is formed on an element, that stacking context confines all of its child elements to a particular place in the stacking order, That means that if an element is contained in a stacking context at the bottom of the stacking order, there is no way to get it to appear in front of another element in a different stacking context that is higher in the stacking order, even with a z-index of a billion!

New stacking contexts can be formed on an element in one of three ways:

- When an element is the root element of a document (the **html** element)
- When an element has a position value other than static and a z-index value other than auto
- When an element has an opacity value less than 1

In addition to opacity, several newer CSS properties also create stacking contexts. These include: transforms, filters, css-regions, paged media, and possibly others. As a general rule, it seems that if a CSS property requires rendering in an offscreen context, it must create a new stacking context.

Here are the basic rules to determine stacking order within a single stacking context (from back to front):

1. The stacking context’s root element
2. Positioned elements (and their children) with negative z-index values (higher values are stacked in front of lower values; elements with the same value are stacked according to appearance in the HTML)
3. Non-positioned elements (ordered by appearance in the HTML)
4. Positioned elements (and their children) with a z-index value of auto (ordered by appearance in the HTML)
5. Positioned elements (and their children) with positive z-index values (higher values are stacked in front of lower values; elements with the same value are stacked according to appearance in the HTML)

Note: positioned elements with negative z-indexes are ordered first within a stacking context, which means they appear behind all other elements. Because of this, it becomes possible for an element to appear behind its own parent, which is normally not possible. This will only work if the element’s parent is in the same stacking context and is not the root element of that stacking context.
