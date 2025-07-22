# btnCreator.ts

## Overview

Private utility function that generates comprehensive CSS rules for button components with multiple states (default, hover, focus, active) and variants (filled, outline). This function creates Bootstrap-compatible button styles with advanced color management, shadow effects, and state-based styling.

## Purpose

- Generate complete button CSS rule sets with all interactive states
- Support both filled and outline button variants
- Apply automatic color shading and tinting for state variations
- Create Bootstrap-compatible button classes with proper selectors
- Handle complex box-shadow effects for focus and active states

## Core Functionality

### btnCreator(class2Create, specify, value, secondValue?, outline?): Promise<string>

**Parameters:**
- `class2Create`: Base class name for the button
- `specify`: CSS selector template with placeholder
- `value`: Primary color value for the button
- `secondValue`: Secondary color value (default: "transparent")
- `outline`: Boolean flag for outline variant (default: false)

**Returns:** Promise resolving to CSS rule string

**Purpose:** Creates comprehensive button CSS with all interactive states and proper color variations.

## Button Generation Process

### 1. Color Shade Generation

**Shade Creation:**
```typescript
const combinatorsValuesNumbers = combinators.combineArrays<TNameVal, number, TNameValNumber>(
  { name: "val", array: [{ name: "value", val: value }, { name: "secondValue", val: secondValue }] },
  { name: "number", array: [-15, -20, -25, 3] }
);
```

**Shade Processing:**
- Generates color variations using percentages: -15%, -20%, -25%, +3%
- Creates darker shades for hover and active states
- Applies shading to both primary and secondary colors
- Uses `color_transform.getShadeTintColorOrGradient()` for color manipulation

### 2. Shadow Effect Creation

**Shadow Preparation:**
```typescript
let shadowColorValue = color_transform.opacityCreator(shades["value,3"], 0.5);
const shadowNumericalValues = "0 0 0 0.25rem ";
```

**Shadow Features:**
- Creates semi-transparent shadow colors with 50% opacity
- Uses 0.25rem blur radius for focus effects
- Applies shadows to focus and active states
- Supports both primary and secondary shadow colors

### 3. Property-Value Correction

**Correction Process:**
- Applies `propertyNValueCorrector()` to all CSS property-value pairs
- Ensures valid CSS syntax and proper value formatting
- Handles color format conversions and validations
- Processes both color and shadow properties

### 4. CSS Rule Generation

**Rule Types Generated:**

**Basic Button:**
```css
.btn-primary { background-color: #007bff; border-color: #007bff; }
```

**Hover State:**
```css
.btn-primary:hover { background-color: #0056b3; border-color: #004085; }
```

**Focus State (Outline Only):**
```css
.btn-check:focus + .btn-outline-primary, .btn-outline-primary:focus { ... }
```

**Active/Checked State:**
```css
.btn-check:checked + .btn-primary, .btn-primary:active { ... }
```

## Button Variants

### Filled Buttons
- Primary color background and border
- Darker shades for hover/active states
- Box-shadow on focus and active states
- Standard Bootstrap button behavior

### Outline Buttons
- Transparent background with colored border and text
- Filled background on hover with primary color
- Enhanced focus states with background color changes
- Modified active state styling

## State Management

### Interactive States

**Default State:**
- Base colors applied according to variant type
- Primary color for background (filled) or border/text (outline)

**Hover State:**
- Slightly darker shade of primary color
- Maintains visual hierarchy and accessibility

**Focus State:**
- Box-shadow effect for keyboard navigation
- Enhanced visual feedback for accessibility
- Outline variant gets background color on focus

**Active/Checked State:**
- Darkest shade for pressed appearance
- Box-shadow for depth effect
- Supports Bootstrap's button groups and toggles

## Dependencies

- `ValuesSingleton` - Global state and configuration
- `color_transform` - Color manipulation and shade generation
- `console_log` - Debug logging
- `combinators` - Array and object combination utilities
- `propertyNValueCorrector` - CSS property-value validation
- Private types: `TNameVal`, `TNameValNumber`, `TNameValProp`

## Integration Points

### With Color System
- Uses advanced color transformation for shade generation
- Integrates with opacity creation for shadow effects
- Supports gradient and complex color value processing

### With CSS Generation Pipeline
- Generates CSS rules compatible with main generation system
- Uses global separator for rule joining
- Integrates with property correction system

### With Bootstrap Compatibility
- Generates Bootstrap-compatible selectors and structure
- Supports button groups, dropdowns, and form controls
- Maintains Bootstrap's button behavior patterns

## Performance Considerations

### Asynchronous Processing
- Uses `Promise.all()` for parallel color processing
- Optimizes shade generation with concurrent operations
- Efficient property correction processing

### Memory Efficiency
- Reuses computed shade values across states
- Minimizes color transformation calls
- Efficient object creation and combination

## Error Handling

### Robust Processing
- Handles invalid color values gracefully
- Filters empty CSS rules before output
- Continues processing despite individual failures

### Debug Support
- Comprehensive logging throughout the process
- Logs intermediate results for troubleshooting
- Provides visibility into color transformation steps

## Usage Context

### Button Generation
```javascript
// Generate primary button CSS
const primaryBtn = await btnCreator(
  'btn-primary',
  '.btn-primary',
  '#007bff',
  'transparent',
  false
);

// Generate outline button CSS
const outlineBtn = await btnCreator(
  'btn-outline-secondary',
  '.btn-outline-secondary',
  '#6c757d',
  'transparent',
  true
);
```

### Integration with CSS Generation
- Called during CSS class creation for button classes
- Generates complete button styling in single operation
- Provides Bootstrap-compatible button implementations

## Advanced Features

### Color Management
- Automatic shade generation for consistent color scheme
- Support for gradients and complex color values
- Intelligent opacity handling for shadow effects

### Selector Complexity
- Supports complex Bootstrap selectors for button groups
- Handles checkbox and radio button integration
- Manages dropdown toggle states

### Accessibility
- Proper focus indicators with box-shadows
- Maintains color contrast ratios through shading
- Keyboard navigation support through focus states

## Notes

- Essential for Bootstrap-compatible button generation
- Handles complex button state management automatically
- Provides comprehensive styling for all interactive states
- Optimized for performance with asynchronous processing
- Integrates seamlessly with the library's color system
- Supports both filled and outline button variants
- Maintains Bootstrap's accessibility standards
