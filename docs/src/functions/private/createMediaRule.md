# createMediaRule.ts

## Overview

Private utility function that creates and manages media query CSS rules within the stylesheet. This function handles the insertion of media query rules while managing conflicts and maintaining proper CSS rule organization within the global stylesheet.

## Purpose

- Create and insert media query CSS rules into the stylesheet
- Handle conflicts with existing media query rules
- Manage media query rule replacement and updates
- Maintain proper CSS rule structure and organization
- Ensure valid media query syntax in the stylesheet

## Core Functionality

### createMediaRule(rule: string): void

**Parameters:**
- `rule`: Media query CSS rule string to insert

**Purpose:** Inserts media query rules into the global stylesheet with conflict resolution.

## Processing Pipeline

### 1. Existing Rule Detection

**Conflict Detection:**
```typescript
let originalRule = [...values.sheet.cssRules].some((cssRule, i) => {
  if (cssRule.cssText.includes(
    rule.split("{")[0].replace("\n", "").replace(/\s+/g, " ")
  )) {
    index = i;
    return true;
  }
});
```

**Detection Features:**
- Searches existing CSS rules for matching media query selectors
- Normalizes whitespace and newlines for accurate comparison
- Extracts media query selector from rule string
- Identifies rule index for potential replacement

### 2. Rule Normalization

**Selector Extraction:**
- Splits rule on opening brace to get selector
- Removes newline characters for clean comparison
- Normalizes multiple spaces to single spaces
- Ensures consistent selector formatting

**Comparison Logic:**
```typescript
aC.replace(".", "") === rule.split("{")[0].replace("\n", "").replace(/\s+/g, " ")
```

### 3. Conflict Resolution

**Rule Replacement:**
```typescript
if (originalRule) {
  values.sheet.deleteRule(index);
}
```

**Resolution Process:**
- Removes existing conflicting rule if found
- Prevents duplicate media query rules
- Maintains stylesheet integrity
- Ensures most recent rule takes precedence

### 4. Rule Insertion

**Final Insertion:**
```typescript
values.sheet.insertRule(rule, values.sheet.cssRules.length);
```

**Insertion Features:**
- Appends rule to end of stylesheet
- Maintains rule order and precedence
- Ensures valid CSS syntax
- Preserves media query structure

## Dependencies

- `ValuesSingleton` from `../../singletons/valuesSingleton`
- `console_log` from `../console_log`

## Integration Points

### With CSS Generation Pipeline
- Called by CSS rule management system for media queries
- Handles specialized media query insertion logic
- Integrates with overall CSS rule creation workflow
- Maintains consistency with simple rule creation

### With Stylesheet Management
- Direct manipulation of global stylesheet (`values.sheet`)
- Coordinates with other rule creation functions
- Maintains stylesheet organization and structure
- Ensures proper CSS rule lifecycle management

## Media Query Handling

### Rule Structure
- Handles complete media query rules with selectors and declarations
- Supports complex media query syntax
- Maintains proper CSS media query formatting
- Preserves responsive design functionality

### Conflict Management
- Identifies matching media query selectors
- Removes outdated or conflicting rules
- Ensures only current rules remain active
- Maintains clean stylesheet without duplicates

## Performance Considerations

### Efficient Rule Detection
- Single pass through existing CSS rules
- Optimized string comparison operations
- Minimal regular expression usage
- Fast conflict detection logic

### Memory Management
- No memory leaks in rule processing
- Efficient array operations for rule iteration
- Minimal object creation during processing
- Clean rule replacement without accumulation

## Error Handling

### Safe Operations
- Handles missing or malformed rules gracefully
- Continues processing despite individual rule errors
- Maintains stylesheet integrity during failures
- Provides debug logging for troubleshooting

### Debug Support
- Logs rule content before insertion
- Provides visibility into rule processing
- Supports troubleshooting media query issues
- Enables development debugging

## Usage Context

### Media Query Generation
```javascript
// Insert responsive CSS rule
createMediaRule(`@media (min-width: 768px) {
  .responsive-class { display: block; }
}`);
```

### Responsive Design
```javascript
// Handle breakpoint-specific styling
createMediaRule(`@media (max-width: 576px) {
  .mobile-hidden { display: none; }
}`);
```

## Rule Examples

### Basic Media Query
```css
@media (min-width: 768px) {
  .md-visible { display: block; }
}
```

### Complex Media Query
```css
@media screen and (min-width: 1024px) and (max-width: 1440px) {
  .desktop-specific { font-size: 18px; }
}
```

### Device-Specific Query
```css
@media (orientation: landscape) {
  .landscape-layout { flex-direction: row; }
}
```

## Advanced Features

### Selector Normalization
- Handles various whitespace patterns in selectors
- Normalizes rule format for accurate comparison
- Supports complex selector structures
- Maintains CSS validity throughout processing

### Rule Precedence
- Ensures latest rules take precedence
- Maintains proper CSS cascade order
- Handles rule replacement efficiently
- Preserves responsive design behavior

### Conflict Prevention
- Prevents duplicate media query rules
- Maintains clean stylesheet structure
- Ensures predictable CSS behavior
- Optimizes stylesheet performance

## Notes

- Essential for responsive design support in the library
- Handles complex media query rule management
- Provides conflict resolution for media query rules
- Maintains proper CSS structure and organization
- Integrates seamlessly with global stylesheet management
- Optimized for performance with efficient rule processing
- Critical component of responsive CSS generation system
