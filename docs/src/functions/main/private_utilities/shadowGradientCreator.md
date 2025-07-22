# shadowGradientCreator - Advanced Shadow and Gradient CSS Generator

## Overview

The `shadowGradientCreator` function generates complex CSS for creating shadow effects using gradients and pseudo-elements. It handles both traditional box-shadows with gradient colors and pure gradient effects, creating sophisticated visual effects through CSS transforms and clip-path techniques.

## Location

```
src/functions/main/private_utilities/shadowGradientCreator.ts
```

## Dependencies

- `console_log.ts` - Logging functionality for debugging

## Core Function

### shadowGradientCreator()

```typescript
async shadowGradientCreator(
  shadow: string,
  onlyGradient: boolean = false
): Promise<string>
```

Generates CSS for pseudo-element-based shadow effects with gradient colors.

#### Parameters

- `shadow: string` - Shadow definition string containing offset, blur, spread, and color information
- `onlyGradient: boolean` - Flag indicating whether to process only gradient color (default: false)

#### Returns

- `Promise<string>` - Complete CSS property string for pseudo-element shadow effect

## Processing Logic

### Default Shadow Parameters

```typescript
let hOffset: string = `0`;      // Horizontal offset
let vOffset: string = `0`;      // Vertical offset  
let blur: string = `5`;         // Blur radius
let spread: string = `5`;       // Spread distance
let color: string = `black`;    // Shadow color
let inset: boolean = false;     // Inset shadow flag
```

### Shadow Value Parsing

When `onlyGradient` is false, the function parses traditional shadow syntax:

```typescript
let numericalValuesRegex: RegExp =
  /(?<![\(#]+)^(inset)?(\s?-?[0-9\.]+(?:(px)|(cm)|(mm)|(pt)|(in)|(pc)|(r?em)|(vmin)|(vh)|(vm(ax)?)|(%)|(vw))?\s?){2,4}/g;
```

**Regex Pattern Breakdown**
- **Negative Lookbehind**: `(?<![\(#]+)` - Excludes values inside functions or hex colors
- **Inset Detection**: `(inset)?` - Optional inset keyword
- **Numerical Values**: Captures 2-4 numerical values with optional units
- **Unit Support**: Supports px, rem, em, vh, vw, %, and other CSS units

**Value Extraction Logic**
```typescript
if (!!numericalValuesMatches) {
  color = shadow.replace(numericalValuesRegex, '');
  let numericalValuesSplit: string[] = shadow.replace(color, '').split(' ');
  
  if (numericalValuesSplit[0] === 'inset') {
    inset = true;
    numericalValuesSplit.shift();
  }
  
  // Assign positional values
  hOffset = numericalValuesSplit[0] || '0';
  vOffset = numericalValuesSplit[1] || '0';
  blur = numericalValuesSplit[3] || '0';      // Note: index 3 for blur
  spread = numericalValuesSplit[2] || '5';    // Note: index 2 for spread
}
```

### CSS Generation

The function generates complex CSS using pseudo-elements and modern CSS features:

```typescript
return `content:" ";border-radius:inherit;position:absolute;inset:-${spread};transform:translate3d(${hOffset},${vOffset},-1);background:${color};filter:blur(${blur});clip-path: polygon(-100vmax -100vmax,100vmax -100vmax,100vmax 100vmax,-100vmax 100vmax,-100vmax -100vmax,calc(0px  + ${spread} - ${hOffset}) calc(0px  + ${spread} - ${vOffset}),calc(0px  + ${spread} - ${hOffset}) calc(100% - ${spread} - ${vOffset}),calc(100% - ${spread} - ${hOffset}) calc(100% - ${spread} - ${vOffset}),calc(100% - ${spread} - ${hOffset}) calc(0px  + ${spread} - ${vOffset}),calc(0px  + ${spread} - ${hOffset}) calc(0px  + ${spread} - ${vOffset})`;
```

**CSS Properties Generated**

- **`content: " "`** - Creates pseudo-element content
- **`border-radius: inherit`** - Matches parent element's border radius
- **`position: absolute`** - Positions relative to parent
- **`inset: -${spread}`** - Expands pseudo-element beyond parent bounds
- **`transform: translate3d(${hOffset},${vOffset},-1)`** - Applies shadow offset and z-positioning
- **`background: ${color}`** - Sets gradient or solid color
- **`filter: blur(${blur})`** - Applies blur effect
- **`clip-path: polygon(...)`** - Creates cutout to prevent shadow overlap

### Clip-Path Polygon Calculation

The complex polygon creates a "donut" shape that excludes the original element area:

```
Outer Rectangle: -100vmax to 100vmax (covers entire viewport)
Inner Rectangle: Calculated based on spread and offset values
```

**Calculation Logic**
- **Top-Left**: `calc(0px + ${spread} - ${hOffset}), calc(0px + ${spread} - ${vOffset})`
- **Top-Right**: `calc(100% - ${spread} - ${hOffset}), calc(0px + ${spread} - ${vOffset})`
- **Bottom-Right**: `calc(100% - ${spread} - ${hOffset}), calc(100% - ${spread} - ${vOffset})`
- **Bottom-Left**: `calc(0px + ${spread} - ${hOffset}), calc(100% - ${spread} - ${vOffset})`

## Usage Examples

### Traditional Shadow with Gradient

```typescript
const result = await shadowGradientCreator(
  "5px 10px 15px 8px linear-gradient(45deg, red, blue)", 
  false
);

// Generated CSS properties:
// content:" ";
// border-radius:inherit;
// position:absolute;
// inset:-8px;
// transform:translate3d(5px,10px,-1);
// background:linear-gradient(45deg, red, blue);
// filter:blur(15px);
// clip-path: polygon(...);
```

### Pure Gradient Effect

```typescript
const result = await shadowGradientCreator(
  "radial-gradient(circle, #ff0000, #0000ff)", 
  true
);

// Generated CSS (using default offset/blur values):
// content:" ";
// border-radius:inherit;
// position:absolute;
// inset:-5;
// transform:translate3d(0,0,-1);
// background:radial-gradient(circle, #ff0000, #0000ff);
// filter:blur(5);
// clip-path: polygon(...);
```

### Inset Shadow with Gradient

```typescript
const result = await shadowGradientCreator(
  "inset 2px 4px 6px 3px conic-gradient(from 0deg, yellow, green)", 
  false
);

// Processes inset flag and applies gradient background
```

## Integration with CSS Generation

### Parent Element Setup

The generated CSS is designed to work with pseudo-elements (::before, ::after) on a parent element that has:

```css
.parent-element {
  transform-style: preserve-3d;
  position: relative;
}
```

### Multi-Shadow Support

The function can be called multiple times to create layered shadow effects:

```typescript
// Layer 1: ::before pseudo-element
const shadow1 = await shadowGradientCreator("5px 5px 10px gradient1");

// Layer 2: ::after pseudo-element  
const shadow2 = await shadowGradientCreator("10px 10px 20px gradient2");
```

## Performance Considerations

### CSS Efficiency

- **Hardware Acceleration**: Uses `translate3d()` for GPU acceleration
- **Modern Properties**: Leverages `inset` and `clip-path` for efficiency
- **Minimal DOM Impact**: Uses pseudo-elements instead of additional elements

### Calculation Optimization

- **Single Parse**: Parses shadow values in one pass
- **Fallback Values**: Provides sensible defaults for missing values
- **String Operations**: Efficient string manipulation for value extraction

## Browser Compatibility

### Modern CSS Features

- **`clip-path`**: Requires modern browser support
- **`inset` Property**: CSS Logical Properties support needed
- **`translate3d()`**: Widely supported for hardware acceleration
- **CSS Gradients**: Supported in all modern browsers

### Fallback Strategy

The generated CSS is designed to gracefully degrade in older browsers by relying on:
- Standard `position` and `background` properties
- Transform-based positioning
- Filter effects for blur

## Error Handling

### Robust Parsing

- **Regex Safety**: Handles malformed shadow strings gracefully
- **Default Values**: Provides fallbacks for missing parameters
- **Type Safety**: Ensures string output regardless of input format

### Logging Integration

- **Debug Information**: Logs parsing results for troubleshooting
- **Value Tracking**: Records extracted numerical values
- **Error Context**: Provides context for debugging malformed inputs

This function represents advanced CSS generation capabilities, creating sophisticated visual effects that would typically require complex CSS or additional HTML elements, all through programmatic pseudo-element generation.
