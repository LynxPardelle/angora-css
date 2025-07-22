# Properties and Values Declaration in HTML Classes

## Overview

Angora CSS uses a powerful notation system that allows you to declare CSS properties and values directly in HTML class names. This guide will teach you the syntax and patterns for creating dynamic CSS using class-based declarations.

**Note**: Unlike ngx-bootstrap-expanded-features which uses the `bef` prefix, Angora CSS uses `ank` as the activator class prefix, which can be customized.

## Basic Syntax Pattern

The fundamental pattern for declaring CSS properties and values in Angora CSS follows this structure:

```
ank-property-value || ank-property-breakpoint-value || ank-property-value
```

### Key Differences from NGX-Bootstrap-Expanded-Features

- **Activator Class**: Angora CSS uses `ank` instead of `bef`
- **Fixed Prefix**: The `ank` prefix.
- **Service Name**: Uses `AngoraService` instead of `NgxBootstrapExpandedFeaturesService`

### Core Components

- **Property**: CSS property name (can be abbreviated)
- **Breakpoint** (optional): Responsive breakpoint prefix (sm, md, lg, xl, xxl)
- **Value**: CSS value (can be abbreviated or literal)

```html
<!-- Class usage -->
<div class="ank-color-red">Red text</div>
```

### Framework Integration Examples

#### Vanilla JavaScript/HTML

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="angora-styles.css">
    <script src="angora-css.js"></script>
</head>
<body>
    <div class="ank-p-20px ank-bg-primary">
        Angora CSS with vanilla HTML
    </div>
    
    <script>
        // Initialize Angora CSS
        const angoraService = new AngoraService();
        angoraService.cssCreate();
    </script>
</body>
</html>
```

#### Angular Integration

```typescript
// Component
import { Component } from '@angular/core';
import { AngoraService } from 'angora-css';

@Component({
  selector: 'app-example',
  template: `
    <div class="ank-bg-primary ank-color-white ank-p-20px">
      Angular with Angora CSS
    </div>
  `
})
export class ExampleComponent {
  constructor(private angoraService: AngoraService) {
    this.angoraService.cssCreate();
  }
}
```

#### React Integration

```jsx
import React, { useEffect } from 'react';
import { AngoraService } from 'angora-css';

function ExampleComponent() {
  const angoraService = new AngoraService();
  
  useEffect(() => {
    angoraService.cssCreate();
  }, []);
  
  return (
    <div className="ank-bg-primary ank-color-white ank-p-20px">
      React with Angora CSS
    </div>
  );
}
```

#### Vue Integration

```vue
<template>
  <div class="ank-bg-primary ank-color-white ank-p-20px">
    Vue with Angora CSS
  </div>
</template>

<script>
import { AngoraService } from 'angora-css';

export default {
  name: 'ExampleComponent',
  mounted() {
    const angoraService = new AngoraService();
    angoraService.cssCreate();
  }
}
</script>
```

## Simple Property-Value Declarations

### Margin and Padding

```html
<!-- Margin examples -->
<div class="ank-m-10px">Margin 10px on all sides</div>
<div class="ank-mt-20px">Margin-top 20px</div>
<div class="ank-ml-auto">Margin-left auto</div>
<div class="ank-mx-5px">Margin left and right 5px</div>

<!-- Padding examples -->
<div class="ank-p-15px">Padding 15px on all sides</div>
<div class="ank-pt-10px">Padding-top 10px</div>
<div class="ank-py-8px">Padding top and bottom 8px</div>
```

### Colors and Background

```html
<!-- Text colors -->
<div class="ank-color-red">Red text</div>
<div class="ank-color-primary">Primary color text</div>
<div class="ank-color-HASH007bff">Custom hex color (#007bff)</div>

<!-- Background colors -->
<div class="ank-backgroundColor-blue">Blue background</div>
<div class="ank-bg-success">Success background color</div>
<div class="ank-bg-gradient-primary">Gradient background</div>
```

### Typography

```html
<!-- Font sizes -->
<div class="ank-fontSize-16px">16px font size</div>
<div class="ank-fs-24px">24px font size</div>
<div class="ank-text-lg">Large text size</div>

<!-- Font weight and style -->
<div class="ank-fontWeight-bold">Bold text</div>
<div class="ank-fw-600">Font weight 600</div>
<div class="ank-textDecoration-underline">Underlined text</div>
```

### Layout and Positioning

```html
<!-- Display properties -->
<div class="ank-display-flex">Flexbox container</div>
<div class="ank-d-block">Block display</div>
<div class="ank-d-none">Hidden element</div>

<!-- Positioning -->
<div class="ank-position-relative">Relative position</div>
<div class="ank-pos-absolute">Absolute position</div>
<div class="ank-top-50px">Top position 50px</div>
```

## Value Types and Formats

### Numeric Values

```html
<!-- Pixels -->
<div class="ank-w-300px">Width: 300px</div>
<div class="ank-w-200px">Width: 200px</div>

<!-- Percentages -->
<div class="ank-h-100per">Height: 100%</div>
<div class="ank-w-50per">Width: 50%</div>

<!-- Em and Rem units -->
<div class="ank-fontSize-2em">Font size: 2em</div>
<div class="ank-p-1_5rem">Padding: 1.5rem</div>

<!-- Viewport units -->
<div class="ank-height-100vh">Height: 100vh</div>
<div class="ank-width-50vw">Width: 50vw</div>
```

### Color Values

```html
<!-- Named colors -->
<div class="ank-color-red">Named color</div>
<div class="ank-bg-primary">Bootstrap color</div>

<!-- Hex colors -->
<div class="ank-color-HASHff0000">Hex color</div>
<div class="ank-bg-HASH00ff00">Hex background</div>

<!-- RGB/RGBA -->
<div class="ank-color-rgbSD255COM0COM0ED">RGB color</div>
<div class="ank-bg-rgbaSD0COM255COM0COM0_5ED">RGBA background</div>

<!-- HSL colors -->
<div class="ank-color-hslSD120COM100perCOM50perED">HSL color</div>
```

### Special Values

```html
<!-- Auto values -->
<div class="ank-margin-auto">Auto margins</div>
<div class="ank-width-auto">Auto width</div>

<!-- Inherit and initial -->
<div class="ank-color-inherit">Inherited color</div>
<div class="ank-fontSize-initial">Initial font size</div>

<!-- None and unset -->
<div class="ank-border-none">No border</div>
<div class="ank-textDecoration-unset">Unset decoration</div>
```

## Advanced Value Patterns

### Multi-value Properties

```html
<!-- Border shorthand -->
<div class="ank-border-1px__solid__black">Border: 1px solid black</div>
<div class="ank-border-2px__dashed__red">Border: 2px dashed red</div>

<!-- Box shadow -->
<div class="ank-boxShadow-0__2px__4px__rgbaSD0COM0COM0COM0_1ED">Shadow effect</div>

<!-- Transform -->
<div class="ank-transform-translateSD10pxCOM20pxED">Transform translate</div>
<div class="ank-transform-rotateSD45degED">Rotate 45 degrees</div>
```

### Gradient Values

```html
<!-- Linear gradients -->
<div class="ank-bg-linearMINgradientSDto_rightCOMredCOMblueED">Linear gradient</div>
<div class="ank-bg-gradient-primary-secondary">Predefined gradient</div>

<!-- Radial gradients -->
<div class="ank-bg-radial-gradientSDcircleCOMredCOMblueED">Radial gradient</div>
```

### Custom Properties (CSS Variables)

```html
<!-- Using CSS custom properties -->
<div class="ank-color-varSDMINMINprimaryMINcolorED">CSS variable color</div>
<div class="ank-fontSize-varSDMINMINbaseMINfontMINsizeED">CSS variable size</div>
```

## Responsive Declarations

### Breakpoint Prefixes

```html
<!-- Mobile first approach -->
<div class="ank-p-10 ank-p-md-20 ank-p-lg-30">Responsive padding</div>
<div class="ank-fontSize-14px ank-fontSize-sm-16px ank-fontSize-lg-18px">Responsive text</div>

<!-- Specific breakpoints -->
<div class="ank-display-sm-block ank-display-md-flex ank-display-lg-grid">Responsive layout</div>
```

### Available Breakpoints

| Prefix | Breakpoint | Min Width |
|--------|------------|-----------|
| `xs:` | Extra Small | 0px |
| `sm:` | Small | 576px |
| `md:` | Medium | 768px |
| `lg:` | Large | 992px |
| `xl:` | Extra Large | 1200px |
| `xxl:` | XXL | 1400px |

## State-based Declarations

### Hover States

```html
<!-- Hover effects -->
<div class="ank-colorHover-blue">Blue color on hover</div>
<div class="ank-bgHover-red">Red background on hover</div>
<div class="ank-fontSizeHover-18px">Larger font on hover</div>
```

### Focus States

```html
<!-- Focus effects -->
<input class="ank-borderFocus-blue" placeholder="Focus border">
<button class="ank-bgFocus-primary">Focus background</button>
```

### Active States

```html
<!-- Active effects -->
<button class="ank-transformActive-scaleSD0_95ED">Scale on active</button>
<div class="ank-opacityActive-0_8">Opacity on active</div>
```

## Best Practices

### Naming Conventions

1. **Be consistent with units**: Stick to px, rem, or % consistently
2. **Use semantic color names**: `ank-color-primary` instead of `ank-color-blue`

### Performance Tips

1. **Group related properties**: Use combos for frequently used combinations
2. **Avoid overly complex values**: Break down complex declarations
3. **Use abbreviations wisely**: Balance brevity with readability

### Debugging

```html
<!-- Enable debug mode to see CSS generation -->
<script>
// In your JavaScript
angoraService.changeDebugOption(); // Toggle debug mode
</script>

<!-- Check console for detailed processing information -->
```

### Common Patterns

```html
<!-- Flexbox centering -->
<div class="ank-display-flex ank-justifyContent-center ank-alignItems-center">
  Centered content
</div>

<!-- Full height section -->
<div class="ank-minHeight-100vh ank-p-20px ank-bg-gray">
  Full height section
</div>

<!-- Responsive text -->
<h1 class="ank-fontSize-24px ank-fontSize-sm-32px ank-fontSize-lg-40px ank-fontWeight-bold">
  Responsive heading
</h1>
```

## Troubleshooting

### Common Issues

1. **Property not recognized**: Check spelling and use debug mode
2. **Value not applied**: Ensure proper value format and units
3. **Pseudo-class not working**: Verify pseudo-class syntax

### Debug Mode

Enable debug mode to see exactly how your classes are processed:

```javascript
// Enable debug logging
angoraService.changeDebugOption();

// Check generated CSS
console.log(angoraService.getGeneratedCSS());
```

This comprehensive guide covers the fundamentals of declaring CSS properties and values in HTML classes using Angora CSS. Practice with these examples and experiment with your own combinations to master the system!
