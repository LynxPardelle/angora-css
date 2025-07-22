# Functions Directory

## Overview

The functions directory contains all the core functionality modules for the Angora CSS library. Each file provides specific capabilities that are aggregated into the main service.

## Structure

The functions are organized into several categories:

### Core Functions
- `cssCreate.ts` - Main CSS rule creation functionality
- `manage_classes.ts` - CSS class management
- `manage_CSSRules.ts` - CSS rule management
- `manage_sheet.ts` - Stylesheet management

### Color Management
- `color_transform.ts` - Color format conversions and transformations
- `manage_colors.ts` - Color CRUD operations and management

### Utility Functions
- `css-camel.ts` - CSS property name conversions
- `console_log.ts` - Enhanced console logging
- `debugg_options.ts` - Debug configuration management

### Data Management
- `manage_abreviations.ts` - Abbreviation management
- `manage_bps.ts` - Breakpoint management
- `manage_combos.ts` - Combination rule management
- `manage_CSSNamesParsed.ts` - CSS name parsing management

### Configuration
- `utility_configurations.ts` - Utility configuration functions
- `abreviation_traductors.ts` - Abbreviation translation functions

### Subdirectories

#### main/
Contains primary functionality implementations:
- `doCssCreate.ts` - Core CSS creation logic

#### private/
Contains internal implementation functions:
- `createMediaRule.ts` - Media query rule creation
- `createSimpleRule.ts` - Simple CSS rule creation
- `doUseRecurrentStrategy.ts` - Recurrent strategy implementation
- `doUseTimer.ts` - Timer-based processing
- `timeManagerCssCreate.ts` - Time management for CSS creation

#### utilities/
Contains utility helper functions:
- `combinators.ts` - CSS combinator utilities
- `multiTransform.ts` - Multi-value transformation utilities

## Function Module Pattern

Each function module follows a consistent pattern:

1. **Imports**: ValuesSingleton and required dependencies
2. **Values Instance**: Gets singleton instance for shared state
3. **Export Object**: Exports an object containing related functions
4. **Error Handling**: Uses try-catch with console logging
5. **State Management**: Updates singleton values as needed

## Integration

All function modules are:
- Imported into `service.ts` and aggregated into AngoraService
- Re-exported through `index.ts` for public API access
- Designed to work together through shared state in ValuesSingleton

## Dependencies

Most functions depend on:
- `ValuesSingleton` for shared state
- `console_log` for error reporting and debugging
- Other function modules for specific operations
