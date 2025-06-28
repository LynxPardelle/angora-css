# propertyNValueCorrector - CSS Property-Value Correction and Enhancement Engine

## Overview

The `propertyNValueCorrector` function handles advanced CSS property-value correction, specializing in complex visual effects like gradient shadows, border gradients, and text gradients. It transforms standard CSS properties into sophisticated multi-layer effects using pseudo-elements and modern CSS techniques.

## Location

```
src/functions/main/private_utilities/propertyNValueCorrector.ts
```

## Dependencies

- `valuesSingleton.ts` - Global configuration and values
- `console_log.ts` - Comprehensive logging functionality
- `shadowGradientCreator.ts` - Advanced shadow effect generation

## Core Function

### propertyNValueCorrector()

```typescript
async propertyNValueCorrector(
  property2Use: string,
  value: string
): Promise<string>
```

Processes and corrects CSS property-value combinations, applying advanced transformations for gradient effects.

#### Parameters

- `property2Use: string` - The CSS property being processed
- `value: string` - The CSS value that may require correction or enhancement

#### Returns

- `Promise<string>` - Enhanced CSS rule string with corrections and effects applied

## Processing Categories

### 1. Box-Shadow Gradient Processing

**Trigger Condition**
```typescript
if (['box-shadow'].includes(property2Use) && value.includes('gradient'))
```

**Complex Shadow Analysis**
The function handles sophisticated shadow parsing using multiple regex patterns:

```typescript
let shadowRegex: RegExp =
  /(inset)?(\s?-?[0-9\.]+(?:(px)|(cm)|(mm)|(pt)|(in)|(pc)|(r?em)|(vmin)|(vh)|(vm(ax)?)|(%)|(vw))?\s?){2,4}(([A-z]+\-[A-z]+\([0-9\.]+(?:%|(deg)),\s*)?(((((?:(rgb)|(hsl))a?)\((([0-9]*)(%)?(deg)?,?\s?){1,4}(\/?\s?([0-9\.]*)(%)?\s?)\))|(#[0-9A-Fa-f]{3,8}))(\s*[0-9]*%,?\)?)?)*)(inset)?/g;

let onlyGradientRegex: RegExp =
  /(([A-z]+\-[A-z]+\([0-9\.]+(?:%|(deg)),\s*)?(((((?:(rgb)|(hsl))a?)\((([0-9]*)(%)?(deg)?,?\s?){1,4}(\/?\s?([0-9\.]*)(%)?\s?)\))|(#[0-9A-Fa-f]{3,8}))(\s*[0-9]*%,?\)?)?)*)/g;
```

**Pattern Components**
- **Inset Detection**: Identifies inset shadows
- **Dimensional Values**: Captures offset, blur, and spread values with units
- **Gradient Colors**: Matches complex gradient function syntax
- **Color Formats**: Supports RGB, HSL, hex, and named colors

**Processing Logic**
```typescript
let shadows2Use: string[] = [''];
const shadowMatches: RegExpMatchArray | null = value.match(shadowRegex);
const gradientMatches: RegExpMatchArray | null = value.match(onlyGradientRegex);

let onlyGradient: boolean = false;
if (!!shadowMatches && shadowMatches.every((a) => a.includes('gradient'))) {
  shadows2Use = shadowMatches.filter((a) => a !== '' && a.length > 2);
} else if (!!gradientMatches && gradientMatches.every((a) => a.includes('gradient'))) {
  shadows2Use = gradientMatches.filter((a) => a !== '' && a.length > 2);
  onlyGradient = true;
}
```

**Shadow Generation**
```typescript
let correctedShadows: string[] = await Promise.all(
  shadows2Use.map(async (a: string) => {
    return await shadowGradientCreator(a, onlyGradient);
  })
);
```

**Pseudo-Element Assembly**
```typescript
let add2NewRule: string = correctedShadows
  .map((a: string, i: number) => {
    if (i <= 1) {
      return `${values.separator}${values.specify}${
        i === 0 ? '::before' : '::after'
      }{${a}`;
    } else {
      return '';
    }
  })
  .join('');

newRule = `transform-style:preserve-3d;}${add2NewRule}`;
```

### 2. Background Gradient Processing

**Background-Color Gradients**
```typescript
['background-color', 'color'].includes(property2Use) && value.includes('gradient')
  ? 'background-image'
  : property2Use
```

**Transformation Logic**
- Converts `background-color` to `background-image` for gradient support
- Maintains compatibility with CSS gradient requirements

### 3. Text Gradient Effects

**Color Gradients**
```typescript
property2Use === 'color' && value.includes('gradient')
  ? `background-clip: text;background-size: 100%;-webkit-background-clip: text;-moz-background-clip: text;-webkit-text-fill-color: transparent;-moz-text-fill-color: transparent;`
  : ''
```

**Text Gradient Properties**
- **Background Clipping**: Clips background to text shape
- **Vendor Prefixes**: Ensures cross-browser compatibility
- **Text Transparency**: Makes text transparent to show background
- **Size Control**: Sets background size for proper rendering

### 4. Border Gradient Processing

**Border-Color Gradients**
```typescript
property2Use === 'border-color' && value.includes('gradient')
  ? `border-image-source`
  : property2Use
```

**Additional Properties**
```typescript
property2Use === 'border-color' && value.includes('gradient')
  ? `border-image-slice:2;border-image-width:2px;`
  : ''
```

**Border Image Configuration**
- **Source Conversion**: Changes property to `border-image-source`
- **Slice Settings**: Configures how gradient is sliced
- **Width Settings**: Sets border image width

## Usage Examples

### Box-Shadow with Gradient

```typescript
const result = await propertyNValueCorrector(
  'box-shadow',
  '5px 10px 15px linear-gradient(45deg, red, blue)'
);

// Result: Complex CSS with pseudo-elements:
// transform-style:preserve-3d;}
// ::before{content:" ";position:absolute;...}
```

### Text Gradient Effect

```typescript
const result = await propertyNValueCorrector(
  'color',
  'linear-gradient(90deg, #ff0000, #0000ff)'
);

// Result: 
// background-image:linear-gradient(90deg, #ff0000, #0000ff);
// background-clip: text;
// -webkit-background-clip: text;
// -webkit-text-fill-color: transparent;
// ...
```

### Border Gradient

```typescript
const result = await propertyNValueCorrector(
  'border-color',
  'conic-gradient(from 0deg, yellow, green, blue)'
);

// Result:
// border-image-source:conic-gradient(from 0deg, yellow, green, blue);
// border-image-slice:2;
// border-image-width:2px;
```

### Standard Property (No Correction)

```typescript
const result = await propertyNValueCorrector(
  'margin',
  '10px'
);

// Result: margin:10px;
```

## Advanced Shadow Processing

### Multi-Layer Shadows

- **Layer Limit**: Processes up to 2 shadow layers (::before and ::after)
- **Layer Assignment**: First shadow uses ::before, second uses ::after
- **Excess Handling**: Additional shadows beyond 2 are ignored

### 3D Transform Integration

- **Preserve-3D**: Enables 3D rendering context for layered effects
- **Z-Index Management**: Uses transform3d for proper layering
- **Perspective**: Maintains 3D perspective for complex effects

## Performance Considerations

### Regex Optimization

- **Compiled Patterns**: Complex regex patterns compiled once
- **Efficient Matching**: Specific patterns reduce backtracking
- **Conditional Processing**: Only processes when gradients detected

### Async Processing

- **Parallel Shadow Creation**: Uses Promise.all for concurrent processing
- **Non-blocking**: Doesn't block other CSS generation
- **Memory Efficiency**: Minimal memory allocation during processing

## Error Handling

### Graceful Fallbacks

- **Pattern Matching**: Continues if regex patterns fail
- **Shadow Processing**: Handles malformed shadow definitions
- **Logging Integration**: Comprehensive error logging for debugging

### Validation

- **Input Validation**: Validates property and value parameters
- **Format Checking**: Ensures gradient syntax compatibility
- **Output Validation**: Ensures valid CSS output

## Browser Compatibility

### Modern CSS Features

- **Background-Clip**: Text clipping support required
- **Border-Image**: Modern border gradient support
- **Transform-Style**: 3D rendering context support
- **Pseudo-Elements**: Standard pseudo-element support

### Vendor Prefixes

- **WebKit**: Comprehensive WebKit prefix support
- **Mozilla**: Firefox-specific prefixes included
- **Graceful Degradation**: Fallbacks for unsupported features

## Integration Points

### CSS Generation Pipeline

```
valueTraductor → propertyNValueCorrector → property2ValueJoiner
```

This function serves as the enhancement layer for complex CSS effects.

### Shadow System Integration

- **Shadow Creator**: Delegates complex shadow generation
- **Pseudo-Element Management**: Coordinates multiple shadow layers
- **Effect Composition**: Combines multiple visual effects

This function represents the most advanced CSS processing capability in the system, transforming simple gradient declarations into sophisticated multi-layer visual effects using modern CSS techniques and pseudo-element manipulation.
