# commonPropertiesValuesAbreviations.ts

## Overview

Defines a comprehensive mapping of abbreviated CSS property values to their full CSS values. This file provides shorthand notation for common CSS values, enabling faster development and consistent value usage across the library.

## Purpose

- Provides abbreviated CSS property values for rapid development
- Maps shorthand notation to standard CSS values
- Ensures consistent value usage across the library
- Reduces typing and potential errors in CSS value specification

## Structure

The `commonPropertiesValuesAbreviations` object contains mappings in the format:
```typescript
{
  "ABBREVIATION": "full-css-value"
}
```

## Value Categories

### Position Values
Position-related CSS values for the `position` property:
- `ABS`: "absolute" - Absolute positioning
- `REL`: "relative" - Relative positioning  
- `FIX`: "fixed" - Fixed positioning
- `STA`: "static" - Static positioning (default)
- `STI`: "sticky" - Sticky positioning

### Display Values
Display-related CSS values for the `display` property:
- `BLO`: "block" - Block display
- `INL`: "inline" - Inline display
- `IBL`: "inline-block" - Inline-block display
- `FLX`: "flex" - Flexbox container
- `GRI`: "grid" - Grid container
- `NON`: "none" - No display
- `TAB`: "table" - Table display
- `TAC`: "table-cell" - Table cell display
- `TAR`: "table-row" - Table row display
- `CNT`: "contents" - Contents display
- `LST`: "list-item" - List item display
- `IFL`: "inline-flex" - Inline flex container
- `IGR`: "inline-grid" - Inline grid container
- `ITB`: "inline-table" - Inline table display

### Flexbox/Grid Alignment Values
Values for flexbox and grid alignment properties:
- `FST`: "flex-start" - Flex start alignment
- `FEN`: "flex-end" - Flex end alignment
- `CEN`: "center" - Center alignment
- `SBE`: "space-between" - Space between items
- `SAR`: "space-around" - Space around items
- `SEV`: "space-evenly" - Space evenly distributed
- `STR`: "stretch" - Stretch to fill
- `BAS`: "baseline" - Baseline alignment

### Flex Direction Values
Values for `flex-direction` property:
- `COL`: "column" - Column direction
- `ROW`: "row" - Row direction
- `CRE`: "column-reverse" - Reverse column
- `RRE`: "row-reverse" - Reverse row

### Flex Wrap Values
Values for `flex-wrap` property:
- `WRA`: "wrap" - Allow wrapping
- `NOW`: "nowrap" - No wrapping
- `WRE`: "wrap-reverse" - Reverse wrapping

### Directional Values
Common directional values:
- `JUS`: "justify" - Justify alignment
- `SRT`: "start" - Start position
- `END`: "end" - End position
- `LEF`: "left" - Left position
- `RIG`: "right" - Right position
- `TOP`: "top" - Top position
- `BOT`: "bottom" - Bottom position

## Usage in Library

### CSS Class Generation
These abbreviations are used during CSS generation to:
1. Recognize abbreviated values in class strings
2. Convert them to proper CSS values
3. Generate valid CSS rules

### Value Validation
The mappings serve as a validation system:
- Ensures only recognized abbreviated values are used
- Provides consistent value translation
- Prevents invalid CSS value generation

### Developer Experience
Enables developers to use:
- Shorter class names with abbreviated values
- Consistent abbreviation patterns
- Familiar shorthand notation

## Integration Points

### With Color Validation
Used during color validation to:
- Prevent conflicts between color names and value abbreviations
- Ensure color names don't override value abbreviations
- Maintain system integrity

### With Class Parsing
Integrated into class parsing to:
- Translate abbreviated values to full CSS values
- Generate proper CSS syntax
- Support complex class combinations

### With CSS Generation
Used in CSS rule creation to:
- Expand abbreviated values
- Generate valid CSS declarations
- Support responsive and pseudo-class variants

## Naming Conventions

### Abbreviation Patterns
The abbreviation system follows consistent patterns:
- **Three-letter codes**: Most abbreviations use 3 characters (ABS, REL, FLX)
- **Logical groupings**: Related values use similar prefixes
- **Uppercase format**: All abbreviations are uppercase for distinction
- **Mnemonic basis**: Abbreviations are based on recognizable parts of the full value

### Value Categories
Abbreviations are organized by CSS property type:
- Position values for `position` property
- Display values for `display` property
- Alignment values for flexbox/grid properties
- Direction values for layout properties

## Extensibility

### Adding New Abbreviations
New value abbreviations can be easily added:
```typescript
export const commonPropertiesValuesAbreviations = {
  // existing abbreviations...
  "NEW": "new-css-value",
  "CUS": "custom-value"
};
```

### Category Expansion
New categories of values can be added following existing patterns:
- Consistent three-letter abbreviations
- Logical grouping by CSS property
- Clear mnemonic relationships

## Performance Considerations

### Lookup Efficiency
- Object literal provides O(1) lookup time
- No complex processing required
- Memory-efficient storage

### Build Optimization
- Static object structure
- Tree-shaking friendly
- Minimal runtime overhead

## Validation Features

### Conflict Prevention
Designed to prevent conflicts with:
- Color names defined in colors.ts
- CSS property abbreviations
- Custom user-defined values

### Case Sensitivity
- Uses uppercase for all abbreviations
- Distinguishes from lowercase property abbreviations
- Provides clear visual distinction

## Browser Compatibility

### Standard CSS Values
- Uses only standard CSS property values
- Compatible with all modern browsers
- Follows CSS specification standards

### Fallback Support
- Provides commonly supported values
- Avoids experimental or vendor-specific values
- Ensures broad browser compatibility

## Development Benefits

### Faster Development
- Reduces typing for common values
- Minimizes errors in value specification
- Provides consistent value usage

### Code Readability
- Makes class names more concise
- Provides recognizable abbreviation patterns
- Maintains semantic meaning

### Maintenance
- Centralized value definition
- Easy to update or extend
- Consistent across the library

## Notes

- Essential for the library's value abbreviation system
- Provides comprehensive coverage of common CSS values
- Balances brevity with clarity
- Designed for easy extension and maintenance
- Follows consistent naming patterns
- Integrates seamlessly with the broader abbreviation system
- Supports rapid CSS development with abbreviated notation
