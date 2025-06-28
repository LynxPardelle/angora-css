# service.ts

## Overview

The `AngoraService` class serves as the main service layer for the Angora CSS library. It consolidates all functionality from various function modules and the values singleton into a single service class.

## Purpose

- Provides a unified service interface for all library functionality
- Aggregates capabilities from multiple function modules
- Serves as the central orchestrator for the library's operations

## Class: AngoraService

### Constructor

The constructor uses `Object.assign()` to merge all functionality from:

- `ValuesSingleton.getInstance()`: Core configuration and values
- `abreviation_traductors`: Abbreviation translation functions
- `color_transform`: Color manipulation functions
- `console_log`: Console logging utilities
- `css_camel`: CSS property name conversion functions
- `cssCreate`: CSS rule creation functions
- `debugg_options`: Debug configuration functions
- `manage_abreviations`: Abbreviation management functions
- `manage_bps`: Breakpoint management functions
- `manage_classes`: CSS class management functions
- `manage_colors`: Color management functions
- `manage_combos`: Combination rule management functions
- `manage_CSSNamesParsed`: CSS name parsing management
- `manage_CSSRules`: CSS rule management functions
- `manage_sheet`: Stylesheet management functions
- `utility_configurations`: Utility configuration functions

## Architecture Pattern

This service follows a composition pattern where:

1. **Singleton Integration**: Incorporates the ValuesSingleton for shared state
2. **Function Module Aggregation**: Combines all function modules into one interface
3. **Dynamic Assignment**: Uses Object.assign to merge all capabilities at runtime

## Dependencies

### Core Dependencies
- `ValuesSingleton` from `./singletons/valuesSingleton`

### Function Modules
- `abreviation_traductors` from `./functions/abreviation_traductors`
- `color_transform` from `./functions/color_transform`
- `console_log` from `./functions/console_log`
- `css_camel` from `./functions/css-camel`
- `cssCreate` from `./functions/cssCreate`
- `debugg_options` from `./functions/debugg_options`
- `manage_abreviations` from `./functions/manage_abreviations`
- `manage_bps` from `./functions/manage_bps`
- `manage_classes` from `./functions/manage_classes`
- `manage_colors` from `./functions/manage_colors`
- `manage_combos` from `./functions/manage_combos`
- `manage_CSSNamesParsed` from `./functions/manage_CSSNamesParsed`
- `manage_CSSRules` from `./functions/manage_CSSRules`
- `manage_sheet` from `./functions/manage_sheet`
- `utility_configurations` from `./functions/utility_configurations`

## Usage

The `AngoraService` is instantiated in `index.ts` and provides the main API surface for the library. All public methods available on the service instance come from the aggregated function modules and singleton.

## Notes

- This service acts as a facade pattern, simplifying access to complex subsystems
- The dynamic composition allows for easy extension and modification of functionality
- All methods are dynamically assigned, so TypeScript types should be carefully managed
