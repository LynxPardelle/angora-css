# interfaces.ts

## Overview

This file defines TypeScript interfaces that extend base types defined in `types.ts`. It serves as the interface layer for the Angora CSS library, providing type safety and structure for various components.

## Purpose

- Defines interfaces that extend base types
- Provides type safety for the library's public API
- Ensures consistent structure for data objects

## Interfaces

### IBPS

Extends `TBPS` type to define breakpoint structures.

**Purpose:** Defines the interface for breakpoint objects used throughout the library.

### IConsoleParser

Extends `TConsoleParser` type to define console parsing configuration.

**Purpose:** Provides structure for console logging and parsing operations.

### IPseudo

Extends `TPseudo` type to define pseudo-element/pseudo-class mappings.

**Purpose:** Handles pseudo-element and pseudo-class transformations.

### IAbreviationTraductor

Extends `TAbreviationTraductor` type to define abbreviation translation rules.

**Purpose:** Manages abbreviation to full property name translations.

## Dependencies

- All base types from `./types`

## Usage

These interfaces are used throughout the library to ensure type safety when working with:

- Breakpoint definitions
- Console parsing configurations
- Pseudo-element handling
- Abbreviation translations

## Notes

This file follows a pattern of extending types into interfaces, which allows for future extensibility while maintaining type safety. The interfaces serve as contracts for objects used in the library's public API.
