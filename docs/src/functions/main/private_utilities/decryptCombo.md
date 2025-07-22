# decryptCombo.ts

## Overview

Private utility function that decrypts combo abbreviations back to their original class names. This function reverses the combo encryption process by finding abbreviated combo references and replacing them with their full class names, supporting the combo system's abbreviation and encryption features.

## Purpose

- Decrypt abbreviated combo references to full class names
- Reverse the combo encryption process
- Handle combo abbreviation lookup and replacement
- Support multiple string values in parallel processing
- Maintain combo system consistency

## Core Functionality

### decryptCombo(specify, class2Create, class2CreateStringed): Promise<string[]>

**Parameters:**
- `specify`: CSS selector specification string
- `class2Create`: Base class name being processed
- `class2CreateStringed`: Stringified version of the class

**Returns:** Promise resolving to array of decrypted strings

**Purpose:** Finds combo abbreviations and replaces them with their original class names across multiple input strings.

## Decryption Process

### 1. Abbreviation Detection

**Lookup Process:**
```typescript
let alreadyABBRCombo = Object.keys(values.combosCreated).find((cs) => {
  return specify.includes(cs);
});
```

**Detection Features:**
- Searches for known combo abbreviations in the specify string
- Uses the global `combosCreated` mapping for abbreviation lookup
- Identifies first matching abbreviation for processing
- Supports partial string matching within larger selectors

### 2. Parallel Decryption

**Batch Processing:**
```typescript
return await Promise.all(
  [specify, class2Create, class2CreateStringed].map(async (val, index) => {
    return alreadyABBRCombo
      ? val.replace(new RegExp(alreadyABBRCombo, "g"), values.combosCreated[alreadyABBRCombo])
      : val;
  })
);
```

**Processing Features:**
- Processes all three input strings simultaneously
- Uses global regular expression replacement for all occurrences
- Maintains string order in output array
- Preserves original strings if no abbreviation found

### 3. Replacement Logic

**String Replacement:**
- Replaces all occurrences of abbreviation with full class name
- Uses global regex for comprehensive replacement
- Maintains string structure and formatting
- Preserves non-abbreviated content

## Combo Abbreviation System

### Abbreviation Mapping
- Uses `values.combosCreated` for abbreviation-to-class mapping
- Supports both encrypted and plain abbreviations
- Maintains bidirectional lookup capability
- Tracks all created combo abbreviations

### Decryption Examples
```javascript
// Encrypted abbreviation
"abc123" → "btn-primary-large"

// Plain abbreviation
"btn-combo" → "btn-primary-large"

// Partial replacement in selector
".abc123:hover" → ".btn-primary-large:hover"
```

## Return Value Structure

### Success Case (Abbreviation Found)
```javascript
[
  "decrypted-specify-string",
  "decrypted-class2Create",
  "decrypted-class2CreateStringed"
]
```

### No Abbreviation Case
```javascript
[
  "original-specify-string",
  "original-class2Create", 
  "original-class2CreateStringed"
]
```

## Dependencies

- `ValuesSingleton` from `../../../singletons/valuesSingleton`
- `console_log` from `../../../functions/console_log`

## Integration Points

### With Combo System
- Integrates with combo abbreviation creation system
- Uses global combo abbreviation mapping
- Supports combo encryption/decryption workflow

### With CSS Generation
- Provides decrypted class names for CSS rule generation
- Ensures proper selector syntax in generated CSS
- Maintains class name consistency across processing

### With Class Processing Pipeline
- Part of class name resolution process
- Handles abbreviation expansion during CSS generation
- Supports complex selector processing

## Performance Considerations

### Asynchronous Processing
- Uses `Promise.all()` for parallel string processing
- Optimizes multiple string replacement operations
- Efficient abbreviation lookup with early termination

### Memory Efficiency
- Minimal object creation during processing
- Efficient regular expression usage
- No memory leaks in string operations

### Lookup Optimization
- Single abbreviation search per function call
- Efficient object key iteration
- Early exit for non-abbreviated content

## Error Handling

### Graceful Processing
- Returns original strings if no abbreviation found
- Handles missing abbreviations without errors
- Continues processing despite lookup failures

### Debug Support
- Logs abbreviation detection for troubleshooting
- Provides visibility into decryption process
- Supports combo system debugging

## Usage Context

### CSS Rule Generation
```javascript
// Decrypt combo abbreviation in CSS selector
const [decryptedSpecify, decryptedClass, decryptedStringed] = 
  await decryptCombo(".abc123:hover", "abc123", "abc123-string");
// Result: [".btn-primary-large:hover", "btn-primary-large", "btn-primary-large-string"]
```

### Selector Processing
```javascript
// Handle abbreviated selectors
const decrypted = await decryptCombo(
  ".combo-abc:focus", 
  "combo-abc", 
  "combo-abc-processed"
);
```

## Advanced Features

### Global Replacement
- Replaces all occurrences of abbreviation in each string
- Handles complex selectors with multiple abbreviation references
- Maintains selector structure integrity

### Multi-String Processing
- Processes multiple related strings simultaneously
- Maintains consistency across all processed strings
- Optimizes for batch operations

### Conditional Processing
- Only processes strings when abbreviations are found
- Preserves original content when no decryption needed
- Efficient for mixed content scenarios

## Integration Examples

### With Combo Creation
```javascript
// After combo abbreviation creation
const abbreviated = "abc123"; // Created by combo system
const [decrypted] = await decryptCombo(abbreviated, abbreviated, abbreviated);
// Returns original class name
```

### With CSS Generation
```javascript
// During CSS rule processing
const [selector, className] = await decryptCombo(
  ".encrypted-combo:hover",
  "encrypted-combo", 
  "encrypted-combo-str"
);
// Use decrypted values for CSS generation
```

## Notes

- Essential for combo abbreviation resolution
- Supports both encrypted and plain combo abbreviations
- Handles multiple string processing efficiently
- Maintains consistency with combo creation system
- Provides robust error handling and debug support
- Optimized for performance with parallel processing
- Critical component of combo system workflow
