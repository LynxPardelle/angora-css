# manage_sheet.ts

## Overview

Manages the CSS stylesheet that the library uses for dynamic rule creation. This module handles stylesheet discovery, validation, and provides access to the target stylesheet.

## Purpose

- Discovers and validates the target CSS stylesheet
- Provides stylesheet access for rule creation
- Resets creation tracking when stylesheet changes
- Ensures stylesheet availability for CSS generation

## Functions

### checkSheet()

**Purpose:** Locates and validates the target stylesheet.

**Process:**
1. Gets all stylesheets from the document
2. Searches for stylesheet containing the target name (from `values.styleSheetToManage`)
3. Sets the found stylesheet as the active sheet
4. Resets tracking arrays for clean state

**Side Effects:**
- Sets `values.sheet` to the found stylesheet
- Resets `values.alreadyCreatedClasses` to empty array
- Resets `values.combosCreated` to empty object

**Usage:** Called automatically by CSS creation functions to ensure stylesheet availability.

### getSheet()

**Returns:** CSSStyleSheet | undefined

**Purpose:** Provides access to the currently managed stylesheet.

**Process:**
1. Checks if a stylesheet is currently set
2. Logs stylesheet information for debugging
3. Returns the stylesheet or undefined if none is set

**Usage:** Used by other modules that need direct access to the stylesheet.

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`
- `cssCreate` from `./cssCreate`

## Stylesheet Discovery

### Target Identification
- Uses `values.styleSheetToManage` (default: "angora-styles") to identify the target stylesheet
- Searches through all document stylesheets
- Matches by href containing the target name

### Browser Compatibility
- Works with all modern browsers that support `document.styleSheets`
- Handles both linked and embedded stylesheets
- Compatible with dynamic stylesheet loading

## State Management

### Tracking Reset
When a new stylesheet is found:
- Clears the list of already created classes
- Resets combination tracking
- Ensures clean state for new stylesheet

### Singleton Integration
- Stores stylesheet reference in ValuesSingleton
- Provides global access across the library
- Maintains consistency with other library components

## Error Handling

### Graceful Fallback
- Returns undefined if no stylesheet is found
- Allows calling code to handle missing stylesheet scenarios
- Doesn't throw errors for better reliability

### Debug Support
- Logs stylesheet information when found
- Provides visibility into stylesheet discovery process
- Helps with troubleshooting stylesheet issues

## Usage Patterns

### Automatic Discovery
Most commonly used automatically by CSS creation functions:
- Called before CSS rule generation
- Ensures stylesheet is available
- Handles dynamic stylesheet changes

### Manual Access
Can be used directly for:
- Stylesheet validation
- Direct stylesheet manipulation
- Custom rule insertion

## Integration Points

### With CSS Creation
- Called by `cssCreate` before rule generation
- Ensures stylesheet availability
- Provides foundation for CSS generation

### With Rule Management
- Provides stylesheet access for rule insertion
- Supports rule modification and deletion
- Enables direct stylesheet manipulation

## Configuration

### Target Stylesheet Name
- Configurable through `values.styleSheetToManage`
- Defaults to "angora-styles"
- Can be changed to target different stylesheets

### Discovery Method
- Uses href-based matching for linked stylesheets
- Supports partial name matching
- Works with dynamically loaded stylesheets

## Security Considerations

### CORS Handling
- Respects browser CORS policies for cross-origin stylesheets
- May have limited access to external stylesheets
- Works best with same-origin stylesheets

### Stylesheet Access
- Only accesses stylesheets available to the document
- Respects browser security restrictions
- Provides safe stylesheet manipulation

## Performance

### Efficient Discovery
- Single pass through document stylesheets
- Caches result in singleton for reuse
- Minimal overhead for repeated calls

### State Reset Optimization
- Only resets state when new stylesheet is found
- Avoids unnecessary array/object clearing
- Maintains performance during normal operation

## Notes

- Essential for library operation - CSS creation depends on stylesheet access
- Handles dynamic stylesheet scenarios gracefully
- Provides both automatic and manual stylesheet management
- Integrates seamlessly with the broader library architecture
