# manage_colors.ts

## Overview

Manages color operations including CRUD operations for colors, validation, and automatic CSS class updates when colors change.

## Purpose

- Provides comprehensive color management functionality
- Handles color validation and conflict resolution
- Automatically updates CSS classes when colors are modified
- Maintains color state in the singleton

## Functions

### pushColors(newColors)

**Parameters:**
- `newColors`: Object with color names as keys and color values as strings

**Returns:**
- Success object with message on successful addition
- Error object with array of error messages if validation fails

**Purpose:** Adds new colors to the system with validation.

**Process:**
1. Validates color names against reserved abbreviations
2. Cleans color values (removes !important, !default, extra spaces)
3. Updates the colors in the singleton
4. Finds and updates any existing CSS classes that use the new colors
5. Returns validation results

### getColors()

**Returns:** Object containing all colors (name: value pairs)

**Purpose:** Retrieves all colors from the system.

### getColorsNames()

**Returns:** Array of color names

**Purpose:** Gets just the names of all available colors.

### getColorValue(color)

**Parameters:**
- `color`: Name of the color to retrieve

**Returns:** Color value string

**Purpose:** Gets the value of a specific color.

### updateColor(color, value)

**Parameters:**
- `color`: Name of the color to update
- `value`: New color value

**Purpose:** Updates an existing color and regenerates affected CSS classes.

**Process:**
1. Validates that the color exists
2. Updates the color value with cleaning
3. Finds all CSS classes that use this color
4. Regenerates those classes with the new color value

### deleteColor(color)

**Parameters:**
- `color`: Name of the color to delete

**Purpose:** Removes a color from the system.

**Validation:** Checks if the color exists before deletion.

### clearAllColors()

**Purpose:** Removes all colors from the system.

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`
- `cssCreate` from `./cssCreate`

## Validation Features

### Reserved Name Protection
- Prevents using color names that conflict with abbreviations
- Maintains system integrity by avoiding naming conflicts

### Value Cleaning
- Removes CSS modifiers (!important, !default)
- Normalizes whitespace in color values

### Existence Validation
- Validates color exists before update/delete operations
- Provides meaningful error messages

## Automatic Updates

When colors are added or updated:
1. Scans all existing CSS classes for color usage
2. Identifies classes that need regeneration
3. Automatically calls cssCreate to update affected classes
4. Ensures UI stays in sync with color changes

## Error Handling

- Comprehensive try-catch blocks around all operations
- Detailed error logging with console_log
- Graceful error recovery without breaking the application
- Validation error collection and reporting

## Usage Patterns

This module is used for:
- Theme management systems
- Dynamic color customization
- Color palette management
- Runtime color updates in CSS

## Notes

- Colors are stored in the ValuesSingleton for global access
- Color validation prevents system conflicts
- Automatic CSS regeneration keeps styles synchronized
- All operations include comprehensive logging for debugging
