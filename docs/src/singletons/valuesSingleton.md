# valuesSingleton.ts

## Overview

The central state management singleton for the Angora CSS library. This class manages all configuration values, colors, abbreviations, breakpoints, and other shared state across the library.

## Purpose

- Provides centralized state management using the Singleton pattern
- Stores all colors, abbreviations, and configuration values
- Manages CSS class creation tracking
- Handles breakpoint definitions and pseudo-class/element mappings
- Maintains debug and configuration settings

## Singleton Pattern

### getInstance()

**Returns:** ValuesSingleton instance

**Purpose:** Ensures only one instance exists throughout the application lifecycle.

## Core Properties

### Identification
- `indicatorClass`: String identifier for CSS classes (default: "ank")

### Colors Management
- `colors`: Object mapping color names to color values
- Initialized with colors from `../values/colors`

### Abbreviations
- `abreviationsClasses`: Maps class abbreviations to full class names
- `abreviationsValues`: Maps value abbreviations to full values

### Combinations
- `combos`: Maps combination names to arrays of values
- `combosCreated`: Tracks created combination classes
- `encryptCombo`: Boolean flag for combination encryption
- `encryptComboCharacters`: Characters used for encryption ("■■■")
- `encryptComboCreatedCharacters`: Characters for created combos ("🜔🜔🜔")

### CSS Management
- `cssNamesParsed`: Object mapping CSS names to parsed values
- `alreadyCreatedClasses`: Array tracking already created CSS classes
- `sheet`: Reference to the managed stylesheet

### Debugging
- `isDebug`: Boolean flag for debug mode
- `styleConsole`: CSS styling for console output

### Breakpoints
- `bps`: Array of breakpoint definitions (IBPS[])
  - sm: 576px
  - md: 768px
  - lg: 992px
  - xl: 1200px
  - xxl: 1400px
- `bpsSpecifyOptions`: Array of breakpoint specification options
- `limitBPS`: Boolean flag to limit breakpoint usage

### CSS Generation
- `styleSheetToManage`: Name of the stylesheet to manage ("angora-styles")
- `separator`: Special separator character ("þµÞ")
- `specify`: Special specification character ("🜏🜏🜏")
- `importantActive`: Boolean flag for !important CSS rules

### Pseudo-Classes and Elements

#### Pseudo-Classes
Comprehensive list including:
- State-based: Active, Focus, Hover, Visited
- Structural: FirstChild, LastChild, NthChild
- Form-related: Checked, Disabled, Invalid, Valid
- Advanced: Has, Is, Where, Not

#### Pseudo-Elements
Including:
- Content: Before, After, FirstLetter, FirstLine
- Form: Placeholder, FileSelectorButton
- Advanced: Backdrop, Highlight, Selection

#### Pseudo Processing
- `pseudos`: Combined and processed pseudo mappings
- `pseudosHasSDED`: Pseudos that have special data or element dependencies
- Automatically converts camelCase to CSS-valid format
- Sorts by length for proper pattern matching

## Timer and Performance
- `useTimer`: Boolean flag for timer-based processing
- `useRecurrentStrategy`: Boolean flag for recurrent strategy
- `timeBetweenReCreate`: Time interval for recreation (milliseconds)

## Dependencies

### Value Imports
- `allColors` from `../values/colors`
- `cssNamesParsed` from `../values/cssNamesParsed`
- `commonPropertiesValuesAbreviations` from `../values/commonPropertiesValuesAbreviations`

### Type Imports
- `IAbreviationTraductor`, `IBPS`, `IPseudo` from `../interfaces`

### Function Imports
- `css_camel` from `../functions/css-camel`

## Initialization Features

### Automatic Color Processing
- Loads default color palette
- Includes Bootstrap colors, Lynx Pardelle colors, Angora brand colors
- Supports CSS basic colors

### Pseudo-Class Processing
- Automatically generates pseudo-class mappings
- Converts camelCase names to CSS-valid pseudo-selectors
- Maintains mask/real relationships for transformation

### Breakpoint Setup
- Pre-configured responsive breakpoints
- Bootstrap-compatible breakpoint values
- Extensible breakpoint system

## Configuration Management

### Debug Settings
- Debug mode controls console output
- Styled console output for better debugging
- Performance monitoring capabilities

### CSS Strategy Options
- Multiple CSS creation strategies available
- Timer-based creation for performance
- Recurrent strategy for complex updates
- Immediate creation for simple updates

## State Tracking

### Class Creation Tracking
- Maintains list of already created classes
- Prevents duplicate class creation
- Enables efficient updates

### Combo Management
- Tracks combination definitions
- Manages encryption for complex combinations
- Maintains creation state

## Usage Patterns

This singleton is used throughout the library for:
- Configuration value access
- State management
- Color and abbreviation lookups
- Breakpoint processing
- Debug control

## Thread Safety

The singleton implementation ensures:
- Single instance across the application
- Consistent state management
- Thread-safe access to shared values

## Notes

- Uses comprehensive pseudo-class and pseudo-element support
- Integrates with multiple value definition files
- Provides extensive configuration options
- Maintains backward compatibility with common CSS patterns
- Supports advanced CSS features like custom properties and modern pseudo-selectors
