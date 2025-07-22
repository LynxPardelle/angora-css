# Methods Documentation for Angora CSS

Angora CSS provides a set of methods through the `AngoraService` to manage CSS classes, colors, breakpoints, and more. This guide covers all available methods and their usage.

## Table of Contents

1. [CSS Management](#css-management)
2. [Color Management](#color-management)
3. [Abbreviation Management](#abbreviation-management)
4. [Combo Management](#combo-management)
5. [Breakpoint Management](#breakpoint-management)
6. [Class Management](#class-management)
7. [Utility Methods](#utility-methods)
8. [Debug Options](#debug-options)

---

## CSS Management

### `cssCreate(configs?: Object)`

Creates CSS classes based on the provided configuration.

```typescript
angoraService.cssCreate({
  colors: ['primary', 'secondary'],
  breakpoints: ['xs', 'sm', 'md']
});
```

---

## Color Management

### `pushColors(colors: Object)`

Adds new colors to the color palette.

```typescript
angoraService.pushColors({
  'custom-blue': '#007bff',
  'custom-red': '#dc3545'
});
```

### `getColors()`

Returns all available colors.

```typescript
const colors = angoraService.getColors();
```

### `updateColor(colorName: string, colorValue: string)`

Updates an existing color.

```typescript
angoraService.updateColor('primary', '#new-color-value');
```

---

## Abbreviation Management

### `pushAbreviationsValues(abbreviations: Object)`

Adds new abbreviation values.

```typescript
angoraService.pushAbreviationsValues({
  'xlg': 'extra-large',
  'xsm': 'extra-small'
});
```

### `pushAbreviationsClasses(abbreviations: Object)`

Adds new abbreviation classes.

```typescript
angoraService.pushAbreviationsClasses({
  'btn': 'button',
  'nav': 'navigation'
});
```

### `getAbreviationsValues()`

Returns all abbreviation values.

```typescript
const values = angoraService.getAbreviationsValues();
```

### `getAbreviationsClasses()`

Returns all abbreviation classes.

```typescript
const classes = angoraService.getAbreviationsClasses();
```

### `updateAbreviationsValue(key: string, value: string)`

Updates an abbreviation value.

```typescript
angoraService.updateAbreviationsValue('lg', 'large-size');
```

### `updateAbreviationsClass(key: string, value: string)`

Updates an abbreviation class.

```typescript
angoraService.updateAbreviationsClass('btn', 'new-button-class');
```

---

## Combo Management

### `pushCombos(combos: Object)`

Adds new combos to the system.

```typescript
angoraService.pushCombos({
  'flex-center': {
    'display': 'flex',
    'justify-content': 'center',
    'align-items': 'center'
  }
});
```

---

## Breakpoint Management

### `getBPS()`

Returns all breakpoints.

```typescript
const breakpoints = angoraService.getBPS();
```

### `pushBPS(breakpoints: Object)`

Adds new breakpoints.

```typescript
angoraService.pushBPS({
  'xxl': 1400,
  'xxxl': 1600
});
```

---

## Class Management

### `getAlreadyCreatedClasses()`

Returns all already created classes.

```typescript
const createdClasses = angoraService.getAlreadyCreatedClasses();
```

### `updateClasses(classes: Object)`

Updates the classes configuration.

```typescript
angoraService.updateClasses({
  'margin': 'm',
  'padding': 'p'
});
```

---

## Utility Methods

### `getSheet()`

Returns the style sheet reference.

```typescript
const sheet = angoraService.getSheet();
```

### `cssValidToCamel(cssProperty: string)`

Converts CSS property to camelCase.

```typescript
const camelCase = angoraService.cssValidToCamel('background-color');
// Returns: 'backgroundColor'
```

### `camelToCSSValid(camelProperty: string)`

Converts camelCase property to CSS valid format.

```typescript
const cssFormat = angoraService.camelToCSSValid('backgroundColor');
// Returns: 'background-color'
```

### Color Transformation Methods

#### `convertToRGB(color: string)`

Converts color to RGB format.

```typescript
const rgb = angoraService.convertToRGB('#ff0000');
```

#### `convertToHEX(color: string)`

Converts color to HEX format.

```typescript
const hex = angoraService.convertToHEX('rgb(255, 0, 0)');
```

#### `convertToHSL(color: string)`

Converts color to HSL format.

```typescript
const hsl = angoraService.convertToHSL('#ff0000');
```

#### `lighten(color: string, amount: number)`

Lightens a color by the specified amount.

```typescript
const lightColor = angoraService.lighten('#ff0000', 0.2);
```

#### `darken(color: string, amount: number)`

Darkens a color by the specified amount.

```typescript
const darkColor = angoraService.darken('#ff0000', 0.2);
```

#### `saturate(color: string, amount: number)`

Saturates a color by the specified amount.

```typescript
const saturatedColor = angoraService.saturate('#ff0000', 0.2);
```

#### `desaturate(color: string, amount: number)`

Desaturates a color by the specified amount.

```typescript
const desaturatedColor = angoraService.desaturate('#ff0000', 0.2);
```

#### `grayscale(color: string)`

Converts a color to grayscale.

```typescript
const grayColor = angoraService.grayscale('#ff0000');
```

#### `complement(color: string)`

Returns the complement of a color.

```typescript
const complementColor = angoraService.complement('#ff0000');
```

#### `mix(color1: string, color2: string, weight?: number)`

Mixes two colors with optional weight.

```typescript
const mixedColor = angoraService.mix('#ff0000', '#0000ff', 0.5);
```

---

## Debug Options

### `changeDebugOption(option: string, value: any)`

Changes a debug option.

```typescript
angoraService.changeDebugOption('verbose', true);
```

### `setTimeBetweenReCreate(time: number)`

Sets the time between CSS recreation cycles.

```typescript
angoraService.setTimeBetweenReCreate(1000);
```

---

## Class Usage Examples

Here are practical examples of using these methods to create CSS classes:

### Basic Class Creation

```html
<!-- Creates: ank-text-primary -->
<div class="ank-text-primary">Primary text</div>

<!-- Creates: ank-bg-secondary -->
<div class="ank-bg-secondary">Secondary background</div>
```

### Color Management Example

```typescript
// Add custom colors
angoraService.pushColors({
  'brand-blue': '#1a73e8',
  'brand-green': '#34a853'
});

// Use in HTML
// Creates: ank-text-brand-blue
// <div class="ank-text-brand-blue">Brand colored text</div>
```

### Breakpoint Example

```typescript
// Add custom breakpoint
angoraService.pushBPS({
  'tablet': 768
});

// Use in HTML with breakpoint
// Creates: ank-tablet-text-center
// <div class="ank-tablet-text-center">Centered text on tablet</div>
```

---

## Best Practices

1. **Initialize Early**: Call configuration methods during application initialization
2. **Batch Updates**: Use batch methods when adding multiple items
3. **Performance**: Use `setTimeBetweenReCreate()` to optimize CSS regeneration
4. **Debug Mode**: Enable debug mode during development for better insights
5. **Naming Conventions**: Use consistent naming for custom colors and breakpoints
6. **Class Syntax**: Always use the `ank-property-value` format for CSS classes
