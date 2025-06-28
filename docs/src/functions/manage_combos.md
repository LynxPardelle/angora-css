# manage_combos.ts

## Overview

Manages CSS class combinations (combos) within the Angora CSS library, providing functionality to add, update, and retrieve class combinations that generate multiple CSS rules from a single class name. This module enables the creation of compound utility classes for efficient styling.

## Purpose

- Add new class combinations dynamically
- Update existing combinations and clean up old CSS rules
- Retrieve current combination configurations
- Manage complex class combinations with multiple values
- Maintain CSS rule consistency during combo updates

## Core Functions

### pushCombos(combos: any): void

**Parameters:**
- `combos`: Object containing combo name-value pairs

**Purpose:** Adds new class combinations to the system and regenerates affected CSS.

**Process:**
1. Iterates through provided combo definitions
2. Processes combo values to handle both string and array formats
3. Normalizes values by splitting strings and flattening arrays
4. Identifies previously created classes that use these combos
5. Regenerates CSS for affected classes or performs full regeneration
6. Handles errors gracefully with comprehensive logging

**Value Processing:**
- String values: Splits on spaces and converts to array
- Array values: Maps through nested arrays, splits strings, and flattens
- Ensures consistent array format for all combo values

**CSS Regeneration:**
- If affected classes found: Regenerates only those classes
- If no affected classes: Performs full CSS regeneration
- Maintains system consistency throughout process

### getCombos(): any

**Returns:** Current combos object from singleton

**Purpose:** Retrieves the complete set of class combinations currently configured.

**Features:**
- Logs current combo state for debugging
- Provides read-only access to combo definitions
- Enables inspection of current combo configuration
- Useful for development and debugging

### updateCombo(combo: string, newValues: string[]): void

**Parameters:**
- `combo`: Name of the combo to update
- `newValues`: New array of values for the combo

**Purpose:** Updates an existing combo definition and performs comprehensive cleanup.

**Process:**
1. Validates that the combo exists in the system
2. Updates the combo with new values
3. Identifies all created classes using this combo
4. Removes old CSS rules from the stylesheet
5. Cleans up tracking arrays
6. Regenerates CSS with new combo definition
7. Throws descriptive error if combo doesn't exist

**Cleanup Operations:**
- Removes CSS rules from `values.sheet`
- Updates `values.alreadyCreatedClasses` tracking
- Ensures no orphaned CSS rules remain
- Maintains stylesheet integrity

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`
- `cssCreate` from `./cssCreate`

## Data Processing

### Value Normalization

**String Processing:**
```javascript
// Input: "class1 class2 class3"
// Output: ["class1", "class2", "class3"]
```

**Array Processing:**
```javascript
// Input: [["class1 class2"], ["class3 class4"]]
// Output: ["class1", "class2", "class3", "class4"]
```

**Mixed Processing:**
- Handles complex nested structures
- Flattens all nested arrays
- Splits space-separated strings
- Ensures consistent array output

### Combo Structure

Combos are stored as:
```javascript
{
  "combo-name": ["value1", "value2", "value3"],
  "another-combo": ["valueA", "valueB"]
}
```

## CSS Rule Management

### Rule Creation
- Each combo value generates separate CSS rules
- Maintains association between combo names and generated rules
- Supports complex multi-value combinations

### Rule Cleanup
- Identifies CSS rules by content matching
- Removes rules from active stylesheet
- Updates tracking arrays for consistency
- Prevents CSS rule accumulation

### Rule Regeneration
- Regenerates CSS after combo updates
- Ensures new combo values are properly applied
- Maintains stylesheet consistency

## Integration Points

### With CSS Generation
- Directly integrates with `cssCreate` module
- Triggers appropriate regeneration strategies
- Maintains consistency between combos and CSS

### With Stylesheet Management
- Direct manipulation of `values.sheet` for rule removal
- Coordinate with stylesheet singleton
- Ensures proper CSS rule lifecycle

### With Class Tracking
- Updates `values.alreadyCreatedClasses` arrays
- Maintains dependency tracking
- Enables selective regeneration

## Performance Optimizations

### Selective Regeneration
- Only regenerates CSS for affected classes when possible
- Avoids full CSS rebuilds for incremental updates
- Optimizes performance for targeted changes

### Efficient Cleanup
- Direct CSS rule removal from stylesheet
- Minimal array operations for tracking updates
- Batch operations for multiple rule changes

### Smart Processing
- Handles various input formats efficiently
- Minimizes string splitting and array operations
- Optimizes for common usage patterns

## Error Handling

### Validation
- Validates combo existence before updates
- Provides descriptive error messages
- Prevents invalid operations

### Graceful Recovery
- Continues operation despite individual errors
- Comprehensive error logging
- Maintains system stability during failures

### Cleanup Safety
- Ensures proper cleanup even if errors occur
- Maintains stylesheet integrity
- Prevents partial update states

## Usage Patterns

### Adding Combos
```javascript
// Add new combinations
manage_combos.pushCombos({
  'margin-combo': 'mt-4 mb-4 ml-2 mr-2',
  'padding-set': ['pt-2', 'pb-2', 'pl-4', 'pr-4'],
  'layout-combo': [['flex', 'items-center'], ['justify-between']]
});
```

### Updating Combos
```javascript
// Update existing combo
manage_combos.updateCombo('margin-combo', [
  'mt-6', 'mb-6', 'ml-3', 'mr-3'
]);
```

### Retrieving Combos
```javascript
// Get all current combos
const combos = manage_combos.getCombos();
console.log('Available combos:', combos);
```

## Advanced Features

### Complex Nesting Support
- Handles deeply nested array structures
- Processes mixed string/array inputs
- Flattens to consistent output format

### Dynamic Updates
- Real-time combo updates with CSS regeneration
- Automatic cleanup of old CSS rules
- Maintains visual consistency during updates

### Debug Support
- Comprehensive logging for all operations
- Error tracking and reporting
- State inspection capabilities

## State Management

### Singleton Integration
- All combo data stored in ValuesSingleton
- Global consistency across library
- Centralized combo management

### Tracking Consistency
- Maintains accurate class creation tracking
- Updates all relevant tracking arrays
- Ensures system state integrity

### CSS Synchronization
- Keeps CSS rules synchronized with combo definitions
- Automatic cleanup and regeneration
- Prevents CSS rule conflicts

## Notes

- Essential for compound utility class management
- Provides powerful combo system for complex styling
- Handles various input formats for flexibility
- Maintains CSS rule integrity during updates
- Optimizes performance through selective regeneration
- Comprehensive error handling and validation
- Supports complex nested combo structures
- Integrates seamlessly with CSS generation pipeline
