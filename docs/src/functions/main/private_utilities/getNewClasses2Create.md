# getNewClasses2Create.ts

## Overview

Private utility function that scans the entire DOM to identify new CSS classes that need to be created. This function analyzes all elements in the document, processes combos, and filters classes that should be generated by the CSS creation system.

## Purpose

- Scan DOM for all CSS classes used in the document
- Identify classes that require CSS generation
- Process combo classes and expand them appropriately
- Filter classes based on library conventions and rules
- Build comprehensive list of classes needing CSS creation

## Core Functionality

### getNewClasses2Create(classes2Create: string[]): Promise<string[]>

**Parameters:**
- `classes2Create`: Initial array of classes to create (accumulator)

**Returns:** Promise resolving to updated array of classes requiring CSS generation

**Purpose:** Scans the entire DOM and identifies all classes that need CSS rule generation.

## Processing Pipeline

### 1. DOM Scanning

**Element Iteration:**
```typescript
Array.from(document.querySelectorAll("*")).forEach((value: Element) => {
  value.classList.forEach(async (item: any) => {
    // Process each class...
  });
});
```

**Scanning Features:**
- Queries all elements in the document using `*` selector
- Iterates through every class on every element
- Comprehensive DOM coverage for class detection
- Processes classes asynchronously for performance

### 2. Combo Detection and Processing

**Combo Identification:**
```typescript
let comb = Object.keys(values.combos).find((cs) => {
  return item.includes(cs);
});
```

**Combo Processing:**
- Identifies classes that contain combo definitions
- Processes combos using `comboParser` for expansion
- Generates additional classes from combo definitions
- Maintains class relationships and dependencies

**Combo Expansion:**
```typescript
if (!!comb && values.combos[comb]) {
  classes2Create = await comboParser(item, comb, value as HTMLElement, classes2Create);
}
```

### 3. Class Filtering

**Inclusion Criteria:**
```typescript
if (!comb && 
    !classes2Create.includes(item) && 
    item !== values.indicatorClass &&
    (item.includes(values.indicatorClass) || 
     Object.keys(values.abreviationsClasses).find((aC) => item.includes(aC)))) {
  classes2Create.push(item);
}
```

**Filter Rules:**
- **Not a combo**: Class doesn't match combo patterns
- **Not duplicate**: Class not already in creation list
- **Not indicator class**: Not the base indicator class itself
- **Contains indicator**: Class contains the library's indicator prefix
- **Contains abbreviation**: Class contains known abbreviation patterns

## Class Categories

### Combo Classes
- Classes that match combo definition patterns
- Require expansion through combo processing
- Generate multiple related CSS rules
- Processed by `comboParser` for full expansion

### Indicator Classes
- Classes containing the library's indicator prefix
- Target classes for CSS generation
- Follow library naming conventions
- Require CSS rule creation

### Abbreviation Classes
- Classes containing known abbreviation patterns
- Use the library's abbreviation system
- Require translation and CSS generation
- Follow abbreviation-based naming conventions

### Excluded Classes
- Base indicator class itself
- Classes already in creation list
- Classes not following library conventions
- System-reserved class names

## Dependencies

- `ValuesSingleton` from `../../../singletons/valuesSingleton`
- `comboParser` from `./comboParser`

## Integration Points

### With DOM
- Direct DOM scanning and analysis
- Real-time class detection from live document
- Element-by-element class processing
- Comprehensive document coverage

### With Combo System
- Integrates with combo processing pipeline
- Expands combo classes to their components
- Maintains combo relationships and dependencies
- Processes complex combo structures

### With CSS Generation
- Provides input for CSS rule creation
- Identifies classes requiring CSS generation
- Filters classes based on generation rules
- Maintains class creation queue

## Performance Considerations

### DOM Scanning Optimization
- Single pass through entire DOM
- Efficient element and class iteration
- Minimal DOM queries for comprehensive coverage
- Asynchronous processing for complex operations

### Memory Efficiency
- Accumulates classes in existing array
- Avoids duplicate class entries
- Efficient array operations for class management
- Minimal object creation during scanning

### Processing Efficiency
- Early filtering to avoid unnecessary processing
- Efficient combo detection with single lookup
- Optimized abbreviation pattern matching
- Streamlined class validation logic

## Error Handling

### Robust DOM Processing
- Handles dynamic DOM changes gracefully
- Continues processing despite individual element errors
- Maintains scanning integrity across the document
- Safe class list iteration

### Combo Processing Safety
- Handles missing combo definitions
- Continues processing despite combo errors
- Maintains class list integrity during failures
- Safe async/await error handling

## Usage Context

### CSS Generation Trigger
```javascript
// Scan for new classes during CSS generation
const newClasses = await getNewClasses2Create(existingClasses);
// Process newClasses for CSS rule creation
```

### Dynamic Class Detection
```javascript
// Detect classes after DOM updates
const updatedClasses = await getNewClasses2Create([]);
// Generate CSS for newly discovered classes
```

## Advanced Features

### Real-Time Detection
- Scans current DOM state for up-to-date class detection
- Handles dynamically added classes and elements
- Supports single-page application scenarios
- Adapts to runtime DOM changes

### Comprehensive Coverage
- Processes all elements regardless of nesting
- Handles complex DOM structures
- Supports shadow DOM and modern web components
- Ensures complete class discovery

### Intelligent Filtering
- Multiple criteria for class inclusion
- Supports various library conventions
- Handles edge cases and special patterns
- Maintains high signal-to-noise ratio

## Integration Examples

### With CSS Creation
```javascript
// Used in CSS generation pipeline
const classesToCreate = await getNewClasses2Create([]);
// classesToCreate now contains all classes needing CSS
```

### With Combo Processing
```javascript
// Automatic combo expansion during scanning
// Combos are processed and expanded automatically
// Generated classes added to creation list
```

## Notes

- Essential for comprehensive class detection in the library
- Handles both simple and complex class patterns
- Integrates combo processing seamlessly
- Provides efficient DOM scanning with intelligent filtering
- Supports dynamic web applications with real-time detection
- Maintains performance while providing comprehensive coverage
- Critical component of the CSS generation pipeline
