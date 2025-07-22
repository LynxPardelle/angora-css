# index.ts

## Overview
The main entry point for the Angora CSS library. This file exports all public APIs, functions, and utilities that developers can use to interact with the library.

## Purpose
- Serves as the central export hub for the entire library
- Provides a clean, unified API surface
- Initializes the library and sets up event listeners

## Exports

### Core Services
- `service`: Instance of AngoraService containing all library functionality
- `values`: Singleton instance containing configuration values
- `functions`: Object containing all utility functions

### Main Functions
- `cssCreate(updateClasses2Create?, primordial?)`: Creates CSS rules dynamically
- `createCSSRules(rule)`: Creates specific CSS rules
- `cssValidToCamel(st)`: Converts CSS property names to camelCase
- `camelToCSSValid(st)`: Converts camelCase to CSS-valid property names

### Color Transformation Functions
- `colorToRGB(color)`: Converts color to RGB format
- `RGBToRGBA(rgb, alpha)`: Adds alpha channel to RGB
- `parseRGB(rgba)`: Parses RGB/RGBA string
- `HexToRGB(Hex)`: Converts hexadecimal to RGB
- `HSLToRGB(HSL)`: Converts HSL to RGB
- `HWBToRGB(HWB)`: Converts HWB to RGB
- `shadeTintColor(rgb, percent)`: Creates shade or tint of color

### CRUD Operations
- `pushCssNamesParsed(cssNamesParsed)`: Adds CSS names to parsed collection
- `pushBPS(bps)`: Adds breakpoints
- `pushColors(newColors)`: Adds new colors
- `pushAbreviationsValues(abreviationsValues)`: Adds abbreviation values
- `pushAbreviationsClasses(abreviationsClasses)`: Adds abbreviation classes
- `pushCombos(combos)`: Adds combination rules

### Getters
- `getColors()`: Retrieves all colors
- `getBPS()`: Retrieves all breakpoints
- `getAbreviationsClasses()`: Retrieves abbreviation classes
- `getAbreviationsValues()`: Retrieves abbreviation values
- `getCombos()`: Retrieves combination rules
- `getCssNamesParsed()`: Retrieves parsed CSS names
- `getColorsNames()`: Retrieves color names
- `getColorValue(color)`: Gets specific color value
- `getAlreadyCreatedClasses()`: Gets already created CSS classes
- `getSheet()`: Gets the current stylesheet

### Update Operations
- `updateColor(color, value)`: Updates specific color
- `updateAbreviationsClass(abreviationsClass, value)`: Updates abbreviation class
- `updateAbreviationsValue(abreviationsValue, value)`: Updates abbreviation value
- `updateCombo(combo, values)`: Updates combination rule
- `updateCssNamesParsed(cssNameParsed, value)`: Updates parsed CSS name
- `updateClasses(classesToUpdate)`: Updates multiple classes

### Delete Operations
- `deleteColor(color)`: Removes specific color
- `clearAllColors()`: Removes all colors

### Configuration Functions
- `changeImportantActive()`: Toggles !important flag
- `changeDebugOption()`: Toggles debug mode
- `changeUseTimerOption()`: Toggles timer usage
- `setTimeBetweenReCreate(time)`: Sets recreation time interval

### Utility Functions
- `unbefysize(value)`: Removes size modifications
- `befysize(value)`: Applies size modifications
- `consoleLog(type, thing, style, line, stoper)`: Custom console logging
- `consoleParser(config)`: Parses console configuration

## Initialization
The module automatically initializes when the window loads, creating initial CSS rules.

## Dependencies
- AngoraService from `./service`
- Interfaces from `./interfaces`
- ValuesSingleton from `./singletons/valuesSingleton`
- Various function modules from `./functions/`
