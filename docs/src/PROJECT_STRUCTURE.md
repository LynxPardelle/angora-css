# Project Structure Summary

## Overview

This document provides a complete overview of the Angora CSS library project structure, documenting every file and directory within the `src/` folder and their relationships.

## Source Code Structure

```
src/
├── index.ts                    # Main entry point and public API
├── interfaces.ts               # TypeScript interfaces extending base types
├── service.ts                  # AngoraService class with aggregated functionality
├── types.ts                    # Core TypeScript type definitions
├── functions/                  # Function modules directory
│   ├── abreviation_traductors.ts
│   ├── color_transform.ts
│   ├── console_log.ts
│   ├── css-camel.ts
│   ├── cssCreate.ts
│   ├── debugg_options.ts
│   ├── manage_abreviations.ts
│   ├── manage_bps.ts
│   ├── manage_classes.ts
│   ├── manage_colors.ts
│   ├── manage_combos.ts
│   ├── manage_CSSNamesParsed.ts
│   ├── manage_CSSRules.ts
│   ├── manage_sheet.ts
│   ├── utility_configurations.ts
│   ├── main/
│   │   ├── doCssCreate.ts
│   │   ├── private_types/
│   │   └── private_utilities/
│   ├── private/
│   │   ├── createMediaRule.ts
│   │   ├── createSimpleRule.ts
│   │   ├── doUseRecurrentStrategy.ts
│   │   ├── doUseTimer.ts
│   │   └── timeManagerCssCreate.ts
│   └── utilities/
│       ├── combinators.ts
│       └── multiTransform.ts
├── singletons/
│   └── valuesSingleton.ts      # Central state management singleton
└── values/
    ├── colors.ts               # Color definitions
    ├── commonPropertiesValuesAbreviations.ts
    └── cssNamesParsed.ts       # CSS property mappings
```

## Documentation Structure

The documentation mirrors the source structure exactly:

```
docs/
├── README.md                   # Project overview and architecture
└── src/
    ├── index.md               # Main entry point documentation
    ├── interfaces.md          # Interface definitions documentation
    ├── service.md             # Service layer documentation
    ├── types.md               # Type system documentation
    ├── functions/
    │   ├── README.md          # Functions overview
    │   ├── cssCreate.md
    │   ├── console_log.md
    │   ├── css-camel.md
    │   ├── manage_colors.md
    │   ├── manage_sheet.md
    │   ├── main/
    │   │   ├── README.md      # Main functions overview
    │   │   └── doCssCreate.md
    │   ├── private/
    │   └── utilities/
    ├── singletons/
    │   └── valuesSingleton.md
    └── values/
        ├── README.md          # Values overview
        └── colors.md
```

## File Categories

### Core Files

#### index.ts
- **Purpose**: Main entry point and public API
- **Exports**: All public functions, service instance, and utilities
- **Key Features**: Auto-initialization, unified API surface

#### service.ts
- **Purpose**: Central service aggregation using composition pattern
- **Architecture**: Aggregates all function modules and singleton
- **Pattern**: Facade pattern for simplified access

#### types.ts & interfaces.ts
- **Purpose**: TypeScript type system foundation
- **Features**: Comprehensive type definitions, interface contracts
- **Usage**: Throughout library for type safety

### Function Modules

#### Core CSS Generation
- `cssCreate.ts`: Main CSS creation orchestrator
- `manage_CSSRules.ts`: CSS rule management
- `manage_classes.ts`: CSS class management
- `manage_sheet.ts`: Stylesheet management

#### Color System
- `color_transform.ts`: Color format conversions
- `manage_colors.ts`: Color CRUD operations

#### Data Management
- `manage_abreviations.ts`: Abbreviation system
- `manage_bps.ts`: Breakpoint management
- `manage_combos.ts`: Combination management
- `manage_CSSNamesParsed.ts`: CSS property parsing

#### Utilities
- `css-camel.ts`: Property name conversions
- `console_log.ts`: Enhanced debugging
- `debugg_options.ts`: Debug configuration
- `utility_configurations.ts`: General utilities

### Specialized Subdirectories

#### functions/main/
Contains core CSS creation implementations:
- `doCssCreate.ts`: Primary CSS generation pipeline
- `private_types/`: Internal type definitions
- `private_utilities/`: Core utility functions

#### functions/private/
Internal implementation functions:
- `createMediaRule.ts`: Media query creation
- `createSimpleRule.ts`: Basic rule creation
- `doUseRecurrentStrategy.ts`: Recurrent processing
- `doUseTimer.ts`: Timer-based processing
- `timeManagerCssCreate.ts`: Time management

#### functions/utilities/
Helper utility functions:
- `combinators.ts`: CSS combinator utilities
- `multiTransform.ts`: Multi-value transformations

### State and Configuration

#### singletons/valuesSingleton.ts
- **Purpose**: Central state management
- **Features**: Configuration, colors, breakpoints, pseudo-classes
- **Pattern**: Singleton for shared state

#### values/
Static data definitions:
- `colors.ts`: Comprehensive color palette
- `cssNamesParsed.ts`: CSS property mappings
- `commonPropertiesValuesAbreviations.ts`: Abbreviation definitions

## Architectural Patterns

### Composition Pattern
The service layer uses composition to aggregate functionality from multiple modules.

### Singleton Pattern
ValuesSingleton ensures consistent state management across the library.

### Module Pattern
Each function file exports an object with related functions.

### Strategy Pattern
Multiple CSS generation strategies (immediate, timer, recurrent).

## Dependencies and Relationships

### Core Dependencies
```
index.ts → service.ts → all function modules → valuesSingleton.ts
```

### Function Module Dependencies
```
cssCreate.ts → main/doCssCreate.ts → private utilities
manage_colors.ts → cssCreate.ts (for updates)
console_log.ts ← (used by most modules)
manage_sheet.ts ← (used by CSS creation)
```

### Value Dependencies
```
valuesSingleton.ts → values/* (imports static data)
All modules → valuesSingleton.ts (shared state)
```

## Integration Points

### Public API (index.ts)
- Exports all public functionality
- Provides consistent interface
- Handles library initialization

### Service Layer (service.ts)
- Aggregates all capabilities
- Provides unified access
- Manages module composition

### State Management (valuesSingleton.ts)
- Central configuration
- Shared state across modules
- Consistent data access

### Utility Layers
- Common functions used across modules
- Enhanced debugging and logging
- Property name transformations

## Extension Points

### Adding New Functions
1. Create function module in appropriate directory
2. Import into service.ts
3. Export through index.ts if public

### Adding New Colors
1. Add to values/colors.ts
2. Automatically available through singleton
3. Usable in color management functions

### Adding New Types
1. Define in types.ts
2. Create interfaces in interfaces.ts
3. Use throughout library for type safety

## Documentation Coverage

Every file in the `src/` directory has corresponding documentation:
- Individual file documentation explaining purpose and functionality
- Directory README files explaining organization and relationships
- Main project documentation providing overall architecture overview

The documentation maintains the same structure as the source code for easy navigation and understanding.
