---
show:
  - toc
---

# Shorthands

Using CSS shorthand properties allows you to set multiple related CSS properties in a single line. This makes CSS code more concise and readable.

## Summary Table

| Property          | Shorthand Example                                        |
| ----------------- | -------------------------------------------------------- |
| `animation`       | `animation: slide 2s ease-in 0.5s;`                      |
| `background`      | `background: #f0f0f0 url('image.jpg') no-repeat center;` |
| `border`          | `border: 2px solid black;`                               |
| `border-radius`   | `border-radius: 10px 20px 30px 40px;`                    |
| `box-shadow`      | `box-shadow: 10px 10px 5px rgba(0,0,0,0.75);`            |
| `columns`         | `columns: 200px 3;`                                      |
| `font`            | `font: italic bold 16px/1.5 Arial, sans-serif;`          |
| `list-style`      | `list-style: square inside none;`                        |
| `margin`          | `margin: 10px 20px;`                                     |
| `padding`         | `padding: 15px 25px;`                                    |
| `outline`         | `outline: 2px solid red;`                                |
| `overflow`        | `overflow: hidden auto;`                                 |
| `transition`      | `transition: background-color 0.3s ease-in-out;`         |
| `text-decoration` | `text-decoration: underline dotted blue;`                |
| `text-shadow`     | `text-shadow: 2px 2px 5px rgba(0,0,0,0.3);`              |
| `flex`            | `flex: 1 0 auto;`                                        |
| `grid`            | `grid: 100px 200px / 1fr 2fr;`                           |
| `gap`             | `gap: 10px 15px;`                                        |
| `place-items`     | `place-items: center start;`                             |

---

## Animation

Shorthand for all the `animation` properties: `name`, `duration`, `timing-function`, `delay`, `iteration-count`, `direction`, `fill-mode`, and `play-state`.

```css
/* Longhand */
animation-name: slide;
animation-duration: 2s;
animation-timing-function: ease-in;
animation-delay: 0.5s;

/* Shorthand */
animation: slide 2s ease-in 0.5s;
```

---

## Background

Combines background-related properties like `color`, `image`, `position`, `size`, `repeat`, and more.

```css
/* Longhand */
background-color: #f0f0f0;
background-image: url('image.jpg');
background-repeat: no-repeat;
background-position: center;

/* Shorthand */
background: #f0f0f0 url('image.jpg') no-repeat center;

/* Shorthand with size */
background: #f0f0f0 url('image.jpg') no-repeat center / cover;
```

---

## Border

Sets multiple border properties (`width`, `style`, `color`) at once.

```css
/* Longhand */
border-width: 2px;
border-style: solid;
border-color: black;

/* Shorthand */
border: 2px solid black;

/* Shorthand for top border */
border-top: 3px dotted blue;
```

---

## Border-radius

Defines the rounding of the corners of an element, for all four corners or each one individually.

```css
/* Longhand */
border-top-left-radius: 10px;
border-top-right-radius: 20px;
border-bottom-right-radius: 30px;
border-bottom-left-radius: 40px;

/* Shorthand */
border-radius: 10px 20px 30px 40px; /* TL, TR, BR, BL */
```

---

## Box-shadow

Shorthand for defining multiple box shadows. You can specify values for horizontal and vertical offsets, blur radius, spread radius, and color.

```css
/* Longhand */
box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);

/* Shorthand */
box-shadow: 10px 10px 5px rgba(0,0,0,0.75);
```

---

## Columns

Shorthand for defining the number of columns (`column-count`) and their width (`column-width`) in a multi-column layout.

```css
/* Longhand */
column-count: 3;
column-width: 200px;

/* Shorthand */
columns: 200px 3;
```

---

## Font

Shorthand for `font-style`, `font-variant`, `font-weight`, `font-size`, `line-height`, and `font-family`.

```css
/* Longhand */
font-style: italic;
font-weight: bold;
font-size: 16px;
line-height: 1.5;
font-family: Arial, sans-serif;

/* Shorthand */
font: italic bold 16px/1.5 Arial, sans-serif;
```

---

## List-style

Combines properties for list appearance like `list-style-type`, `list-style-position`, and `list-style-image`.

```css
/* Longhand */
list-style-type: square;
list-style-position: inside;
list-style-image: none;

/* Shorthand */
list-style: square inside none;
```

---

## Margin

Sets the `margin` for all four sides (top, right, bottom, left) in one declaration.

```css
/* Longhand */
margin-top: 10px;
margin-right: 20px;
margin-bottom: 10px;
margin-left: 20px;

/* Shorthand */
margin: 10px 20px; /* Top/bottom: 10px, Right/left: 20px */

/* Shorthand for all sides (top, right, bottom, left) */
margin: 10px 20px 30px 40px;
```

---

## Padding

Sets the `padding` for all four sides similarly to `margin`.

```css
/* Longhand */
padding-top: 15px;
padding-right: 25px;
padding-bottom: 15px;
padding-left: 25px;

/* Shorthand */
padding: 15px 25px; /* Top/bottom: 15px, Right/left: 25px */

/* Shorthand for all sides */
padding: 5px 10px 15px 20px; /* Top, Right, Bottom, Left */
```

---

## Outline

Shorthand for `outline-width`, `outline-style`, and `outline-color`.

```css
/* Longhand */
outline-width: 2px;
outline-style: solid;
outline-color: red;

/* Shorthand */
outline: 2px solid red;
```

---

## Overflow

Shorthand for `overflow-x` and `overflow-y`.

```css
/* Longhand */
overflow-x: hidden;
overflow-y: auto;

/* Shorthand */
overflow: hidden auto;
```

---

## Transition

Shorthand for transition-related properties: `property`, `duration`, `timing-function`, and `delay`.

```css
/* Longhand */
transition-property: background-color;
transition-duration: 0.3s;
transition-timing-function: ease-in-out;

/* Shorthand */
transition: background-color 0.3s ease-in-out;
```

---


## Text-decoration

Shorthand for `text-decoration-line`, `text-decoration-color`, and `text-decoration-style`.

```css
/* Longhand */
text-decoration-line: underline;
text-decoration-color: blue;
text-decoration-style: dotted;

/* Shorthand */
text-decoration: underline dotted blue;
```

---

## Text-shadow

Defines shadow effects for text. You can specify horizontal offset, vertical offset, blur radius, and color.

```css
/* Longhand */
text-shadow: 2px 2px 5px rgba(0,0,0,0.3);

/* Shorthand */
text-shadow: 2px 2px 5px rgba(0,0,0,0.3);
```

---

## Flex

Shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`.

```css
/* Longhand */
flex-grow: 1;
flex-shrink: 0;
flex-basis: auto;

/* Shorthand */
flex: 1 0 auto;
```

---

## Grid

Shorthand for setting both `grid-template-rows` and `grid-template-columns` (along with other grid properties).

```css
/* Longhand */
grid-template-rows: 100px 200px;
grid-template-columns: 1fr 2fr;

/* Shorthand */
grid: 100px 200px / 1fr 2fr;
```

## Gap (for Flexbox or Grid)

Shorthand for `row-gap` and `column-gap`.

```css
/* Longhand */
row-gap: 10px;
column-gap: 15px;

/* Shorthand */
gap: 10px 15px;
```

---

## Place-items (for Grid or Flexbox)

Shorthand for `align-items` and `justify-items`.

```css
/* Longhand */
align-items: center;
justify-items: start;

/* Shorthand */
place-items: center start;
```
