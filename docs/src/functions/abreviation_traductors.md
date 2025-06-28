# abreviation_traductors.ts

## Overview

Provides abbreviation translation functions that convert between abbreviated and full forms of CSS property names and values. This module enables the library's shorthand notation system by translating between human-readable abbreviations and full CSS syntax.

## Purpose

- Translates abbreviated CSS property names to full names
- Converts full CSS property names back to abbreviations
- Supports bidirectional translation with regular expressions
- Enables consistent abbreviation usage across the library

## Functions

### abreviationTraductor(value, type?)

**Parameters:**
- `value`: String to translate
- `type`: Translation direction ("traduce" | "convert"), defaults to "traduce"

**Returns:** Translated string

**Purpose:** Core translation function that handles bidirectional abbreviation conversion.

**Process:**
1. Logs the original value for debugging
2. Iterates through all abbreviation translators in the singleton
3. Applies appropriate regular expression replacements based on type
4. Logs the final translated value
5. Returns the translated result

**Translation Types:**
- `"traduce"`: Converts abbreviations to full forms (default)
- `"convert"`: Converts full forms back to abbreviations

### unbefysize(value)

**Parameters:**
- `value`: String containing abbreviations to expand

**Returns:** String with abbreviations translated to full forms

**Purpose:** Convenience function to expand abbreviations to full CSS syntax.

**Usage:** Commonly used when generating CSS rules from abbreviated class names.

### befysize(value)

**Parameters:**
- `value`: String containing full forms to abbreviate

**Returns:** String with full forms converted to abbreviations

**Purpose:** Convenience function to convert full CSS syntax to abbreviated forms.

**Usage:** Used for optimization and creating compact representations.

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`

## Abbreviation Translation System

### Translation Rules

The system uses regular expressions defined in `values.abreviationTraductors`:

```typescript
interface AbreviationTraductor {
  abreviation: string;
  abreviationRegExp: RegExp;
  traduction: string;
  traductionRegExp: RegExp;
}
```

### Bidirectional Translation

**Forward Translation (traduce):**
- Uses `abreviationRegExp` to find abbreviations
- Replaces with `traduction` (full form)
- Example: "m-10" → "margin: 10px"

**Reverse Translation (convert):**
- Uses `traductionRegExp` to find full forms
- Replaces with `abreviation` (abbreviated form)
- Example: "margin: 10px" → "m-10"

## Integration Points

### With CSS Generation
- Used during class parsing to expand abbreviations
- Enables generation of valid CSS from abbreviated class names
- Supports complex abbreviation patterns

### With Class Parsing
- Integrated into class processing pipeline
- Handles nested abbreviations and complex patterns
- Maintains consistency across different abbreviation types

### With Debug System
- Logs before and after values for debugging
- Provides visibility into translation process
- Helps troubleshoot abbreviation issues

## Usage Patterns

### CSS Generation
```javascript
// Expand abbreviations for CSS generation
const expanded = unbefysize("m-10 p-5");
// Result: full CSS property syntax
```

### Optimization
```javascript
// Convert to abbreviations for compact storage
const abbreviated = befysize("margin: 10px; padding: 5px;");
// Result: abbreviated form
```

### Debug Mode
When debug mode is enabled, the functions log:
- Original input values
- Final output values
- Translation steps for troubleshooting

## Regular Expression Processing

### Pattern Matching
- Uses compiled regular expressions for efficiency
- Supports complex pattern matching
- Handles edge cases and special characters

### Performance Optimization
- Regular expressions are pre-compiled in singleton
- Single pass through abbreviation list
- Efficient string replacement operations

## Error Handling

### Input Validation
- Handles undefined values gracefully
- Returns original value if no translations apply
- Non-blocking error handling

### Debug Information
- Comprehensive logging for troubleshooting
- Visibility into translation process
- Performance monitoring capabilities

## Extensibility

### Adding New Abbreviations
New abbreviation rules can be added to the singleton's `abreviationTraductors` array:

```typescript
values.abreviationTraductors.push({
  abreviation: "newAbbr",
  abreviationRegExp: /pattern/g,
  traduction: "full-form",
  traductionRegExp: /full-pattern/g
});
```

### Custom Translation Logic
The modular design allows for:
- Custom translation functions
- Extended pattern matching
- Specialized abbreviation handling

## State Management

### Singleton Integration
- Abbreviation rules stored in ValuesSingleton
- Consistent translation across library
- Global access to translation patterns

### Stateless Operations
- Functions are stateless and pure
- No side effects beyond logging
- Safe for concurrent usage

## Performance Considerations

### Efficient Processing
- Single pass through abbreviation rules
- Pre-compiled regular expressions
- Minimal string allocations

### Caching Potential
- Results could be cached for repeated translations
- Pattern matching optimization
- Memory-efficient operation

## Notes

- Essential for the library's abbreviation system
- Provides bidirectional translation capabilities
- Integrates seamlessly with CSS generation pipeline
- Supports complex abbreviation patterns
- Designed for performance and extensibility
- Comprehensive debug support for development
