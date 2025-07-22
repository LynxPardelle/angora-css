# manage_CSSRules.ts

## Overview

Manages the creation and processing of CSS rules within the Angora CSS library. This module serves as the central coordinator for CSS rule generation, handling both simple CSS rules and complex media queries while routing to appropriate specialized creation functions.

## Purpose

- Process and create CSS rules from string or array inputs
- Route rule creation to appropriate specialized handlers
- Handle both simple CSS rules and media queries
- Support batch processing of multiple rules
- Provide centralized CSS rule management interface

## Core Functions

### createCSSRules(rules: string | string[], dontSplitted: boolean = false): void

**Parameters:**
- `rules`: CSS rule(s) to create - can be string or array
- `dontSplitted`: Flag indicating if string rules need splitting (default: false)

**Purpose:** Batch processes multiple CSS rules with intelligent routing and splitting.

**Processing Logic:**
1. **String with Splitting (`dontSplitted = true`)**: Splits string by separator and processes each rule
2. **Array Input**: Iterates through array and processes each rule individually
3. **Single String**: Processes as single CSS rule directly

**Features:**
- Handles various input formats flexibly
- Filters empty rules to prevent processing errors
- Uses singleton separator for consistent splitting
- Comprehensive error handling with logging

**Use Cases:**
- Batch processing of generated CSS rules
- Handling mixed input formats from different sources
- Processing separator-delimited rule strings

### createCSSRule(rule: string): void

**Parameters:**
- `rule`: Individual CSS rule string to process

**Purpose:** Creates a single CSS rule by routing to appropriate specialized handler.

**Process:**
1. Logs the incoming rule for debugging
2. Analyzes rule structure to determine type
3. Routes to appropriate creation function:
   - **Media Rules**: Contains `@media` → `createMediaRule()`
   - **Simple Rules**: Standard CSS → `createSimpleRule()`
4. Logs the updated stylesheet state
5. Handles errors gracefully with comprehensive logging

**Rule Type Detection:**
- Checks if rule selector contains `@media`
- Routes based on CSS rule structure
- Ensures appropriate handling for different rule types

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`
- `createSimpleRule` from `./private/createSimpleRule`
- `createMediaRule` from `./private/createMediaRule`

## Rule Processing Architecture

### Input Handling

**Flexible Input Support:**
- Single CSS rule strings
- Arrays of CSS rule strings
- Separator-delimited rule strings
- Mixed format processing

**Preprocessing:**
- Automatic string splitting when needed
- Empty rule filtering
- Format normalization

### Rule Routing

**Type Detection:**
```javascript
// Media query detection
if (rule && !rule.split("{")[0].includes("@media")) {
  createMediaRule(rule);
} else {
  createSimpleRule(rule);
}
```

**Specialized Handlers:**
- `createSimpleRule()`: Handles standard CSS rules
- `createMediaRule()`: Processes media query rules
- Appropriate routing based on rule structure

## Integration Points

### With CSS Generation
- Central entry point for all CSS rule creation
- Integrates with rule generation pipeline
- Coordinates with stylesheet management

### With Private Utilities
- Delegates to specialized private functions
- Maintains clean separation of concerns
- Leverages specialized rule creation logic

### With Debug System
- Comprehensive logging for all rule processing
- Error tracking and reporting
- State inspection before and after processing

### With Singleton Management
- Uses singleton separator for consistent processing
- Integrates with global stylesheet state
- Maintains consistency across library

## Performance Considerations

### Efficient Processing
- Direct routing to appropriate handlers
- Minimal string processing overhead
- Optimized for batch operations

### Error Isolation
- Individual rule error handling
- Non-blocking error processing
- Continues processing despite individual failures

### Logging Optimization
- Strategic logging placement
- Debug information without performance impact
- Configurable logging levels

## Error Handling

### Comprehensive Coverage
- Try-catch blocks for all major operations
- Detailed error logging with context
- Graceful degradation on failures

### Fault Tolerance
- Individual rule failures don't block batch processing
- System continues operation despite errors
- Error information preserved for debugging

### Debug Support
- Before and after state logging
- Rule content logging for troubleshooting
- Error context preservation

## Usage Patterns

### Single Rule Creation
```javascript
// Create individual CSS rule
manage_CSSRules.createCSSRule('.example { color: red; }');
```

### Batch Rule Processing
```javascript
// Process array of rules
manage_CSSRules.createCSSRules([
  '.class1 { margin: 10px; }',
  '.class2 { padding: 5px; }'
]);

// Process separator-delimited string
manage_CSSRules.createCSSRules(
  '.rule1 { color: blue; } || .rule2 { font-size: 16px; }',
  true
);
```

### Mixed Format Handling
```javascript
// Handles various input formats automatically
manage_CSSRules.createCSSRules(singleRule);        // string
manage_CSSRules.createCSSRules(ruleArray);         // array
manage_CSSRules.createCSSRules(delimitedRules, true); // split string
```

## Rule Type Support

### Simple CSS Rules
- Standard CSS property-value pairs
- Class selectors, ID selectors, element selectors
- Pseudo-classes and pseudo-elements
- Complex selectors and combinators

### Media Query Rules
- Responsive breakpoint rules
- Device-specific media queries
- Feature-based media queries
- Nested media query structures

### Error Recovery
- Invalid rule handling
- Malformed CSS recovery
- Partial rule processing

## Advanced Features

### Flexible Input Processing
- Automatic format detection
- Intelligent string splitting
- Empty content filtering

### Rule Validation
- Basic structural validation
- Type-appropriate routing
- Error prevention strategies

### Debug Integration
- Comprehensive rule logging
- Processing state tracking
- Error context preservation

## State Management

### Singleton Integration
- Global separator configuration
- Stylesheet state coordination
- Consistent processing parameters

### Processing Coordination
- Maintains processing order
- Coordinates with specialized handlers
- Ensures rule creation consistency

## Development Support

### Debug Capabilities
- Rule-by-rule processing visibility
- Error tracking and reporting
- State inspection at processing stages

### Testing Support
- Clear input/output behavior
- Predictable error handling
- Isolated function testing

## Notes

- Central coordinator for all CSS rule creation
- Provides flexible input handling for various formats
- Intelligent routing to specialized rule handlers
- Comprehensive error handling and recovery
- Optimized for both single and batch operations
- Essential integration point for CSS generation pipeline
- Supports both simple and complex CSS rule structures
- Maintains system consistency through singleton integration
