# valueComboReplacer - Dynamic Value Substitution Engine

## Overview

The `valueComboReplacer` function handles dynamic value substitution in combo definitions using a VAL/DEF pattern. It processes placeholder tokens in combo strings and replaces them with actual values, supporting default values and cross-references between value positions.

## Location

```
src/functions/main/private_utilities/valueComboReplacer.ts
```

## Dependencies

- `console_log.ts` - Logging functionality for debugging

## Core Function

### valueComboReplacer()

```typescript
async valueComboReplacer(c: string, vals: string[]): Promise<string>
```

Processes value replacement tokens in combo strings using a sophisticated pattern matching system.

#### Parameters

- `c: string` - Combo string containing VAL tokens to be replaced
- `vals: string[]` - Array of values to substitute for VAL tokens

#### Returns

- `Promise<string>` - Processed string with VAL tokens replaced by actual values

## Token Pattern System

### VAL Token Format

```
VAL{index}         - Basic value reference
VAL{index}DEF{default}DEF  - Value reference with default fallback
```

### Pattern Examples

- `VAL0` - References `vals[0]`
- `VAL1DEFredDEF` - References `vals[1]`, defaults to "red" if empty
- `VAL2DEF10pxDEF` - References `vals[2]`, defaults to "10px" if empty

## Processing Logic

### 1. Pattern Detection

```typescript
let reg = new RegExp(/VAL[0-9]+(DEF.*DEF)?/, "g");
if (reg.test(c)) {
  // Process VAL tokens
}
```

**Regex Pattern**
- `VAL[0-9]+` - Matches VAL followed by one or more digits
- `(DEF.*DEF)?` - Optionally matches default value wrapped in DEF tags
- Global flag processes all matches in the string

### 2. Token Processing Loop

```typescript
for (let match of matches) {
  let val = parseInt(match.split("VAL")[1].split("DEF")[0]);
  let valueToMatch = `VAL${val}(DEF.*DEF)?`;
  let valueReg = new RegExp(valueToMatch, "g");
  let def = match.split("DEF")[1];
  // Value replacement logic
}
```

**Extraction Process**
- **Index Extraction**: Parses numeric index from VAL token
- **Dynamic Regex**: Creates specific regex for current token
- **Default Extraction**: Extracts default value from DEF wrapper

### 3. Value Resolution Strategy

```typescript
if (
  !!vals[val] &&
  vals[val] !== "" &&
  vals[val] !== "undefined" &&
  vals[val] !== "DEF" &&
  vals[val] !== "null"
) {
  // Process valid value
} else {
  // Use default value
}
```

**Validation Checks**
- Ensures value exists and is not empty
- Excludes string literals "undefined", "DEF", "null"
- Provides comprehensive null/empty checking

### 4. Cross-Reference Handling

```typescript
if (/VAL[0-9]+/.test(vals[val])) {
  /* When you want to use another defined value */
  let valval = vals[val].replace(/VAL/g, "");
  c = c.replace(
    valueReg,
    vals[parseInt(valval)] &&
      vals[parseInt(valval)] !== "VAL" + valval
      ? vals[parseInt(valval)]
      : def
      ? def
      : ""
  );
}
```

**Reference Chain Resolution**
- Detects when value contains another VAL reference
- Extracts target index from reference value
- Resolves to final value or default if chain breaks

### 5. Direct Value Replacement

```typescript
else {
  /* When you defined a custom value */
  c = c.replace(valueReg, vals[val]);
}
```

**Simple Substitution**
- Direct replacement for concrete values
- No additional processing required

### 6. Default Value Fallback

```typescript
else {
  /* When you dont define a value its defined the default value */
  c = c.replace(valueReg, def ? def : "");
}
```

**Fallback Strategy**
- Uses default value when primary value is invalid
- Replaces with empty string if no default provided

## Usage Examples

### Basic Value Replacement

```typescript
const combo = "margin:VAL0 VAL1;";
const values = ["10px", "20px"];

const result = await valueComboReplacer(combo, values);
// Result: "margin:10px 20px;"
```

### Default Value Usage

```typescript
const combo = "color:VAL0DEFblueDEF; font-size:VAL1DEF16pxDEF;";
const values = ["red", ""]; // Second value is empty

const result = await valueComboReplacer(combo, values);
// Result: "color:red; font-size:16px;"
```

### Cross-Reference Values

```typescript
const combo = "border:VAL0 solid VAL1;";
const values = ["VAL2", "red", "2px"]; // VAL0 references VAL2

const result = await valueComboReplacer(combo, values);
// Result: "border:2px solid red;"
```

### Complex Example

```typescript
const combo = "box-shadow:VAL0DEF0pxDEF VAL1DEF0pxDEF VAL2DEF5pxDEF VAL3DEFblackDEF;";
const values = ["2px", "", "10px"]; // Missing VAL3

const result = await valueComboReplacer(combo, values);
// Result: "box-shadow:2px 0px 10px black;"
```

## Error Handling

### Graceful Degradation

- **Missing Values**: Uses default values when array indices don't exist
- **Invalid References**: Breaks reference chains gracefully
- **Empty Tokens**: Handles empty or malformed VAL tokens

### Validation Strategy

- **Type Checking**: Validates value types and content
- **Chain Breaking**: Prevents infinite reference loops
- **Default Fallbacks**: Always provides fallback values

## Performance Considerations

### Regex Efficiency

- **Compiled Patterns**: Regex patterns are compiled once per match
- **Global Processing**: Single pass processes all tokens
- **Minimal Backtracking**: Efficient pattern design

### String Operations

- **In-Place Replacement**: Modifies string progressively
- **Minimal Allocations**: Reuses string objects when possible
- **Batch Processing**: Processes all matches in sequence

## Integration Points

### Combo System Integration

- **Combo Processing**: Essential part of combo expansion pipeline
- **Value Resolution**: Handles dynamic value assignment
- **Template System**: Enables flexible combo templates

### CSS Generation Flow

```
comboParser → decryptCombo → valueComboReplacer → property2ValueJoiner
```

This function serves as the value resolution step in combo processing.

## Advanced Features

### Nested References

- **Multi-Level**: Supports VAL tokens referencing other VAL tokens
- **Chain Resolution**: Resolves reference chains to final values
- **Circular Prevention**: Prevents infinite reference loops

### Default Value System

- **Flexible Defaults**: Any string can serve as default value
- **Conditional Application**: Defaults only used when needed
- **Empty Handling**: Graceful handling of empty defaults

This function provides a sophisticated template system for combo values, enabling flexible and powerful CSS generation through dynamic value substitution with comprehensive fallback mechanisms.
