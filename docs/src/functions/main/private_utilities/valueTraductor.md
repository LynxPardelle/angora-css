# valueTraductor - CSS Value Translation and Color Processing Engine

## Overview

The `valueTraductor` function serves as a comprehensive CSS value translator that handles abbreviation expansion, color name resolution, opacity parsing, and color format conversion. It ensures CSS values are properly formatted and compatible with CSS standards.

## Location

```
src/functions/main/private_utilities/valueTraductor.ts
```

## Dependencies

- `valuesSingleton.ts` - Global color and abbreviation configurations
- `abreviation_traductors.ts` - Abbreviation translation services
- `console_log.ts` - Logging functionality
- `color_transform.ts` - Color format conversion utilities

## Core Functions

### valueTraductor()

```typescript
async valueTraductor(value: string, property: string): Promise<string>
```

Translates and processes CSS values, handling abbreviations, colors, and special formatting.

#### Parameters

- `value: string` - The CSS value to be translated and processed
- `property: string` - The CSS property context for value processing

#### Returns

- `Promise<string>` - Processed and validated CSS value

### opaParser()

```typescript
async opaParser(value: string): Promise<string>
```

Specialized parser for opacity notation (OPA) in color values.

#### Parameters

- `value: string` - Value string potentially containing opacity notation

#### Returns

- `Promise<string>` - Value with opacity notation converted to valid CSS

## Processing Pipeline

### 1. Abbreviation Translation

```typescript
value = abreviation_traductors.abreviationTraductor(
  !!values.abreviationsValues[value]
    ? values.abreviationsValues[value]
    : value
);
```

- **Lookup**: Checks `values.abreviationsValues` for abbreviation definitions
- **Translation**: Replaces abbreviated values with full CSS values
- **Fallback**: Uses original value if no abbreviation found

### 2. Content Property Bypass

```typescript
if (!property.includes("content")) {
  // Process colors and opacity only for non-content properties
}
```

- **Content Exception**: Skips color processing for CSS `content` property
- **Literal Values**: Preserves literal strings in content declarations
- **Security**: Prevents unwanted color substitution in text content

### 3. Opacity Processing

```typescript
value = await opaParser(value);
```

Processes OPA (opacity) notation before color processing.

### 4. Color Name Resolution

```typescript
let colors = Object.keys(values.colors)
  .sort((c1, c2) => c2.length - c1.length)
  .map((c) => `(${c})`)
  .join("|");
let colorsRegString: string = `(?<![a-zA-Z0-9])(${colors})(?![a-zA-Z0-9])`;
let colorsReg = new RegExp(colorsRegString, "gi");
```

**Dynamic Regex Construction**
- **Length Sorting**: Processes longer color names first to avoid partial matches
- **Word Boundaries**: Uses negative lookbehind/lookahead to ensure complete word matches
- **Case Insensitive**: Supports color names in any case

**Color Processing Loop**
```typescript
for (let match of matches) {
  let realColor: string | undefined = values.colors[match.replace(/\s/g, "")];
  // Color format conversion logic
}
```

### 5. Color Format Standardization

```typescript
switch (true) {
  case !!realColor && realColor.startsWith("rgb") && !realColor.includes("rgba"):
    realColorValue = `rgba(${realColor}, 1)`;
    break;
  case !!realColor && realColor.startsWith("#"):
    realColorValue = `rgba(${color_transform.colorToRGB(realColor)}, 1)`;
    break;
  default:
    realColorValue = realColorValue;
}
```

- **RGB to RGBA**: Adds alpha channel to RGB colors
- **Hex to RGBA**: Converts hex colors to RGBA format
- **Standardization**: Ensures consistent color format across the system

## Opacity Parser (OPA) System

### OPA Notation Format

```
colorOPA0.5  →  rgba(color, 0.5)
```

### Processing Logic

```typescript
const reg = new RegExp(
  /(?:([A-z0-9#]*)|(?:(rgb)|(hsl)|(hwb))a?\([0-9\.\,\s%]*\))\s?OPA\s?0\.[0-9]*/gi
);
```

**Pattern Matching**
- **Color Formats**: Supports hex, named colors, rgb(), hsl(), hwb()
- **Opacity Values**: Matches decimal opacity values (0.0 to 0.9)
- **Flexible Spacing**: Handles optional whitespace around OPA notation

**Conversion Process**
```typescript
const color = OPA.split("OPA")[0];
const OPAValue = OPA.split("OPA")[1];
const realColor = color_transform.colorToRGB(
  !!values.colors[color.toString().replace(/\s/g, "")]
    ? values.colors[color.toString().replace(/\s/g, "")]
    : color
);
value = value
  .replace(color, `rgba(${realColor},${OPAValue})`)
  .replace("OPA" + OPAValue, "");
```

## Usage Examples

### Abbreviation Translation

```typescript
// values.abreviationsValues = { "sm": "small", "lg": "large" }
const result = await valueTraductor("sm", "font-size");
// Input: "sm" → Output: "small"
```

### Color Name Resolution

```typescript
// values.colors = { "primary": "#007bff", "red": "#ff0000" }
const result = await valueTraductor("primary", "background-color");
// Input: "primary" → Output: "rgba(0, 123, 255, 1)"
```

### Opacity Notation

```typescript
const result = await valueTraductor("primaryOPA0.5", "background-color");
// Input: "primaryOPA0.5" → Output: "rgba(0, 123, 255, 0.5)"
```

### Complex Color Processing

```typescript
const result = await valueTraductor("#ff0000OPA0.8", "color");
// Input: "#ff0000OPA0.8" → Output: "rgba(255, 0, 0, 0.8)"
```

### Content Property Bypass

```typescript
const result = await valueTraductor("'Hello primary world'", "content");
// Input: "'Hello primary world'" → Output: "'Hello primary world'" (unchanged)
```

## Performance Optimizations

### Color Regex Efficiency

- **Length Sorting**: Processes longer color names first to prevent partial matches
- **Single Pass**: One regex operation handles all color replacements
- **Compiled Regex**: Regex is constructed once per function call

### Async Processing

- **Promise.all**: Parallel processing of multiple OPA matches
- **Non-blocking**: Doesn't block other CSS generation operations
- **Efficient Memory**: Minimal memory allocation during processing

## Error Handling

### Graceful Degradation

- **Invalid Colors**: Preserves original value if color lookup fails
- **Malformed OPA**: Continues processing if OPA pattern is invalid
- **Missing Values**: Handles undefined abbreviations gracefully

### Validation

- **Type Safety**: TypeScript ensures proper parameter types
- **Format Validation**: Ensures output is valid CSS syntax
- **Null Safety**: Handles empty or undefined input values

## Integration Points

### Color System Integration

- **Global Colors**: Uses `values.colors` for color name resolution
- **Color Transform**: Integrates with color conversion utilities
- **Format Consistency**: Ensures all colors use RGBA format

### Abbreviation System

- **Value Abbreviations**: Processes value-specific abbreviations
- **Extensible**: Supports custom abbreviation definitions
- **Fallback**: Graceful handling of unknown abbreviations

## Architecture Integration

### CSS Generation Pipeline

```
parseClass → look4BPNVals → valueTraductor → property2ValueJoiner
```

This function serves as the value processing hub, ensuring all CSS values are properly translated and formatted before final rule assembly.

### Configuration Dependencies

- **Color Definitions**: `values.colors` for color name mappings
- **Abbreviations**: `values.abreviationsValues` for value shortcuts
- **Global State**: Read-only access to configuration systems

This function represents a critical component in the CSS value processing system, handling the complex task of translating human-readable values into valid CSS syntax while maintaining compatibility with the broader color and abbreviation systems.
