# manage_abreviations.ts

## Overview

Manages the dynamic addition, updating, and retrieval of abbreviation values and classes within the Angora CSS library. This module provides a comprehensive API for extending the library's abbreviation system at runtime, allowing for custom abbreviations and their corresponding CSS implementations.

## Purpose

- Add new abbreviation values and classes dynamically
- Update existing abbreviations and automatically refresh affected CSS
- Retrieve current abbreviation configurations
- Maintain consistency between abbreviations and generated CSS
- Support real-time abbreviation system extension

## Core Functions

### pushAbreviationsValues(abreviationsValues: any): void

**Parameters:**
- `abreviationsValues`: Object containing abbreviation-value pairs to add

**Purpose:** Adds new abbreviation values to the system and regenerates affected CSS classes.

**Process:**
1. Iterates through provided abbreviation values
2. Merges new values with existing `values.abreviationsValues`
3. Identifies previously created classes that use these abbreviations
4. Regenerates CSS for affected classes to incorporate new values
5. Handles errors gracefully with logging

**Integration:** Automatically triggers CSS regeneration for consistency.

### pushAbreviationsClasses(abreviationsClasses: any): void

**Parameters:**
- `abreviationsClasses`: Object containing abbreviation-class pairs to add

**Purpose:** Adds new abbreviation classes to the system and regenerates CSS.

**Process:**
1. Merges new abbreviation classes with existing `values.abreviationsClasses`
2. Identifies existing classes that might be affected
3. Regenerates CSS for affected classes or performs full regeneration
4. Ensures all new abbreviations are properly integrated
5. Provides comprehensive error handling

**Behavior:**
- If affected classes found: Regenerates only those classes
- If no affected classes: Performs full CSS regeneration
- Maintains system consistency throughout process

### getAbreviationsClasses(): any

**Returns:** Current abbreviation classes object

**Purpose:** Retrieves the complete set of abbreviation classes currently configured.

**Features:**
- Logs current state for debugging
- Provides read-only access to abbreviation classes
- Enables inspection of current abbreviation configuration

### getAbreviationsValues(): any

**Returns:** Current abbreviation values object

**Purpose:** Retrieves the complete set of abbreviation values currently configured.

**Features:**
- Logs current state for debugging
- Provides read-only access to abbreviation values
- Enables inspection of current abbreviation configuration

## Update Functions

### updateAbreviationsClass(abreviationsClass: string, value: string): void

**Parameters:**
- `abreviationsClass`: Name of the abbreviation class to update
- `value`: New value for the abbreviation class

**Purpose:** Updates an existing abbreviation class and regenerates affected CSS.

**Process:**
1. Validates that the abbreviation class exists
2. Updates the abbreviation class with new value
3. Searches for all created classes using this abbreviation
4. Regenerates CSS only for affected classes
5. Throws descriptive error if abbreviation doesn't exist

**Error Handling:**
- Validates existence before updating
- Provides specific error messages
- Logs all errors for debugging

### updateAbreviationsValue(abreviationsValue: string, value: string): void

**Parameters:**
- `abreviationsValue`: Name of the abbreviation value to update
- `value`: New value for the abbreviation

**Purpose:** Updates an existing abbreviation value and regenerates affected CSS.

**Process:**
1. Validates that the abbreviation value exists
2. Updates the abbreviation value with new content
3. Identifies all created classes that reference this abbreviation
4. Regenerates CSS for affected classes only
5. Provides error feedback for non-existent abbreviations

**Efficiency:** Only regenerates CSS for classes that actually use the updated abbreviation.

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`
- `cssCreate` from `./cssCreate`

## State Management

### Singleton Integration
- All abbreviation data stored in ValuesSingleton
- Maintains global consistency across library
- Provides centralized abbreviation management

### Automatic CSS Regeneration
- Tracks which classes use specific abbreviations
- Regenerates only affected CSS for performance
- Maintains real-time consistency between abbreviations and CSS

### Class Tracking
- Uses `values.alreadyCreatedClasses` to track dependencies
- Enables selective CSS regeneration
- Prevents unnecessary processing

## Integration Points

### With CSS Generation
- Automatically triggers `cssCreate.cssCreate()` when needed
- Maintains consistency between abbreviations and generated CSS
- Supports both selective and full regeneration

### With Class Management
- Integrates with class tracking system
- Supports dependency analysis for updates
- Enables efficient CSS updates

### With Debug System
- Comprehensive logging for all operations
- Error tracking and reporting
- State inspection capabilities

## Performance Optimizations

### Selective Regeneration
- Only regenerates CSS for affected classes
- Avoids full CSS rebuilds when possible
- Maintains optimal performance for updates

### Efficient Dependency Tracking
- Uses array filtering for dependency identification
- Minimizes processing overhead
- Scales well with large abbreviation sets

### Batched Operations
- Supports bulk abbreviation additions
- Minimizes CSS regeneration cycles
- Optimizes for multiple simultaneous updates

## Error Handling

### Validation
- Validates abbreviation existence before updates
- Provides descriptive error messages
- Prevents invalid operations

### Graceful Degradation
- Continues operation despite individual errors
- Comprehensive error logging
- Non-blocking error handling

### Error Recovery
- Maintains system state integrity
- Provides rollback capabilities
- Enables debugging and troubleshooting

## Usage Patterns

### Adding New Abbreviations
```javascript
// Add new abbreviation values
manage_abreviations.pushAbreviationsValues({
  'xxl': '1200px',
  'mega': '2000px'
});

// Add new abbreviation classes
manage_abreviations.pushAbreviationsClasses({
  'custom-margin': 'margin: {value}',
  'special-padding': 'padding: {value}'
});
```

### Updating Existing Abbreviations
```javascript
// Update abbreviation value
manage_abreviations.updateAbreviationsValue('lg', '1024px');

// Update abbreviation class
manage_abreviations.updateAbreviationsClass('m', 'margin: {value} !important');
```

### Retrieving Configurations
```javascript
// Get current abbreviation classes
const classes = manage_abreviations.getAbreviationsClasses();

// Get current abbreviation values  
const values = manage_abreviations.getAbreviationsValues();
```

## Real-time Updates

### Dynamic Extension
- Supports runtime abbreviation system extension
- Enables plugin-like functionality
- Maintains backward compatibility

### Live CSS Updates
- Automatically updates CSS when abbreviations change
- Maintains visual consistency in real-time
- Supports hot-reloading scenarios

### Dependency Management
- Tracks abbreviation usage across classes
- Enables intelligent update propagation
- Minimizes unnecessary regeneration

## Advanced Features

### Bulk Operations
- Supports adding multiple abbreviations simultaneously
- Optimizes CSS regeneration for bulk updates
- Maintains atomicity for batch operations

### Conflict Resolution
- Handles abbreviation name conflicts gracefully
- Provides override capabilities
- Maintains system consistency

### Debug Support
- Comprehensive logging for all operations
- State inspection capabilities
- Error tracking and reporting

## Notes

- Essential for dynamic abbreviation system management
- Provides real-time extension capabilities
- Optimizes CSS regeneration for performance
- Maintains system consistency automatically
- Supports both individual and bulk operations
- Comprehensive error handling and validation
- Integrates seamlessly with CSS generation pipeline
- Enables plugin-like extensibility for the library
