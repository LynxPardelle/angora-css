# comboParser.ts

## Overview

Private utility function that processes CSS class combinations (combos) by parsing combo definitions, applying value replacements, and managing combo abbreviations with encryption. This function handles complex combo processing including pseudo-class integration and dynamic class generation.

## Purpose

- Parse and process CSS class combinations from combo definitions
- Apply value replacements to combo templates using extracted values
- Manage combo abbreviations with optional encryption
- Handle pseudo-class integration within combo structures
- Generate new classes for combo components and track them

## Core Functionality

### comboParser(class2Create, comb, class2CreateElement, classes2Create): Promise<string[]>

**Parameters:**
- `class2Create`: Base class name being processed
- `comb`: Combo identifier/key from combo definitions
- `class2CreateElement`: DOM element to apply classes to
- `classes2Create`: Array of classes being accumulated

**Returns:** Promise resolving to updated classes2Create array

**Purpose:** Processes combo definitions and generates appropriate CSS classes with value substitution and abbreviation management.

## Processing Pipeline

### 1. Combo Resolution

**Combo Lookup:**
```typescript
let combIndex = comb ? Object.keys(values.combos).indexOf(comb) : -1;
```

**Value Extraction:**
- Gets values from the base class using `values4ComboGetter()`
- Extracts relevant values for substitution in combo templates
- Prepares value context for combo processing

### 2. Combo Processing Loop

**Template Processing:**
```typescript
await Promise.all(
  values.combos[comb].map(async (c: string) => {
    c = await valueComboReplacer(c, vals);
    // Further processing...
  })
);
```

**Processing Steps:**
1. Applies value replacement to combo templates
2. Handles special class indicators and abbreviations
3. Processes pseudo-class integration
4. Manages class addition to DOM element

### 3. Abbreviation Management

**Combo Encryption System:**
```typescript
let combCreatedKey = combosCreatedKeys.find((cs) => {
  return values.combosCreated[cs] === class2Create;
}) || values.encryptComboCharacters + combosCreatedKeys.length;
```

**Abbreviation Features:**
- Creates unique abbreviations for combo classes
- Supports encryption mode for shortened class names
- Tracks already created combo abbreviations
- Prevents duplicate abbreviation generation

### 4. Pseudo-Class Integration

**Pseudo-Class Detection:**
```typescript
let pseudos = values.pseudos.filter((p: any) =>
  c.split("-")[1].includes(p.mask)
);
```

**Integration Logic:**
- Detects pseudo-classes within combo templates
- Handles pseudo-class positioning and precedence
- Integrates combo abbreviations with pseudo-class syntax
- Manages complex selector patterns

## Combo Processing Modes

### Standard Class Processing
- Direct class addition to element
- No abbreviation or special processing
- Simple combo component handling

### Indicator Class Processing
- Classes starting with `values.indicatorClass`
- Triggers abbreviation generation
- Applies combo encryption if enabled
- Handles complex selector patterns

### Pseudo-Class Integration
- Integrates pseudo-classes with combo abbreviations
- Maintains proper selector syntax
- Handles multiple pseudo-class scenarios
- Preserves pseudo-class precedence

## Abbreviation System

### Combo Abbreviation Creation

**Key Generation:**
```typescript
let comboABBR = values.encryptCombo ? combCreatedKey : class2Create;
```

**Abbreviation Types:**
- **Encrypted**: Uses generated abbreviation characters
- **Plain**: Uses original class name
- **Incremental**: Appends numbers for uniqueness

### Tracking and Storage
- Stores abbreviations in `values.combosCreated`
- Prevents duplicate abbreviation creation
- Maintains mapping between abbreviations and original classes
- Supports lookup and reverse lookup

## Selector Pattern Management

### SEL Token Processing

**Pattern Types:**
1. **Pseudo-class with SEL**: `SEL__COM_{abbr}{pseudo}`
2. **SEL only**: `SEL__COM_{abbr}__`
3. **No SEL**: Appends `SEL__COM_{abbr}` to class

**Selector Examples:**
```css
.class-hover → .classSEL__COM_abbr:hover
.class-focus → .classSEL__COM_abbr:focus
.class-active → .classSEL__COM_abbr:active
```

## Dependencies

- `ValuesSingleton` - Global state and combo definitions
- `console_log` - Debug logging
- `valueComboReplacer` - Value substitution in templates
- `values4ComboGetter` - Value extraction from classes

## Integration Points

### With Combo System
- Processes combo definitions from singleton
- Integrates with combo value replacement system
- Manages combo abbreviation lifecycle

### With Pseudo-Class System
- Integrates pseudo-class detection and processing
- Maintains pseudo-class syntax and precedence
- Handles complex selector combinations

### With DOM Manipulation
- Directly adds classes to DOM elements
- Maintains element class list integrity
- Supports dynamic class application

## Error Handling

### Robust Processing
- Handles missing combo definitions gracefully
- Continues processing despite individual combo failures
- Maintains class list integrity

### Debug Support
- Comprehensive logging throughout the process
- Logs combo processing steps
- Provides visibility into abbreviation generation

## Performance Considerations

### Asynchronous Processing
- Uses `Promise.all()` for parallel combo processing
- Optimizes value replacement operations
- Efficient abbreviation lookup and generation

### Memory Efficiency
- Reuses existing abbreviations when possible
- Minimizes abbreviation storage overhead
- Efficient array and object operations

## Usage Context

### Combo Processing
```javascript
// Process combo for button component
const updatedClasses = await comboParser(
  'btn-primary',
  'button-combo',
  buttonElement,
  existingClasses
);
```

### Integration with CSS Generation
- Called during class processing pipeline
- Generates additional classes from combo definitions
- Maintains class relationship tracking

## Advanced Features

### Encryption Support
- Optional combo abbreviation encryption
- Configurable encryption characters
- Maintains readability while reducing class name length

### Complex Selector Handling
- Supports nested pseudo-class combinations
- Handles special selector tokens (SEL)
- Maintains CSS selector validity

### Value Substitution
- Dynamic value replacement in combo templates
- Context-aware value extraction
- Support for complex value patterns

## Notes

- Essential for complex combo class processing
- Handles abbreviation generation and encryption
- Integrates pseudo-classes with combo system
- Optimized for performance with asynchronous processing
- Provides comprehensive debug logging
- Supports both simple and complex combo patterns
- Maintains CSS selector validity and syntax
