# createSimpleRule.ts

## Overview

Private utility function that creates and inserts CSS rules into the stylesheet, handling both simple CSS rules and complex media query rules. This function manages rule parsing, conflict resolution, and proper insertion into the global stylesheet while maintaining rule order and media query structure.

## Purpose

- Parse and process CSS rule strings for insertion
- Handle both simple CSS rules and media query rules
- Manage rule conflicts and replacements within media queries
- Insert rules into appropriate locations in the stylesheet
- Maintain proper CSS rule structure and hierarchy

## Core Functionality

### createSimpleRule(rule: string): void

**Parameters:**
- `rule`: CSS rule string to parse and insert

**Purpose:** Processes a CSS rule string and inserts it into the global stylesheet with intelligent conflict resolution.

**Process:**
1. **Rule Parsing**: Splits rule string into components using separators
2. **Media Query Detection**: Identifies if rule contains media query syntax
3. **Conflict Resolution**: Checks for existing rules and removes conflicts
4. **Rule Insertion**: Inserts new rule at appropriate location
5. **Structure Maintenance**: Preserves CSS hierarchy and organization

## Rule Processing Architecture

### String Parsing

**Preprocessing Steps:**
```typescript
rule
  .replace(/{/g, values.separator)
  .replace(/}/g, values.separator)
  .split(values.separator)
  .filter((r) => r !== "")
  .map((r) => r.replace(/\n/g, "").replace(/\s{2}/g, ""))
```

**Parsing Operations:**
- Replaces braces with separators for consistent splitting
- Splits into rule components
- Filters empty segments
- Cleans whitespace and newlines
- Normalizes rule formatting

### Media Query Handling

**Detection Logic:**
- Checks if first rule component contains "media"
- Extracts media query selector
- Processes rules within media query context
- Maintains media query structure

**Media Query Processing:**
1. Identifies existing media queries in stylesheet
2. Checks for matching media query rules
3. Handles rule conflicts within media query context
4. Inserts rules into appropriate media query block

## Conflict Resolution

### Rule Replacement Strategy

**Within Media Queries:**
1. Searches existing CSS rules for conflicts
2. Identifies rules with matching selectors
3. Removes conflicting rules using `deleteRule()`
4. Inserts new rule at end of media query block
5. Maintains rule order and hierarchy

**Conflict Detection:**
```typescript
[...css.cssRules].some((cssRule: any, ix: number) => {
  if (cssRule.cssText.includes(rulesParsed[i])) {
    index = ix;
    return true;
  }
})
```

### Rule Insertion

**Media Query Rules:**
- Processes rules in pairs (selector + declarations)
- Creates complete rule string: `${selector}{${declarations}}`
- Inserts into existing media query block
- Maintains proper CSS syntax

**Simple Rules:**
- Direct insertion into main stylesheet
- Appends to end of stylesheet
- Preserves rule order

## Dependencies

- `ValuesSingleton` from `../../singletons/valuesSingleton`
- `console_log` from `../console_log`

## State Management

### Stylesheet Integration
- Direct manipulation of `values.sheet` (CSSStyleSheet)
- Uses `insertRule()` and `deleteRule()` methods
- Maintains stylesheet integrity throughout process

### Rule Tracking
- Processes rules systematically
- Maintains insertion order
- Handles duplicate rule scenarios

## Error Handling

### Safe Operations
- Filters empty rule segments
- Handles malformed CSS gracefully
- Continues processing despite individual rule errors

### Debug Support
- Comprehensive logging for rule processing
- Logs new rules before insertion
- Provides visibility into rule creation process

## Performance Considerations

### Efficient Processing
- Minimal string operations
- Direct stylesheet manipulation
- Optimized rule conflict detection

### Memory Management
- No memory leaks in rule processing
- Efficient rule replacement strategy
- Minimal object creation

## Integration Points

### With CSS Generation Pipeline
- Called by `manage_CSSRules` for simple rule processing
- Integrates with media query creation workflow
- Maintains consistency with overall CSS generation

### With Stylesheet Management
- Direct integration with global stylesheet
- Coordinates with other rule creation functions
- Maintains stylesheet organization

## Usage Context

### Rule Types Handled

**Simple CSS Rules:**
```css
.class-name { property: value; }
```

**Media Query Rules:**
```css
@media (min-width: 768px) {
  .class-name { property: value; }
}
```

### Processing Flow

**For Simple Rules:**
1. Parse rule string
2. Insert directly into stylesheet
3. Log insertion for debugging

**For Media Query Rules:**
1. Parse media query and rule components
2. Find or create appropriate media query block
3. Handle conflicts within media query
4. Insert rules maintaining structure

## Advanced Features

### Rule Normalization
- Consistent formatting across all rules
- Whitespace and newline cleanup
- Proper CSS syntax maintenance

### Conflict Management
- Intelligent duplicate rule detection
- Automatic rule replacement
- Maintains most recent rule versions

### Structure Preservation
- Maintains media query hierarchy
- Preserves rule organization
- Ensures valid CSS output

## Debug and Development

### Comprehensive Logging
- Logs rule processing steps
- Provides visibility into conflict resolution
- Supports troubleshooting and optimization

### Development Support
- Clear processing flow for debugging
- Error isolation and handling
- Performance monitoring capabilities

## Notes

- Essential component of CSS rule creation pipeline
- Handles complex media query rule insertion
- Provides intelligent conflict resolution
- Maintains stylesheet integrity and organization
- Optimized for performance and reliability
- Private utility focused on core CSS manipulation
- Integrates seamlessly with broader CSS generation system
