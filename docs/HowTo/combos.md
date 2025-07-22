# Combos System in Angora CSS

## Overview

The Combos System in Angora CSS allows you to create single class names that generate multiple CSS rules automatically. This powerful feature enables you to define reusable style combinations that expand into complete styling patterns, making your HTML cleaner and your CSS more maintainable.

## Understanding Combos

### What are Combos?

Combos are special class names that expand into multiple CSS classes automatically. When you use a combo class, Angora CSS:

1. **Recognizes the combo**: Identifies the combo pattern in your class name
2. **Expands the combo**: Converts it into multiple individual CSS classes
3. **Generates CSS**: Creates CSS rules for each expanded class
4. **Applies styling**: All styles are applied to the element

### Basic Combo Syntax

```html
<!-- Instead of writing multiple classes with Angora CSS -->
<button class="ank-bg-primary ank-color-white ank-p-10px_20px ank-border-none ank-borderRadius-5px ank-cursor-pointer">
  Traditional approach
</button>

<!-- Use a combo for the same result with Angora CSS -->
<button class="ank-btn-primary">
  Combo approach (expands to multiple classes)
</button>
```

## Creating Basic Combos

### Adding Simple Combos

```javascript
// Create a card combo
angoraService.pushCombos({
  'cardBase': 'ank-bg-white ank-borderRadius-8px ank-boxShadow-0__2px__4px__rgbaSD0COM0COM0COM0_1ED ank-p-20px'
});

// Create a flex center combo
angoraService.pushCombos({
  'flexCenter': 'ank-display-flex ank-justifyContent-center ank-alignItems-center'
});
```

### Using Basic Combos

```html
<!-- Card using combo with Angora CSS -->
<div class="cardBase">
  <h3>Card Title</h3>
  <p>Card content goes here.</p>
</div>

<!-- Flex container using combo with Angora CSS -->
<div class="flexCenter ank-minHeight-100vh">
  <div>Centered content</div>
</div>
```

## Advanced Combo Patterns

### Array-Based Combos

Combos can be defined as arrays of class strings, which provides better organization and readability:

```javascript
// Complex layout combo
angoraService.pushCombos({
  'grid-layout': [
    'ank-display-grid ank-gridTemplateColumns-repeatSDautoMINfitCOMminmaxSD300pxCOM1frEDED',
    'ank-gap-20px ank-p-20px',
    'ank-gridTemplateColumns-sm-repeatSD2COM1frED',
    'gridTemplateColumns-lg-repeatSD3COM1frED'
  ]
});
```

## Variable Values System (VAL/DEF Pattern)

One of the most powerful features of Angora CSS combos is the ability to create combos with variable values using the VAL/DEF pattern.

### Understanding VAL/DEF

- `VAL1`, `VAL2`, etc. - Define placeholder variables
- `DEF` - Define default values: `VAL1DEFdefaultValueDEF`

### Creating Variable Combos

```javascript
// Combo with variable values and defaults
angoraService.pushCombos({
  'customBox': [
    'ank-w-VAL1DEF85perDEF',
    'ank-border-VAL2DEF1px__solid__darkDEF',
    'ank-bg-VAL3DEFsuccessDEF',
    'ank-text-VAL4DEFaquaDEF',
    'ank-p-VAL5DEF1_5remDEF'
  ]
});

// Button combo with customizable theme
angoraService.pushCombos({
  'themeButton': [
    'ank-bg-VAL1DEFprimaryDEF color-VAL2DEFwhiteDEF',
    'ank-p-VAL3DEF10px_20pxDEF',
    'ank-border-none borderRadius-VAL4DEF5pxDEF',
    'ank-cursor-pointer'
  ]
});
```

### Using Variable Combos

```html
<!-- Use default values -->
<div class="customBox">Default styling</div>

<!-- Override specific values using VALSVL notation -->
<div class="customBoxVALSVL75perVL3px__dashed__grayVLtealVLbeastVL2rem">
  Custom styling with values: 75%, 3px dashed gray border, teal background, beast text color, 2rem padding
</div>

<!-- Button with custom theme -->
<button class="themeButtonVALSVLredVLblackVL15px_30pxVL10px">
  Custom button: red background, black text, larger padding, more border radius
</button>
```

### Complex Example from NGX-Bootstrap-Expanded-Features

Based on the sibling library, here's a complex combo example:

```javascript
angoraService.pushCombos({
  'cardBootstrapLike': [
    // Card container
    'maxWidth-VAL1DEF18remDEF bg-VAL2DEFtransparentDEF pos-relative d-flex flexDirection-column border-1px__solid__rgbaSD255COM255COM255COM0_15ED backgroundClip-borderMINbox wordWrap-breakMINword rounded-0_375rem m-VAL3DEF1remDEF__auto text-VAL4DEFwhiteDEF',
    // Card Body
    'flexSELCHILDdiv-1__1__auto pSELCHILDdiv-1rem',
    // Card Title
    'mbSEL__h2COM_cardBootstrapLike__h3COM_cardBootstrapLike__h4COM_cardBootstrapLike__h5COM_cardBootstrapLike__h6-0_5rem',
    // Card Text
    'mtSEL__p-0 mbSEL__p-1rem dSEL__p-block',
    // Card Link
    'dSEL__a-inlineMINblock fwSEL__a-400 lhSEL__a-1_5 taSEL__a-center tdeSEL__a-none verticalAlignSEL__a-middle cursorSEL__a-pointer userSelectSEL__a-none pSEL__a-0_375rem__0_75rem roundedSEL__a-0_25rem transitionSEL__a-color___15s__easeMINinMINoutCOMbackgroundMINcolor___15s__easeMINinMINoutCOMborderMINcolor___15s__easeMINinMINoutCOMboxMINchadow___15s__easeMINinMINout btnOutlineSEL__a-primary-lavender'
  ]
});
```

## Managing Combos

### Available Methods

Angora CSS provides these methods for combo management:

#### `pushCombos(combos: Object)`

Adds new combos to the system.

```javascript
angoraService.pushCombos({
  'btn-primary': 'bg-primary color-white p-10px_20px border-none borderRadius-5px cursor-pointer',
  'btn-secondary': 'bg-secondary color-white p-10px_20px border-none borderRadius-5px cursor-pointer'
});
```

#### `getCombos()`

Returns all current combos.

```javascript
const combos = angoraService.getCombos();
console.log('Available combos:', combos);
```

#### `updateCombo(comboName: string, newValues: string[])`

Updates an existing combo.

```javascript
angoraService.updateCombo('btn-primary', [
  'bg-blue-600 color-white p-12px_24px',
  'border-none borderRadius-8px cursor-pointer'
]);
```

## Implementation Examples

### For CDN Version

```html
<script>
  var combos = {
    boxOne: [
      'ank-w-85per ank-border-1px__solid__dark ank-bg-success ank-text-aqua ank-p-1_5rem',
    ],
    boxCustom: [
      'ank-w-VAL1','ank-border-VAL2','ank-bg-VAL3','ank-text-VAL4','ank-p-VAL5',
    ],
  };
  pushCombos(combos);
</script>
```

### For NPM Version

```javascript
import { cssCreate, pushCombos } from "angora-css";

const combos = {
  boxOne: [
    'ank-w-85per ank-border-1px__solid__dark ank-bg-success ank-text-aqua ank-p-1_5rem',
  ],
  boxCustom: [
    'ank-w-VAL1','ank-border-VAL2','ank-bg-VAL3','ank-text-VAL4','ank-p-VAL5',
  ],
};

pushCombos(combos);
cssCreate();
```

### For Angular/Framework Integration

```typescript
import { AngoraService } from 'angora-css';

export class YourComponent {
  public combos = {
    boxOne: [
      'ank-w-85per ank-border-1px__solid__dark ank-bg-success ank-text-aqua ank-p-1_5rem',
    ],
    boxCustom: [
      'ank-w-VAL1','ank-border-VAL2','ank-bg-VAL3','ank-text-VAL4','ank-p-VAL5',
    ],
  };

  constructor(private angoraService: AngoraService) {
    this.angoraService.pushCombos(this.combos);
    this.angoraService.cssCreate();
  }
}
```

## Best Practices

### Naming Conventions

1. **Use Descriptive Names**: Choose combo names that clearly describe their purpose
   ```javascript
   // ✅ Good
   'btn-primary', 'card-product', 'nav-mobile'
   
   // ❌ Avoid
   'thing1', 'x', 'combo123'
   ```

2. **Follow Consistent Patterns**: Use consistent naming schemes across your project
   ```javascript
   'btn-primary', 'btn-secondary', 'btn-danger'  // Component-state pattern
   'layout-header', 'layout-sidebar'             // Layout-purpose pattern
   ```

### Organization Strategies

1. **Group Related Combos**: Organize combos by component type or functionality

2. **Use Progressive Enhancement**: Build complex combos on simpler base combos

3. **Leverage Arrays**: Use array structure for better readability and maintenance

### Performance Optimization

1. **Efficient Structure**: Organize combo properties logically (visual → layout → typography → interactive)

2. **Reusable Patterns**: Create base patterns that can be extended

3. **Minimal Complexity**: Avoid overly complex single-string combos in favor of organized arrays

## Usage Examples

### Basic Example

```html
<p class="ank-boxOne">
  Box with combo classes.
</p>
```

### Variable Example

```html
<p class="ank-boxCustomVALSVL75perVL3px__dashed__grayVLtealVLbeastVL2rem">
  Box with custom variable values.
</p>
```

### Complex Card Example

```html
<div class="ank-cardBootstrapLikeVALSVAL2NblackVAL2NVL75perVLVAL1">
  <div>
    <h5>Card Component</h5>
    <p>
      You can see my portfolio in the link below.
      <br/>
      If you want to see more about me, you can visit my portfolio.
      <br/>
      Check it out!
    </p>
    <a href="https://lynxpardelle.com" target="_blank" rel="noopener noreferrer">
      Visit my portfolio
    </a>
  </div>
</div>
```

The Combos System in Angora CSS provides a powerful way to create reusable, maintainable styling patterns that keep your HTML clean and your CSS organized while supporting advanced features like variable values and complex nested structures.
