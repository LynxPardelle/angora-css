# css-camel.ts

## Overview

Utility functions for converting between CSS property naming conventions (kebab-case) and JavaScript property naming conventions (camelCase).

## Purpose

- Converts CSS property names to camelCase for JavaScript usage
- Converts camelCase property names back to CSS-valid kebab-case
- Handles both hyphen (-) and underscore (_) separators
- Enables seamless interaction between CSS and JavaScript naming conventions

## Functions

### cssValidToCamel(st)

**Parameters:**
- `st`: String in CSS-valid format (kebab-case or snake_case)

**Returns:** String in camelCase format

**Purpose:** Converts CSS property names to camelCase for JavaScript usage.

**Examples:**
- `"background-color"` → `"backgroundColor"`
- `"font-size"` → `"fontSize"`
- `"border_width"` → `"borderWidth"`

**Process:**
1. Uses regular expression to find hyphen/underscore followed by a letter
2. Converts the found pattern to uppercase
3. Removes the separator character
4. Returns the camelCase result

### camelToCSSValid(st)

**Parameters:**
- `st`: String in camelCase format

**Returns:** String in CSS-valid kebab-case format

**Purpose:** Converts camelCase property names to CSS-valid format.

**Examples:**
- `"backgroundColor"` → `"background-color"`
- `"fontSize"` → `"font-size"`
- `"borderWidth"` → `"border-width"`

**Process:**
1. Uses regular expression to find lowercase letter followed by uppercase letter
2. Inserts a hyphen between them
3. Converts the entire string to lowercase
4. Returns the kebab-case result

## Use Cases

### JavaScript to CSS
When dynamically generating CSS properties from JavaScript objects:
```javascript
const styles = { backgroundColor: "red", fontSize: "16px" };
// Convert to CSS: background-color: red; font-size: 16px;
```

### CSS to JavaScript
When parsing CSS properties for JavaScript manipulation:
```javascript
const cssProperty = "background-color";
// Convert to: backgroundColor for JavaScript usage
```

### Framework Integration
For frameworks that need to convert between naming conventions:
- React inline styles (camelCase) to CSS (kebab-case)
- CSS-in-JS libraries
- Dynamic style generation

## Regular Expression Details

### cssValidToCamel Pattern
`/([-_][a-z])/gi`
- Matches hyphen or underscore followed by a lowercase letter
- Global and case-insensitive flags
- Captures the separator and following character

### camelToCSSValid Pattern
`/[\w]([A-Z])/g`
- Matches word character followed by uppercase letter
- Global flag for all occurrences
- Captures the transition point for separator insertion

## Dependencies

None - this is a pure utility module with no external dependencies.

## Performance Notes

- Uses efficient regular expressions for string transformation
- No loops or complex processing
- Suitable for high-frequency usage
- Memory efficient with minimal allocations

## Browser Compatibility

- Uses standard JavaScript string methods
- Compatible with all modern browsers
- No special browser features required

## Usage Patterns

This module is used throughout the library for:
- CSS property name transformations
- Style object processing
- Dynamic CSS generation
- Framework compatibility layers

## Notes

- Handles both hyphen and underscore separators in input
- Output is always hyphen-separated for CSS compatibility
- Case transformations are handled correctly
- Suitable for both single properties and bulk processing
