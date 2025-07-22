# types.private.ts

## Overview

Private type definitions used within the main CSS generation functions. These types provide structure for internal data handling, parameter passing, and complex operations within the CSS generation pipeline.

## Purpose

- Define internal data structures for CSS generation
- Provide type safety for complex operations
- Structure data flow between private utility functions
- Enable type-safe parameter passing in internal APIs

## Type Definitions

### TCombineArrays

```typescript
type TCombineArrays = {
  name: string;
  array: any[];
};
```

**Purpose:** Structure for combining multiple arrays with named identification.

**Properties:**
- `name`: Identifier for the array combination
- `array`: The array data to be combined

**Usage:** Used in operations that need to merge or process multiple arrays while maintaining their identity and context.

**Common Use Cases:**
- Combining CSS rule arrays from different sources
- Merging configuration arrays with identification
- Processing multiple value sets with context preservation

### TNameVal

```typescript
type TNameVal = {
  name: string;
  val: string;
};
```

**Purpose:** Basic name-value pair structure for CSS-related data.

**Properties:**
- `name`: The name or identifier (e.g., CSS property name, class name)
- `val`: The associated value (e.g., CSS value, computed result)

**Usage:** Fundamental data structure for CSS property-value relationships and intermediate processing results.

**Common Use Cases:**
- CSS property-value pairs during generation
- Intermediate results in CSS processing pipeline
- Configuration name-value mappings
- Class name to CSS value associations

### TNameValNumber

```typescript
type TNameValNumber = {
  val: TNameVal;
  number: number;
};
```

**Purpose:** Extends name-value pairs with numeric context for ordered processing.

**Properties:**
- `val`: A `TNameVal` object containing name-value pair
- `number`: Numeric value for ordering, priority, or context

**Usage:** Used when name-value pairs need numeric context for processing order, priority, or calculations.

**Common Use Cases:**
- Priority-based CSS rule processing
- Ordered generation of CSS rules
- Index-based operations on CSS data
- Weighted or scored CSS properties

### TNameValProp

```typescript
type TNameValProp = {
  val: TNameVal;
  prop: string;
};
```

**Purpose:** Extends name-value pairs with additional property context.

**Properties:**
- `val`: A `TNameVal` object containing name-value pair
- `prop`: Additional property or metadata string

**Usage:** Used when name-value pairs require additional property context or metadata for processing.

**Common Use Cases:**
- CSS rules with property modifiers
- Values with transformation context
- Properties with additional metadata
- Complex CSS property relationships

## Integration Points

### With Private Utilities
- Used extensively throughout `private_utilities/` functions
- Provides consistent data structures for internal operations
- Enables type-safe function signatures

### With CSS Generation Pipeline
- Structures data flow between processing stages
- Maintains type safety during complex transformations
- Enables predictable data handling

### With Value Processing
- Supports complex value transformations
- Provides structure for multi-step processing
- Maintains data integrity through processing pipeline

## Usage Patterns

### Basic Name-Value Operations
```typescript
const property: TNameVal = {
  name: 'margin',
  val: '10px'
};
```

### Ordered Processing
```typescript
const orderedProperty: TNameValNumber = {
  val: { name: 'padding', val: '5px' },
  number: 1
};
```

### Extended Property Context
```typescript
const extendedProperty: TNameValProp = {
  val: { name: 'color', val: 'red' },
  prop: 'hover'
};
```

### Array Combination Operations
```typescript
const combinedArrays: TCombineArrays = {
  name: 'breakpoint-rules',
  array: [rule1, rule2, rule3]
};
```

## Type Safety Benefits

### Compile-Time Validation
- Ensures correct data structure usage
- Prevents runtime errors from malformed data
- Provides IntelliSense support in development

### Consistent Data Flow
- Standardizes internal data structures
- Reduces complexity in function signatures
- Improves maintainability

### Error Prevention
- Catches type mismatches during development
- Ensures proper property access
- Prevents undefined property access

## Design Principles

### Simplicity
- Minimal, focused type definitions
- Clear property naming conventions
- Easy to understand and use

### Extensibility
- Composable type structures
- Building blocks for complex operations
- Flexible enough for various use cases

### Type Safety
- Strict typing for all properties
- No optional properties for clarity
- Predictable data structures

## Notes

- Private types used exclusively within main CSS generation functions
- Provides structure and type safety for internal operations
- Essential for maintaining data integrity in complex CSS processing
- Designed for performance and clarity in internal APIs
- Supports the library's type-safe architecture
- Minimal but comprehensive type definitions for internal use
