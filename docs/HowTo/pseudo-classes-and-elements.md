# Pseudo-classes and Pseudo-elements in Angora CSS

## Overview

Angora CSS provides comprehensive support for CSS pseudo-classes and pseudo-elements, allowing you to create interactive and dynamic styling directly in your HTML class names. This guide covers all supported pseudo-classes, pseudo-elements, and their usage patterns.

## Basic Pseudo-class Syntax

Pseudo-classes in Angora CSS are added directly within the class name using camelCase notation:

```html
<!-- Pseudo-classes are part of the property name -->
<div class="ank-colorHover-red">Red text on hover</div>
<button class="ank-bgFocus-blue">Blue background on focus</button>
<div class="ank-opacityActive-0_5">Semi-transparent when active</div>
```

### Key Features

- **Class Structure**: `ank-propertyPseudo-value` (not separate activator class)
- **Pseudo Notation**: Uses camelCase like `colorHover`, `bgFocus`, `opacityActive`

## Supported Pseudo-classes

### Interactive States

#### :hover

Applied when the user hovers over an element:

```html
<!-- Color changes with Angora CSS -->
<div class="ank-colorHover-blue">Blue text on hover</div>
<div class="ank-bgHover-red">Red background on hover</div>

<!-- Transform effects with Angora CSS -->
<div class="ank-transformHover-scaleSD1_1ED">Scale up on hover</div>
<div class="ank-transformHover-translateYSDMIN5pxED">Move up on hover</div>

<!-- Complex hover effects with Angora CSS -->
<button class="ank-bg-primary ank-color-white ank-bgHover-primary-dark ank-boxShadowHover-0__4px__8px__rgbaSD0COM0COM0COM0_2ED ank-transformHover-translateYSDMIN2pxED">
  Hover Button
</button>
```

#### :focus

Applied when an element has keyboard focus:

```html
<!-- Form inputs with Angora CSS -->
<input class="ank-border-gray-300 ank-borderFocus-blue-500 ank-borderWidthFocus-2px">
<textarea class="ank-outline-none ank-bgFocus-blue-50"></textarea>

<!-- Buttons with Angora CSS -->
<button class="ank-bg-primary ank-boxShadowFocus-0__0__0__3px__rgbaSD0COM123COM255COM0_25ED">
  Focusable Button
</button>
```

#### :active

Applied when an element is being activated (clicked/pressed):

```html
<!-- Button press effects with Angora CSS -->
<button class="ank-transformActive-scaleSD0_95ED">Press effect</button>
<div class="ank-opacityActive-0_8">Fade when pressed</div>
<button class="ank-bgActive-primary-dark">Darker when pressed</button>
```

#### :visited

Applied to visited links:

```html
<a href="#" class="ank-color-blue ank-colorVisited-purple">
  Link that changes color when visited
</a>
```

### Form States

#### :checked

Applied to checked form elements:

```html
<!-- Checkboxes with Angora CSS -->
<input type="checkbox" class="ank-bgChecked-green">
<input type="radio" class="ank-borderChecked-blue">

<!-- Custom checkbox styling with Angora CSS -->
<input type="checkbox" class="ank-appearance-none ank-w-20px ank-h-20px ank-border-2px__solid__gray ank-borderRadius-3px ank-bg-white ank-bgChecked-green ank-borderChecked-green">
```

#### :disabled

Applied to disabled form elements:

```html
<input disabled class="ank-bg-gray-100 ank-color-gray-400 ank-cursor-not-allowed">
<button disabled class="ank-opacityDisabled-0_5 ank-bgDisabled-gray-300">
  Disabled Button
</button>
```

#### :enabled

Applied to enabled form elements:

```html
<input class="ank-border-gray-300 ank-borderEnabled-blue">
<button class="ank-bgEnabled-primary">Enabled Button</button>
```

#### :required

Applied to required form fields:

```html
<input required class="ank-borderRequired-red">
<select required class="ank-outlineRequired-red"></select>
```

#### :valid and :invalid

Applied based on form validation state:

```html
<input type="email" class="ank-border-gray-300 ank-borderValid-green ank-borderInvalid-red">

<input pattern="[0-9]{3}" class="ank-bg-white ank-bgValid-green-100 ank-bgInvalid-red-100">
```

### Structural Pseudo-classes

#### :first-child and :last-child

```html
<!-- First child styling with Angora CSS -->
<div class="ank-borderFirstChild-none">
  <div>No border on first child</div>
  <div>Regular styling</div>
</div>

<!-- Last child styling with Angora CSS -->
<nav class="ank-borderRightLastChild-none">
  <a href="#">Link 1</a>
  <a href="#">Link 2</a>
  <a href="#">Last link (no right border)</a>
</nav>
```

#### :nth-child() with Parameters

Use SD (Start Delimiter) and ED (End Delimiter) for parameters:

```html
<!-- Every second child with Angora CSS -->
<div class="ank-bgNthChildSD2nED-gray-100">
  <div>Normal background</div>
  <div>Gray background (2nd)</div>
  <div>Normal background</div>
  <div>Gray background (4th)</div>
</div>

<!-- Specific positions with Angora CSS -->
<div class="ank-colorNthChildSD3ED-red">
  <div>Normal</div>
  <div>Normal</div>
  <div>Red text (3rd child)</div>
</div>

<!-- Every third child starting from 2nd with Angora CSS -->
<div class="ank-fontWeightNthChildSD3nPLUS2ED-bold">
  <div>Normal</div>
  <div>Bold (2nd)</div>
  <div>Normal</div>
  <div>Normal</div>
  <div>Bold (5th)</div>
</div>
```

#### :nth-of-type()

```html
<!-- Every second paragraph with Angora CSS -->
<div class="ank-colorNthOfTypeSD2nED-blue">
  <h1>Heading</h1>
  <p>First paragraph</p>
  <p>Second paragraph (blue)</p>
  <div>Div element</div>
  <p>Third paragraph</p>
  <p>Fourth paragraph (blue)</p>
</div>
```

### Language and Direction Pseudo-classes

#### :lang()

```html
<!-- Language-specific styling -->
<div class="ank-fontFamilyLangSDenED-serif" lang="en">English text</div>
<div class="ank-fontSizeLangSDfrED-18px" lang="fr">French text</div>
```

#### :dir()

```html
<!-- Direction-based styling -->
<div class="ank-textAlignDirSDrtlED-right" dir="rtl">Right-to-left text</div>
<div class="ank-paddingLeftDirSDltrED-20px" dir="ltr">Left-to-right text</div>
```

## Pseudo-elements

Angora CSS supports modern pseudo-elements for enhanced styling:

### ::before and ::after

```html
<!-- Adding content with pseudo-elements -->
<div class="ank-contentBefore-CDB★CDB ank-colorBefore-gold">
  Star before text
</div>

<div class="ank-contentAfter-CDB→CDB ank-marginLeftAfter-5px">
  Arrow after text
</div>

<!-- Decorative elements -->
<div class="ank-position-relative ank-contentBefore-CDBCDB ank-positionBefore-absolute ank-topBefore-0 ank-leftBefore-0 ank-widthBefore-100per ank-heightBefore-2px ank-bgBefore-primary">
  Element with top border via ::before
</div>
```

### ::first-line and ::first-letter

```html
<!-- Drop cap effect -->
<p class="ank-fontSizeFirstLetter-18px ank-fontWeightFirstLetter-bold ank-colorFirstLetter-primary ank-floatFirstLetter-left ank-lineHeightFirstLetter-1 ank-paddingRightFirstLetter-5px">
  This paragraph has a styled first letter that stands out.
</p>

<!-- First line styling -->
<p class="ank-fontWeightFirstLine-bold ank-colorFirstLine-primary">
  The first line of this paragraph will be bold and colored,
  while the rest of the text maintains normal styling.
</p>
```

### ::placeholder

```html
<!-- Placeholder styling -->
<input placeholder="Enter text" class="ank-colorPlaceholder-gray-400 ank-fontStylePlaceholder-italic ank-opacityPlaceholder-0_7">

<textarea placeholder="Type message" class="ank-colorPlaceholder-blue-300 ank-fontSizePlaceholder-14px">
</textarea>
```

### ::selection

```html
<!-- Text selection styling -->
<div class="ank-bgSelection-blue ank-colorSelection-white">
  Select this text to see custom selection colors
</div>

<p class="ank-bgSelection-yellow-200 ank-colorSelection-black">
  This paragraph has yellow selection background
</p>
```

## Complete Pseudo-class List

Based on the source code, Angora CSS supports the following pseudo-classes (in camelCase):

### Basic Pseudo-classes
- `Active`, `Focus`, `Hover`, `Visited`, `Link`
- `Checked`, `Disabled`, `Enabled`, `Required`
- `Valid`, `Invalid`, `InRange`, `OutOfRange`

### Structural Pseudo-classes
- `FirstChild`, `LastChild`, `OnlyChild`
- `FirstOfType`, `LastOfType`, `OnlyOfType`
- `NthChild`, `NthLastChild`, `NthOfType`, `NthLastOfType`

### Language/Direction
- `Lang`, `Dir`

### Advanced Pseudo-classes
- `Has`, `Is`, `Not`, `Where`
- `Target`, `TargetWithin`
- `FocusVisible`, `FocusWithin`
- `UserValid`, `UserInvalid`

### Pseudo-elements
- `Before`, `After`
- `FirstLine`, `FirstLetter`
- `Placeholder`, `Selection`
- `Marker`, `Backdrop`

## Best Practices

### Syntax Guidelines

1. **Always use camelCase**: `colorHover`, not `color-hover`
2. **Use proper delimiters**: SD for `(`, ED for `)`, COM for `,`

### Example: Complete Interactive Button

```html
<button class="ank-bg-primary ank-color-white ank-p-12px__24px ank-border-none ank-borderRadius-6px ank-cursor-pointer ank-bgHover-primary-dark ank-transformHover-translateYSDMIN2pxED ank-boxShadowHover-0__4px__8px__rgbaSD0COM0COM0COM0_2ED ank-transformActive-translateYSD0ED ank-boxShadowFocus-0__0__0__3px__rgbaSD0COM123COM255COM0_25ED ank-opacityDisabled-0_5 ank-cursorDisabled-not-allowed">
  Complete Interactive Button
</button>
```

This comprehensive guide covers the correct usage of pseudo-classes and pseudo-elements in Angora CSS, ensuring accurate implementation based on the actual source code.
