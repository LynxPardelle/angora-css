# Combinators - Array and Object Utility Functions

## Overview
The `combinators` module provides utility functions for combining arrays and objects in various ways. These functions are essential for data transformation and combination operations throughout the Angora CSS system.

## Location
```
src/functions/utilities/combinators.ts
```

## Dependencies
- `types.private.ts` - Type definitions for combination operations

## Functions

### combineArrays<T, U, V>()
```typescript
combineArrays<T, U, V>(a: TCombineArrays, b: TCombineArrays): V[]
```

Combines two arrays based on their structure, creating cartesian product combinations with named properties.

#### Parameters
- `a: TCombineArrays` - First array with metadata containing name and array values
- `b: TCombineArrays` - Second array with metadata containing name and array values

#### Returns
- `V[]` - Array of combined objects with properties from both input arrays

#### Processing Pipeline
1. **Outer Loop**: Iterates through first array (`a.array`)
2. **Inner Mapping**: Maps each element from second array (`b.array`) 
3. **Object Creation**: Creates objects with properties `{[a.name]: val, [b.name]: v}`
4. **Accumulation**: Spreads results into accumulator array

#### Usage Example
```typescript
const colors = { name: 'color', array: ['red', 'blue'] };
const sizes = { name: 'size', array: ['sm', 'lg'] };

const combinations = combinators.combineArrays(colors, sizes);
// Result: [
//   {color: 'red', size: 'sm'},
//   {color: 'red', size: 'lg'},
//   {color: 'blue', size: 'sm'},
//   {color: 'blue', size: 'lg'}
// ]
```

### combineIntoObject()
```typescript
combineIntoObject(array: TNameVal[]): { [key: string]: string }
```

Converts an array of name-value pairs into a single object with key-value properties.

#### Parameters
- `array: TNameVal[]` - Array of objects with `name` and `val` properties

#### Returns
- `{ [key: string]: string }` - Single object with combined properties

#### Processing Pipeline
1. **Reduction**: Uses array.reduce() for accumulation
2. **Property Extraction**: Extracts `name` and `val` from each item
3. **Object Spreading**: Spreads existing accumulator and adds new property
4. **Dynamic Keys**: Uses computed property names `[val.name]: val.val`

#### Usage Example
```typescript
const nameValuePairs = [
  { name: 'color', val: 'red' },
  { name: 'size', val: 'large' },
  { name: 'weight', val: 'bold' }
];

const combined = combinators.combineIntoObject(nameValuePairs);
// Result: { color: 'red', size: 'large', weight: 'bold' }
```

## Type System Integration

### TCombineArrays Type
```typescript
interface TCombineArrays {
  name: string;    // Property name for resulting objects
  array: any[];    // Array of values to combine
}
```

### TNameVal Type
```typescript
interface TNameVal {
  name: string;    // Property name
  val: string;     // Property value
}
```

## Architecture Integration

### Data Transformation Pipeline
- **CSS Generation**: Combines breakpoint values with CSS properties
- **Class Creation**: Merges different CSS rule components
- **Configuration Processing**: Transforms configuration arrays into objects

### Performance Considerations
- **Memory Efficiency**: Uses spread operators for immutable operations
- **Type Safety**: Generic types ensure compile-time type checking
- **Functional Approach**: Pure functions without side effects

## Usage Patterns

### In CSS Generation
```typescript
// Combining breakpoints with properties
const breakpoints = { name: 'bp', array: ['sm', 'md', 'lg'] };
const properties = { name: 'prop', array: ['margin', 'padding'] };
const combinations = combinators.combineArrays(breakpoints, properties);
```

### In Configuration Processing
```typescript
// Converting configuration to object
const config = [
  { name: 'primaryColor', val: '#007bff' },
  { name: 'secondaryColor', val: '#6c757d' },
  { name: 'borderRadius', val: '4px' }
];
const configObject = combinators.combineIntoObject(config);
```

## Error Handling
- **Type Safety**: TypeScript ensures correct input types
- **Immutable Operations**: No mutation of input arrays/objects
- **Consistent Output**: Always returns expected data structures

## Integration Points
- Used by CSS generation pipeline for property combinations
- Utilized in configuration processing systems
- Integrated with breakpoint management functions
- Applied in theme and variant generation processes
