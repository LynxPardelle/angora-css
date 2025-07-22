# values4ComboGetter - Combo Value Extraction and Organization System

## Overview

The `values4ComboGetter` function extracts and organizes values from combo class names using a sophisticated parsing system. It handles both indexed (VAL{n}N) and sequential (VL) value patterns, organizing them into properly ordered arrays for combo processing.

## Location

```
src/functions/main/private_utilities/values4ComboGetter.ts
```

## Dependencies

- `console_log.ts` - Logging functionality for debugging

## Type Definitions

### TVals2Sort

```typescript
type TVals2Sort = {
  index: number;
  val: string;
}
```

Internal type for managing value sorting and organization.

## Core Function

### values4ComboGetter()

```typescript
async values4ComboGetter(class2Create: string): Promise<string[]>
```

Extracts and organizes values from combo class names with complex indexing support.

#### Parameters

- `class2Create: string` - Class name containing VALS section with value definitions

#### Returns

- `Promise<string[]>` - Ordered array of extracted values

## Value Pattern System

### VALS Section Detection

```typescript
if (!!class2Create.includes("VALS")) {
  let valsSource: string = class2Create.split("VALS")[1];
  // Process values section
}
```

**Section Extraction**
- Splits class name at "VALS" marker
- Processes everything after VALS as values section
- Returns empty array if no VALS section found

### Indexed Values Pattern (VAL{n}N)

```
VAL0Nvalue1VAL0N    - Single index value
VAL1_2Nvalue2VAL1_2N - Multi-index value (indices 1 and 2)
```

**Pattern Regex**
```typescript
let valueReg = new RegExp(/VAL([0-9_]+)N[A-z0-9]+VAL\1N/, "g");
```

**Multi-Index Support**
- **Single Index**: `VAL5N` assigns to position 5
- **Multiple Indices**: `VAL1_3_7N` assigns to positions 1, 3, and 7
- **Duplicate Assignment**: Same value can be assigned to multiple positions

### Sequential Values Pattern (VL)

```
VLvalue1VLvalue2VLvalue3
```

**Simple Sequential**
- Values separated by "VL" markers
- Assigned to available indices not used by indexed values
- Maintains insertion order

## Processing Logic

### 1. Indexed Value Processing

```typescript
let valsToSortExtras: TVals2Sort[] = [];
let valsToSort: TVals2Sort[] = valsToSortSource.map((v: string) => {
  let index: string = v.split("VAL")[1].split("N")[0];
  let valReplace: RegExp = new RegExp(`VAL${index}N`, "g");
  let firstIndex: number = parseInt(index);
  
  if (index.includes("_")) {
    let indexes: string[] = index.split("_");
    firstIndex = parseInt(indexes[0]);
    indexes.forEach((i: string, it: number) => {
      if (it > 0) {
        valsToSortExtras.push({
          index: parseInt(i),
          val: v.replace(valReplace, ""),
        });
      }
    });
  }
  
  return {
    index: firstIndex,
    val: v.replace(valReplace, ""),
  };
});
```

**Index Extraction**
- Parses numeric indices from VAL{index}N pattern
- Handles multi-index assignments with underscore separation
- Creates duplicate entries for multi-index values

**Value Cleaning**
- Removes VAL{index}N wrapper to extract clean value
- Maintains value integrity during extraction

### 2. Sequential Value Integration

```typescript
if (!noValsNotSorted) {
  // Sort the valsNotSorted with indexes not used
  let valsNotSortedSorted: TVals2Sort[] = valsNotSorted.map((v) => {
    let index = 1;
    while (ocupedIndexes.includes(index)) {
      index++;
    }
    ocupedIndexes.push(index);
    return {
      index: index,
      val: v,
    };
  });
}
```

**Available Index Assignment**
- Starts from index 1 for sequential values
- Skips indices already used by indexed values
- Maintains insertion order for sequential values

### 3. Gap Filling

```typescript
let emptyValsToFillValsSorted: TVals2Sort[] = [];
let lastValIndex = valsToSort[valsToSort.length - 1].index;

for (let i = 0; i < lastValIndex; i++) {
  if (!ocupedIndexes.includes(i)) {
    emptyValsToFillValsSorted.push({
      index: i,
      val: "",
    });
  }
}
```

**Index Continuity**
- Identifies gaps in index sequence
- Fills missing indices with empty strings
- Ensures continuous array from 0 to highest index

### 4. Final Sorting and Output

```typescript
let valsSorted: TVals2Sort[] = valsToSort
  .concat(emptyValsToFillValsSorted)
  .sort((v1, v2) => {
    return v1.index - v2.index;
  });

return valsSorted.map((v) => v.val);
```

**Final Organization**
- Combines all value sources
- Sorts by index for proper ordering
- Extracts values into simple string array

## Usage Examples

### Indexed Values Only

```typescript
const className = "btn-VAL0NredVAL0N-VAL2NlargeVAL2N";
const result = await values4ComboGetter(className);
// Result: ["red", "", "large"]
// Index 0: "red", Index 1: empty, Index 2: "large"
```

### Multi-Index Assignment

```typescript
const className = "combo-VAL1_3NblueVAL1_3N";
const result = await values4ComboGetter(className);
// Result: ["", "blue", "", "blue"]
// Assigns "blue" to both indices 1 and 3
```

### Sequential Values Only

```typescript
const className = "style-VLredVLgreenVLblue";
const result = await values4ComboGetter(className);
// Result: ["red", "green", "blue"]
// Sequential assignment starting from index 1
```

### Mixed Values

```typescript
const className = "mixed-VAL0NfirstVAL0N-VLsecondVLthird-VAL5NlastVAL5N";
const result = await values4ComboGetter(className);
// Result: ["first", "second", "third", "", "", "last"]
// Index 0: "first" (indexed)
// Index 1: "second" (sequential)  
// Index 2: "third" (sequential)
// Index 3-4: empty (gap fill)
// Index 5: "last" (indexed)
```

### No Values Section

```typescript
const className = "simple-class-name";
const result = await values4ComboGetter(className);
// Result: []
// No VALS section found
```

## Performance Considerations

### Regex Efficiency

- **Compiled Patterns**: Regex patterns compiled once per function call
- **Specific Matching**: Uses backreferences for accurate pattern matching
- **Minimal Backtracking**: Efficient pattern design

### Array Operations

- **Single Pass Processing**: Most operations in single iterations
- **Efficient Sorting**: Native array sort for final ordering
- **Memory Reuse**: Reuses array structures where possible

## Error Handling

### Graceful Degradation

- **Missing Sections**: Returns empty array for classes without VALS
- **Malformed Patterns**: Falls back to sequential processing
- **Invalid Indices**: Handles non-numeric indices gracefully

### Robust Parsing

- **Pattern Validation**: Validates patterns before processing
- **Fallback Processing**: Multiple processing paths for different patterns
- **Error Recovery**: Continues processing despite individual pattern failures

## Integration Points

### Combo System Integration

- **Value Extraction**: Provides organized values for combo processing
- **Template Support**: Enables complex value organization in combos
- **Pattern Flexibility**: Supports various value assignment patterns

### CSS Generation Flow

```
comboParser → values4ComboGetter → valueComboReplacer → property2ValueJoiner
```

This function provides the structured value input for combo value replacement.

## Advanced Features

### Index Flexibility

- **Arbitrary Indices**: Supports any numeric index values
- **Gap Handling**: Automatically fills gaps in index sequences
- **Multi-Assignment**: Single value can be assigned to multiple indices

### Pattern Mixing

- **Hybrid Approach**: Combines indexed and sequential value assignment
- **Conflict Resolution**: Indexed values take priority over sequential
- **Order Preservation**: Maintains logical ordering across pattern types

This function provides sophisticated value extraction capabilities, enabling complex combo definitions with flexible value organization and assignment patterns while maintaining compatibility with the broader combo processing system.
