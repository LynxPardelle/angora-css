# Abbreviations System in Angora CSS

## Overview

The Abbreviations System in Angora CSS allows you to create custom shorthand notation for both CSS properties and values. This powerful feature enables faster development, improved readability, and consistent styling patterns across your projects.

## Understanding Abbreviations

### What are Abbreviations?

Abbreviations in Angora CSS are shorthand mappings that translate between:

- **Property abbreviations**: Short names that expand to full CSS property names
- **Value abbreviations**: Short values that expand to full CSS values
- **Bidirectional translation**: Convert from abbreviations to full forms and back

### Built-in Abbreviations

Angora CSS comes with many pre-configured abbreviations:


## Creating Custom Class Abbreviations

### Basic Class Abbreviations

```javascript
// Add class abbreviations
angoraService.pushAbreviationsClasses({
  'flexDir': 'ank-flexDirection',
  'justCon': 'ank-justifyContent',
  'alIte': 'ank-alignItems',
  'gridA': 'ank-gridArea'
});
```

### Using Custom Class Abbreviations

```html
<!-- Using the custom class abbreviations with Angora CSS -->
<div class="flexDir-column justCon-center ank-alIte-stretch">
  Flex container with custom abbreviations
</div>

<div class="ank-gridTemplateColumns-repeatSD3COM1frED ank-gridA-main ank-placeItems-center">
  Grid with custom abbreviations
</div>

<h1 class="ank-fontFamily-serif ank-lineHeight-1_2 ank-letterSpacing-2px ank-textTransform-uppercase">
  Typography with custom abbreviations
</h1>
```

## Creating Custom Value Abbreviations


### Complex Value Abbreviations

```javascript
// Advanced value patterns
angoraService.pushAbreviationsValues({
  // Animation values
  'fastTransition': '0_15s__easeMINinMINout',
  'normalTransition': '0_3s__easeMINinMINout',
  'slowTransition': '0:5s__easeMINinMINout',
  
  // Shadow values
  'lightShadow': '0__2px__4px__rgba(0COM0COM0COM0_1ED',
  'mediumShadow': '0__4px__8px__rgba(0COM0COM0COM0_15ED',
  'darkShadow': '0__8px__16px__rgbaSD0COM0COM0COM0_2ED',
  
  // Font families
  'sansSerif': 'system-uiCOM__MINappleMINsystemCOM__sansMINserif',
  'serif': 'GeorgiaCOM__CDBTimes__New__RomanCDBCOM__serif',
  'mono': 'CDBConsolasCDBCOM__CDBMonacoCDBCOM__monospace',
  
  // Layout values
  'fullWidth': '100per',
  'fullHeight': '100vh',
  'fullScreen': '100vw',
  'containerMax': '1200px'
});
```

### Using Custom Value Abbreviations

```html
<!-- Using custom value abbreviations with Angora CSS -->
<div class="ank-padding-1rem ank-margin-1rem ank-maxWidth-containerMax">
  Container with custom spacing
</div>

<div class="ank-boxShadow-mediumShadow ank-transition-normalTransition">
  Card with custom shadow and transition
</div>

<h1 class="ank-fontFamily-sansSerif ank-fontSize-2rem ank-lineHeight-1_2">
  Text with custom font family
</h1>

<div class="ank-width-fullWidth ank-height-fullHeight ank-bg-primary">
  Full viewport element
</div>
```

## Combining Property and Value Abbreviations

### Complete Abbreviation Patterns

```javascript
// Create comprehensive abbreviation system
angoraService.pushAbreviationsClasses({
  // Layout system
  'flex': 'ank-display-flex',
  'flexCol': 'ank-flexDirection-column',
  'flexRow': 'ank-flexDirection-row',
  'flexWrap': 'ank-flexWrap-wrap',
  
  // Grid system  
  'grid': 'ank-display-grid',
  'gridCols2': 'ank-gridTemplateColumns-repeatSD2COM__1frED',
  'gridCols3': 'ank-gridTemplateColumns-repeatSD3COM__1frED',
  'gridCols4': 'ank-gridTemplateColumns-repeatSD4COM__1frED',
});
```

### Advanced Pattern Usage

```html
<!-- Using combined abbreviation patterns with Angora CSS -->
<div class="flex ank-padding-1rem">
  Centered flex container
</div>

<div class="grid gridCols3 ank-gap-l">
  <div class="ank-background-white ank-padding-1rem ank-borderRadius-1rem ank-boxShadow-lightShadow">
    Grid item 1
  </div>
  <div class="ank-background-white ank-padding-1rem ank-borderRadius-1rem ank-boxShadow-lightShadow">
    Grid item 2  
  </div>
  <div class="ank-background-white ank-padding-1rem ank-borderRadius-1rem ank-boxShadow-lightShadow">
    Grid item 3
  </div>
</div>
```

## Responsive Abbreviations

### Breakpoint-Specific Abbreviations

Angora CSS handles responsive behavior through its built-in breakpoint system. You can create value abbreviations that work with the library's responsive classes:

```javascript
// Create responsive value abbreviations
angoraService.pushAbreviationsValues({
  // Spacing values
  'spaceSmall': '16px',
  'spaceMedium': '24px', 
  'spaceLarge': '32px',
  
  // Typography values
  'textSmall': '16px',
  'textMedium': '18px',
  'textLarge': '20px',
  
  // Container values
  'containerFluid': '100per',
  'containerMd': '768px',
  'containerLg': '1200px'
});
```

### Using Responsive Abbreviations

```html
<!-- Responsive design with abbreviations using Angora CSS -->
<div class="ank-maxWidth-containerFluid ank-maxWidth-md-containerMd ank-maxWidth-lg-containerLg ank-margin-auto">
  <h1 class="ank-fontSize-textSmall ank-fontSize-md-textMedium ank-fontSize-lg-textLarge ank-fontWeight-bold">
    Responsive heading
  </h1>
  
  <div class="ank-padding-spaceSmall ank-padding-md-spaceMedium ank-padding-lg-spaceLarge ank-background-white ank-borderRadius-1rem">
    Responsive content container
  </div>
</div>
```


## Managing Abbreviations

### Getting Current Abbreviations

```javascript
// Get all current abbreviations
const classAbbreviations = angoraService.getAbreviationsClasses();
const valueAbbreviations = angoraService.getAbreviationsValues();

console.log('Class abbreviations:', classAbbreviations);
console.log('Value abbreviations:', valueAbbreviations);
```

### Updating Abbreviations

```javascript
// Update existing abbreviations
angoraService.updateAbreviationsClass('flexCol', 'ank-flexDirection-column-reverse');
angoraService.updateAbreviationsValue('spaceSmall', '12px');
```

### Abbreviation Validation

```javascript
// Check against built-in values before adding custom abbreviations
function isAbbreviationSafe(name) {
  const colors = angoraService.getColors();
  const breakpoints = ['sm', 'md', 'lg', 'xl', 'xxl'];
  const commonValues = Object.keys(angoraService.commonPropertiesValuesAbreviations || {});
  
  // Check against reserved words
  return !colors[name] && 
         !breakpoints.includes(name) && 
         !commonValues.includes(name);
}

// Validate before adding
const newAbbr = 'customProp';
if (isAbbreviationSafe(newAbbr)) {
  angoraService.pushAbreviationsValues({
    [newAbbr]: 'custom-css-value'
  });
} else {
  console.warn(`${newAbbr} conflicts with existing values`);
}
```

## Best Practices

### Naming Conventions

#### 1. Use Clear, Descriptive Names

```javascript
// ✅ Good abbreviation names
angoraService.pushAbreviationsValues({
  'textCenter': 'text-align: center',
  'flexCenter': 'display: flex; justify-content: center; align-items: center',
  'borderRadius': 'border-radius: 8px',
  'shadowLight': '0 2px 4px rgba(0,0,0,0.1)'
});

// ❌ Avoid unclear abbreviations
angoraService.pushAbreviationsValues({
  'tc': 'text-align: center',  // Too cryptic
  'x': 'some-property',        // Non-descriptive
  'thing': 'border-radius'     // Vague naming
});
```

#### 2. Follow Consistent Patterns

```javascript
// ✅ Consistent naming patterns
angoraService.pushAbreviationsValues({
  // Size pattern
  'spaceXs': '4px',
  'spaceSm': '8px',
  'spaceMd': '16px',
  'spaceLg': '24px',
  'spaceXl': '32px',
  
  // Shadow pattern
  'shadowNone': 'none',
  'shadowSm': '0 1px 2px rgba(0,0,0,0.05)',
  'shadowMd': '0 4px 6px rgba(0,0,0,0.1)',
  'shadowLg': '0 10px 15px rgba(0,0,0,0.15)',
  
  // Border radius pattern
  'roundedNone': '0',
  'roundedSm': '4px',
  'roundedMd': '8px',
  'roundedLg': '12px',
  'roundedFull': '50%'
});
```

#### 3. Avoid Conflicts

```javascript
// Always check against reserved words before adding
const proposedAbbreviations = {
  'primary': 'some-property',  // ❌ Conflicts with color name
  'hover': 'some-property',    // ❌ Conflicts with pseudo-class
  'sm': 'some-property'        // ❌ Conflicts with breakpoint
};

// ✅ Use safe, non-conflicting names
const safeAbbreviations = {
  'primaryButton': 'some-property',
  'hoverEffect': 'some-property',
  'smallMargin': 'some-property'
};
```

### Performance Considerations

#### 1. Group Related Abbreviations

```javascript
// Add related abbreviations together for better performance
angoraService.pushAbreviationsValues({
  // Layout group
  'flexCol': 'flex-direction: column',
  'flexRow': 'flex-direction: row',
  'flexCenter': 'justify-content: center; align-items: center',
  'flexBetween': 'justify-content: space-between; align-items: center',
  
  // Spacing group
  'p0': 'padding: 0',
  'p1': 'padding: 4px',
  'p2': 'padding: 8px',
  'p3': 'padding: 12px',
  'p4': 'padding: 16px'
});
```

#### 2. Use Efficient Values

```javascript
// ✅ Efficient abbreviation values
angoraService.pushAbreviationsValues({
  'hidden': 'display: none',                    // Direct property
  'block': 'display: block',                    // Single property
  'textCenter': 'text-align: center'            // Clear mapping
});

// ❌ Avoid overly complex values
angoraService.pushAbreviationsValues({
  'complexLayout': 'display: grid; grid-template-columns: repeat(12, 1fr); gap: 16px; padding: 24px; margin: 0 auto; max-width: 1200px' // Too complex
});
```

## Testing and Debugging Abbreviations

### Debug Mode

```javascript
// Enable debug mode to see abbreviation processing
angoraService.changeDebugOption();

// Test abbreviation expansion
console.log('Testing abbreviation expansion...');
```

### Validate Abbreviations

```html
<!-- Test your abbreviations with Angora CSS -->
<div class="ank-flexCenter ank-padding-xl ank-background-brandPrimary ank-color-white ank-borderRadius-m">
  <h1 class="ank-fontSize-title1 ank-marginBottom-m">Test Abbreviations</h1>
  <p class="ank-fontSize-bodyMedium">Check console for processing details</p>
</div>
```

### Common Issues

1. **Abbreviation not recognized**: Check spelling and ensure it's added to the system
2. **Conflict warnings**: Verify abbreviation names don't conflict with reserved words
3. **CSS not generated**: Enable debug mode to see processing details

## Advanced Abbreviation Techniques

### Component-Based Abbreviations

Create reusable abbreviations for common UI patterns:

```javascript
// Create abbreviations for common components
angoraService.pushAbreviationsValues({
  // Button components
  'btnBase': 'padding: 12px 24px; border: none; border-radius: 6px; cursor: pointer; font-weight: 600',
  'btnPrimary': 'background: #007bff; color: white',
  'btnSecondary': 'background: #6c757d; color: white',
  
  // Card components
  'cardBase': 'background: white; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); padding: 24px',
  'cardHover': 'transform: translateY(-2px); box-shadow: 0 4px 8px rgba(0,0,0,0.15)',
  
  // Form components
  'inputBase': 'padding: 12px 16px; border: 1px solid #d1d5db; border-radius: 6px; font-size: 16px',
  'inputFocus': 'border-color: #007bff; outline: none; box-shadow: 0 0 0 3px rgba(0,123,255,0.25)'
});
```

### Usage Examples

```html
<!-- Using component abbreviations -->
<div class="ank-cardBase ank-cardHover-hover">
  <h3 class="ank-marginBottom-16px">Card Title</h3>
  <input class="ank-inputBase ank-inputFocus-focus" type="text" placeholder="Enter text">
  <button class="ank-btnBase ank-btnPrimary">Submit</button>
</div>
```

### Dynamic Abbreviations

Generate abbreviations programmatically:

```javascript
// Generate spacing abbreviations
function generateSpacingAbbreviations() {
  const spacing = {};
  const sizes = [0, 4, 8, 12, 16, 20, 24, 32, 40, 48];
  
  sizes.forEach((size, index) => {
    spacing[`space${index}`] = `${size}px`;
  });
  
  return spacing;
}

angoraService.pushAbreviationsValues(generateSpacingAbbreviations());
```

The Abbreviations System in Angora CSS provides powerful tools for creating efficient, maintainable, and scalable styling solutions. Use these patterns to build consistent design systems and speed up your development workflow!
