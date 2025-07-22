# colors.ts

## Overview

Defines the comprehensive color palette for the Angora CSS library, including default colors, Bootstrap colors, brand colors, and standard CSS colors. This file serves as the central color definition repository for the entire library.

## Purpose

- Provides a comprehensive color palette for CSS generation
- Supports multiple color schemes and design systems
- Enables consistent color usage across applications
- Includes brand-specific and standard web colors

## Color Categories

### Default Colors (Bootstrap-compatible)

Standard Bootstrap color palette for consistent UI design:

- `primary`: #0d6efd - Primary action color (Bootstrap blue)
- `secondary`: #6c757d - Secondary action color (muted gray)
- `success`: #198754 - Success state color (green)
- `info`: #0dcaf0 - Informational color (cyan)
- `warning`: #ffc107 - Warning state color (yellow)
- `danger`: #dc3545 - Error/danger state color (red)
- `light`: #f8f9fa - Light background color
- `dark`: #212529 - Dark text/background color

### Bootstrap Extended Colors

Additional Bootstrap colors for extended palette:

- `indigoBS`: #6610f2 - Bootstrap indigo
- `purpleBS`: #6f42c1 - Bootstrap purple
- `pinkBS`: #d63384 - Bootstrap pink
- `orangeBS`: #fd7e14 - Bootstrap orange
- `tealBS`: #20c997 - Bootstrap teal
- `white`: #fff - Pure white
- `grayBS`: #6c757d - Bootstrap gray

### Lynx Pardelle Colors

Custom color palette by Lynx Pardelle:

- `mystic`: #210020 - Deep mystical purple
- `lavenderLP`: #D6BCFF - Light lavender accent
- `fairy`: #D680FF - Bright fairy purple
- `summer`: #FF9A2E - Warm summer orange
- `old`: #EEEDA0 - Vintage pale yellow
- `friend`: #3BBBB2 - Friendly teal
- `tree`: #5A311D - Natural brown
- `blood`: #8A0707 - Deep blood red
- `beast`: #F5785D - Vibrant coral
- `abyss`: #000 - Pure black

### Angora Brand Colors

Brand-specific colors for Angora CSS:

- `ankcent`: #D01033 - Primary brand color (deep red)
- `secora`: #2D2824 - Secondary brand color (dark brown)
- `succank`: #5D4339 - Success brand color (medium brown)
- `bangrank`: #161B17 - Info brand color (dark green-gray)
- `secbank`: #F0B566 - Warning brand color (golden yellow)
- `dank`: #000000 - Danger brand color (black)
- `dankcent`: linear-gradient(220deg, #D01033 35%,#000000 55%) - Brand gradient
- `revdankcent`: linear-gradient(220deg, #000 35%,#D01033 55%) - Reverse brand gradient
- `ligthora`: #F4EBEC - Light brand color (pale pink)
- `dagora`: #100809 - Dark brand color (very dark brown)

### CSS Basic Colors

Complete set of standard CSS named colors including:

- Primary colors: black, white, red, green, blue
- Extended colors: silver, gray, maroon, purple, fuchsia, lime
- Additional web-safe colors: navy, olive, teal, aqua, yellow, and many more

## Color Format Support

### Hex Colors
All colors are defined in hexadecimal format for consistency and broad compatibility.

### Gradient Support
Includes CSS linear gradient definitions for complex brand colors.

### Named Color Standards
Follows CSS3 named color specifications for maximum compatibility.

## Usage in Library

### Color Management System
- Colors are loaded into ValuesSingleton for global access
- Used by color transformation functions
- Validated against abbreviations to prevent conflicts
- Support dynamic color updates and theme switching

### CSS Generation
- Referenced in dynamic CSS rule creation
- Used for color-based utility classes
- Support responsive color variants
- Enable theme-based color switching

### Validation and Processing
- Color names are checked against reserved abbreviations
- Values are processed and cleaned before use
- Support color format conversions and transformations

## Design Philosophy

### Comprehensive Coverage
Provides colors for various design needs:
- UI state colors (success, warning, error, info)
- Brand identity colors
- Neutral colors for layouts
- Accent colors for highlights

### Accessibility Considerations
- Includes sufficient color contrast options
- Provides both light and dark variants
- Supports accessible color combinations

### Framework Compatibility
- Bootstrap-compatible color names and values
- Standard CSS color support
- Custom brand extensions

## Extensibility

### Adding New Colors
New colors can be easily added to any category by extending the allColors object:

```typescript
export const allColors = {
  // existing colors...
  newColor: "#123456",
  // more colors...
};
```

### Theme Support
Colors are structured to support multiple themes:
- Default/Bootstrap theme
- Brand-specific themes
- Custom theme extensions

## Integration Points

### With Color Management Functions
- Colors are used in all color manipulation functions
- Support runtime updates and theme switching
- Enable color validation and processing

### With CSS Generation
- Referenced during CSS rule creation
- Used in utility class generation
- Support responsive and state-based variants

### With Configuration System
- Loaded into ValuesSingleton for global access
- Used in console styling and debug output
- Support configuration-based color selection

## Notes

- All colors are defined as string values for consistency
- Gradient definitions use CSS linear-gradient syntax
- Color names avoid conflicts with CSS property abbreviations
- Supports both traditional and modern web color specifications
- Designed for easy extension and customization
