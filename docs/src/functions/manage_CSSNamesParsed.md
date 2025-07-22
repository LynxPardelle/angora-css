# manage_CSSNamesParsed.ts

## Overview

Manages parsed CSS property names within the Angora CSS library, providing functionality to add, update, and retrieve CSS property name mappings. This module handles the translation between abbreviated property names and their full CSS equivalents, enabling the library's shorthand notation system.

## Purpose

- Add new CSS property name mappings dynamically
- Update existing property name translations
- Retrieve current CSS name parsing configurations
- Maintain consistency between property names and generated CSS
- Support real-time extension of property name system

## Core Functions

### pushCssNamesParsed(cssNamesParsed: any): void

**Parameters:**
- `cssNamesParsed`: Object containing CSS property name mappings

**Purpose:** Adds new CSS property name mappings to the system and triggers CSS regeneration.

**Process:**
1. Iterates through provided CSS name mappings
2. Merges new mappings with existing `values.cssNamesParsed`
3. Triggers full CSS regeneration to incorporate new mappings
4. Handles errors gracefully with comprehensive logging

**Integration:** Automatically regenerates all CSS to ensure new property names are available.

**Example Mappings:**
```javascript
{
  'm': 'margin',
  'p': 'padding',
  'bg': 'background',
  'w': 'width',
  'h': 'height'
}
```

### getCssNamesParsed(): any

**Returns:** Current CSS names parsed object from singleton

**Purpose:** Retrieves the complete set of CSS property name mappings currently configured.

**Features:**
- Logs current state for debugging
- Provides read-only access to property name mappings
- Enables inspection of current translation configuration
- Useful for development and debugging

**Use Cases:**
- Debugging property name translation issues
- Inspecting available property abbreviations
- Development and testing
- System state validation

### updateCssNamesParsed(cssNameParsed: string, value: string): void

**Parameters:**
- `cssNameParsed`: Name of the CSS property mapping to update
- `value`: New CSS property name value

**Purpose:** Updates an existing CSS property name mapping and regenerates affected classes.

**Process:**
1. Validates that the CSS property name mapping exists
2. Updates the mapping with the new value
3. Identifies all created classes that use this property name
4. Regenerates CSS only for affected classes
5. Throws descriptive error if property name doesn't exist

**Efficiency:** Only regenerates CSS for classes that actually use the updated property name.

**Error Handling:**
- Validates existence before updating
- Provides specific error messages
- Logs all errors for debugging

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`
- `cssCreate` from `./cssCreate`

## CSS Property Name System

### Property Name Mappings

The system maintains mappings between abbreviated and full CSS property names:

**Common Mappings:**
- `m` → `margin`
- `mt` → `margin-top`
- `mr` → `margin-right`
- `mb` → `margin-bottom`
- `ml` → `margin-left`
- `p` → `padding`
- `pt` → `padding-top`
- `bg` → `background`
- `w` → `width`
- `h` → `height`

### Translation Process

1. Class names are parsed for property abbreviations
2. Abbreviations are looked up in `cssNamesParsed`
3. Full CSS property names are used in generated CSS
4. System maintains consistency across all generations

## State Management

### Singleton Integration
- All property name data stored in ValuesSingleton
- Global consistency across library
- Centralized property name management

### Automatic CSS Regeneration
- Tracks which classes use specific property names
- Regenerates affected CSS when mappings change
- Maintains real-time consistency

### Class Dependency Tracking
- Uses `values.alreadyCreatedClasses` to track dependencies
- Enables selective CSS regeneration
- Prevents unnecessary processing

## Integration Points

### With CSS Generation
- Core integration with CSS property name resolution
- Enables abbreviation expansion during CSS creation
- Maintains consistency between abbreviations and CSS

### With Class Parsing
- Used during class name parsing to resolve property names
- Enables shorthand notation throughout the system
- Supports complex property name patterns

### With Debug System
- Comprehensive logging for all property name operations
- Error tracking and reporting
- State inspection capabilities

## Performance Optimizations

### Selective Regeneration
- Only regenerates CSS for affected classes
- Avoids full CSS rebuilds when possible
- Maintains optimal performance for updates

### Efficient Lookup
- Fast object-based property name lookup
- Minimal processing overhead
- Optimized for frequent property name resolution

### Batch Operations
- Supports bulk property name additions
- Minimizes CSS regeneration cycles
- Optimizes for multiple simultaneous updates

## Error Handling

### Validation
- Validates property name existence before updates
- Provides descriptive error messages
- Prevents invalid operations

### Graceful Recovery
- Continues operation despite individual errors
- Comprehensive error logging
- Non-blocking error handling

### System Integrity
- Maintains property name system consistency
- Prevents partial update states
- Ensures reliable property name resolution

## Usage Patterns

### Adding Property Names
```javascript
// Add new property name mappings
manage_CSSNamesParsed.pushCssNamesParsed({
  'br': 'border-radius',
  'bs': 'box-shadow',
  'ta': 'text-align',
  'fs': 'font-size'
});
```

### Updating Property Names
```javascript
// Update existing property name mapping
manage_CSSNamesParsed.updateCssNamesParsed('m', 'margin');
```

### Retrieving Property Names
```javascript
// Get all current property name mappings
const mappings = manage_CSSNamesParsed.getCssNamesParsed();
console.log('Available property mappings:', mappings);
```

## Advanced Features

### Dynamic Extension
- Supports runtime property name system extension
- Enables plugin-like functionality for new properties
- Maintains backward compatibility

### Live Updates
- Real-time property name mapping updates
- Automatic CSS regeneration for consistency
- Supports hot-reloading scenarios

### Complex Mappings
- Supports any CSS property name mapping
- Handles vendor prefixes and custom properties
- Flexible mapping system for various CSS features

## Development Support

### Debug Capabilities
- Comprehensive logging for all operations
- State inspection for troubleshooting
- Error tracking for development

### System Inspection
- Easy access to current property name configurations
- Visibility into property name resolution process
- Development-friendly debugging features

## Integration Examples

### Class Generation
```javascript
// Class "m-10" uses property name "m"
// System looks up "m" → "margin"
// Generates: .m-10 { margin: 10px; }
```

### Property Name Resolution
```javascript
// During CSS generation:
// 1. Parse class name for property abbreviation
// 2. Look up in cssNamesParsed
// 3. Use full property name in CSS
// 4. Generate valid CSS rule
```

## Notes

- Essential for the library's property name abbreviation system
- Provides dynamic extension capabilities for CSS properties
- Optimizes CSS regeneration for performance
- Maintains system consistency automatically
- Supports both individual and bulk operations
- Comprehensive error handling and validation
- Integrates seamlessly with CSS generation pipeline
- Enables flexible and extensible property name management
