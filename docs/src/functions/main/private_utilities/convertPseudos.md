# convertPseudos.ts

## Overview

Private utility function that converts pseudo-class masks to their actual CSS pseudo-class syntax. This function handles the translation from abbreviated pseudo-class notation used within the library to valid CSS pseudo-class selectors, supporting special cases and parameter handling.

## Purpose

- Convert pseudo-class masks to actual CSS pseudo-class syntax
- Handle special pseudo-classes with parameters (e.g., `:nth-child()`)
- Support pseudo-elements like `::before`, `::after`
- Manage page-specific pseudo-classes for print media
- Provide option to remove pseudo-classes entirely

## Core Functionality

### convertPseudos(thing: string, remove: boolean = false): string

**Parameters:**
- `thing`: String containing pseudo-class masks to convert
- `remove`: Optional flag to remove pseudo-classes instead of converting (default: false)

**Returns:** String with converted or removed pseudo-classes

**Purpose:** Transforms pseudo-class masks into valid CSS pseudo-class syntax or removes them entirely.

## Conversion Process

### 1. Pseudo-Class Detection

**Filtering Process:**
```typescript
let pseudoFiltereds: IPseudo[] = values.pseudos.filter((pseudo: IPseudo) => {
  return thing.includes(pseudo.mask);
});
```

**Detection Features:**
- Scans input string for known pseudo-class masks
- Filters applicable pseudo-classes from global definitions
- Supports multiple pseudo-classes in single string
- Maintains order for proper conversion

### 2. Regular Expression Generation

**Pattern Creation:**
```typescript
let regMask = new RegExp(":*" + pse.mask, "gi");
```

**Special Case Handling:**
- **Parameter Pseudo-classes**: Adds `\(` for pseudo-classes with parameters
- **Page Pseudo-classes**: Handles `pageRight`, `pageLeft` for print media
- **Standard Pseudo-classes**: Basic colon-prefixed patterns

### 3. String Replacement

**Replacement Logic:**
```typescript
thing = thing
  .replace("SD", "(")
  .replace("ED", ")")
  .replace(regMask, conversionTarget);
```

**Replacement Types:**
- **Convert Mode**: Replaces masks with actual CSS pseudo-class syntax
- **Remove Mode**: Removes pseudo-class patterns entirely
- **Parameter Handling**: Converts `SD` to `(` and `ED` to `)` for parameters

## Pseudo-Class Categories

### Standard Pseudo-Classes
- Basic pseudo-classes like `:hover`, `:focus`, `:active`
- Simple mask-to-CSS conversion
- No special parameter handling required

**Example:**
```javascript
"button-hover" → "button:hover"
```

### Parameter Pseudo-Classes
- Pseudo-classes requiring parameters like `:nth-child()`, `:nth-of-type()`
- Special handling for opening parenthesis
- Parameter conversion using SD/ED markers

**Example:**
```javascript
"item-nthChildSD2nED" → "item:nth-child(2n)"
```

### Page Pseudo-Classes
- Print media pseudo-classes: `@page :left`, `@page :right`
- Special pattern matching for page contexts
- Handles print stylesheet generation

**Example:**
```javascript
"pageLeft" → "page:left"
```

## Parameter Handling

### SD/ED Token System
- **SD (Start Delimiter)**: Converted to opening parenthesis `(`
- **ED (End Delimiter)**: Converted to closing parenthesis `)`
- Enables parameter representation in class names

### Parameter Examples
```javascript
// nth-child parameter handling
"nthChildSD2nED" → ":nth-child(2n)"
"nthOfTypeSD1ED" → ":nth-of-type(1)"
"notSDdisabledED" → ":not(disabled)"
```

## Dependencies

- `IPseudo` interface from `../../../interfaces`
- `ValuesSingleton` from `../../../singletons/valuesSingleton`
- `console_log` from `../../console_log`

## Integration Points

### With Pseudo-Class System
- Uses global pseudo-class definitions from singleton
- Integrates with pseudo-class detection system
- Maintains consistency with pseudo-class naming

### With CSS Generation
- Provides clean CSS pseudo-class output
- Ensures valid CSS selector syntax
- Supports both conversion and removal modes

### With Class Processing
- Integral part of class name processing pipeline
- Handles pseudo-class conversion during CSS generation
- Maintains class name structure integrity

## Configuration Integration

### Pseudo-Class Definitions
- Uses `values.pseudos` for mask-to-CSS mappings
- Leverages `values.pseudosHasSDED` for parameter identification
- Integrates with global pseudo-class configuration

### Special Categories
- **Parameter Pseudo-classes**: Listed in `pseudosHasSDED`
- **Page Pseudo-classes**: Special handling for `Right`, `Left`
- **Standard Pseudo-classes**: Default conversion behavior

## Error Handling

### Robust Processing
- Handles missing pseudo-class definitions gracefully
- Continues processing despite conversion errors
- Maintains string integrity during failures

### Debug Support
- Logs input and output for debugging
- Provides visibility into conversion process
- Supports troubleshooting pseudo-class issues

## Performance Considerations

### Efficient Processing
- Filters applicable pseudo-classes before processing
- Uses optimized regular expressions
- Minimizes string operations

### Memory Management
- No memory leaks in string processing
- Efficient regular expression compilation
- Minimal object creation

## Usage Context

### CSS Generation
```javascript
// Convert pseudo-class in class name
const converted = convertPseudos("btn-primary-hover");
// Result: "btn-primary:hover"

// Remove pseudo-classes
const cleaned = convertPseudos("btn-primary-hover", true);
// Result: "btn-primary"
```

### Complex Pseudo-Classes
```javascript
// Parameter pseudo-class conversion
const complex = convertPseudos("item-nthChildSD2nPLUS1ED");
// Result: "item:nth-child(2n+1)"
```

## Advanced Features

### Multi-Pseudo Support
- Handles multiple pseudo-classes in single string
- Maintains proper conversion order
- Supports complex selector combinations

### Flexible Removal
- Optional removal mode for cleaning class names
- Useful for base class extraction
- Supports conditional pseudo-class handling

### Print Media Support
- Specialized handling for page pseudo-classes
- Supports print stylesheet generation
- Maintains print media syntax compliance

## Notes

- Essential for pseudo-class conversion in CSS generation
- Handles complex parameter pseudo-classes with special syntax
- Supports both conversion and removal operations
- Integrates seamlessly with global pseudo-class configuration
- Provides robust error handling and debug support
- Optimized for performance with efficient string processing
- Critical component of class name processing pipeline
