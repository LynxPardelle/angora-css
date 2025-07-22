# Values Directory

## Overview

The values directory contains static data definitions and configuration values used throughout the Angora CSS library. These files provide the foundational data for colors, CSS properties, and abbreviations.

## Files

### colors.ts

Defines the comprehensive color palette for the library including:

#### Default Colors
- `primary`: #0d6efd (Bootstrap primary blue)
- `secondary`: #6c757d (Bootstrap secondary gray)
- `success`: #198754 (Bootstrap success green)
- `info`: #0dcaf0 (Bootstrap info cyan)
- `warning`: #ffc107 (Bootstrap warning yellow)
- `danger`: #dc3545 (Bootstrap danger red)
- `light`: #f8f9fa (Bootstrap light gray)
- `dark`: #212529 (Bootstrap dark gray)

#### Bootstrap Colors
- `indigoBS`: #6610f2
- `purpleBS`: #6f42c1
- `pinkBS`: #d63384
- `orangeBS`: #fd7e14
- `tealBS`: #20c997
- `white`: #fff
- `grayBS`: #6c757d

#### Lynx Pardelle Colors
- `mystic`: #210020 (Deep purple)
- `lavenderLP`: #D6BCFF (Light lavender)
- `fairy`: #D680FF (Bright purple)
- `summer`: #FF9A2E (Orange)
- `old`: #EEEDA0 (Pale yellow)
- `friend`: #3BBBB2 (Teal)
- `tree`: #5A311D (Brown)
- `blood`: #8A0707 (Dark red)
- `beast`: #F5785D (Coral)
- `abyss`: #000 (Black)

#### Angora Brand Colors
- `ankcent`: #D01033 (Primary brand color)
- `secora`: #2D2824 (Secondary brand color)
- `succank`: #5D4339 (Success brand color)
- `bangrank`: #161B17 (Info brand color)
- `secbank`: #F0B566 (Warning brand color)
- `dank`: #000000 (Danger brand color)
- `dankcent`: linear-gradient(220deg, #D01033 35%,#000000 55%)
- `revdankcent`: linear-gradient(220deg, #000 35%,#D01033 55%)
- `ligthora`: #F4EBEC (Light brand color)
- `dagora`: #100809 (Dark brand color)

#### CSS Basic Colors
Complete set of CSS named colors including black, silver, gray, maroon, red, purple, fuchsia, green, lime, and many others.

### cssNamesParsed.ts

Contains parsed CSS property names and their configurations for the library's CSS generation system. This file maps CSS properties to their internal representations.

### commonPropertiesValuesAbreviations.ts

Defines common abbreviations used for CSS property values. This enables shorthand notation for frequently used values and maintains consistency across the library.

## Purpose

These value files serve multiple purposes:

### Color Management
- Provides a comprehensive color palette
- Supports multiple color schemes (Bootstrap, brand, basic CSS)
- Enables consistent color usage across the library
- Supports gradient definitions

### CSS Property Mapping
- Maps CSS properties to internal representations
- Enables efficient CSS generation
- Provides property validation and processing

### Abbreviation Support
- Defines shorthand notations for common values
- Improves developer experience with shorter syntax
- Maintains consistency in abbreviation usage

## Integration

These values are integrated into the library through:

### ValuesSingleton
- Colors are loaded into the singleton's colors property
- CSS names are loaded into cssNamesParsed
- Abbreviations are used for validation and processing

### Color Management Functions
- Colors are validated against abbreviations to prevent conflicts
- Color values are used in CSS generation
- Brand colors provide theming capabilities

### CSS Generation
- Property mappings guide CSS rule creation
- Abbreviations enable shorthand syntax
- Values provide validation and processing rules

## Extensibility

The value files are designed for easy extension:

### Adding Colors
New colors can be added to the allColors object following the existing patterns.

### Property Mapping
CSS property mappings can be extended in cssNamesParsed.

### Abbreviations
New abbreviations can be added to commonPropertiesValuesAbreviations.

## Usage Patterns

These values are used for:

### Theme Systems
- Brand color definitions
- Consistent color palette management
- Multi-theme support

### CSS Generation
- Property validation
- Abbreviation expansion
- Value processing

### Developer Experience
- Shorthand notation support
- Consistent naming conventions
- Comprehensive color options

## Notes

- Color definitions include both hex values and CSS gradients
- Property mappings support complex CSS property configurations
- Abbreviations are designed to avoid conflicts with color names
- Values are organized by category for maintainability
- Supports both modern and legacy CSS color specifications
