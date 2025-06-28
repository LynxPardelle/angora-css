# console_log.ts

## Overview

Enhanced console logging utility that provides advanced debugging capabilities including stack traces, styled output, and conditional logging based on debug settings.

## Purpose

- Provides enhanced console logging with stack trace information
- Supports styled console output for better debugging visualization
- Implements conditional logging based on debug configuration
- Offers multiple log types (log, info, trace, error)

## Functions

### consoleLog(type?, thing, style?, line?, stoper?)

**Parameters:**
- `type`: Log type ("log" | "info" | "trace" | "error"), defaults to "log"
- `thing`: The content to log (any type)
- `style`: CSS styling for console output, defaults to values.styleConsole
- `line`: Optional line information string
- `stoper`: Boolean to control if logging should be suppressed, defaults to !values.isDebug

**Purpose:** Main logging function with enhanced capabilities.

**Features:**
- Delegates to consoleParser for actual processing
- Provides convenient defaults for common logging scenarios
- Integrates with global debug settings

### consoleParser(config)

**Parameters:**
- `config`: IConsoleParser object containing logging configuration

**Purpose:** Core logging processor that handles the actual console output.

**Process:**
1. Sets defaults for missing configuration values
2. Checks if logging should proceed based on stoper flag and error type
3. Displays line information if provided
4. Shows stack trace information
5. Creates collapsible trace group
6. Outputs the content using appropriate console method
7. Shows object directory view for object types

**Features:**
- Stack trace integration
- Collapsible trace groups
- Styled output support
- Object inspection
- Multiple log type support

## Helper Functions

### getStackTrace()

**Returns:** Array of stack trace lines

**Purpose:** Captures and formats the current execution stack trace.

**Process:**
1. Throws and catches an error to capture stack
2. Parses and cleans the stack trace
3. Removes internal function calls from the trace
4. Returns formatted stack lines

## Dependencies

- `IConsoleParser` from `../interfaces`
- `ValuesSingleton` from `../singletons/valuesSingleton`

## Configuration Integration

The module integrates with global configuration through ValuesSingleton:
- `values.styleConsole`: Default styling for console output
- `values.isDebug`: Controls whether logging is enabled

## Log Types

### log
Standard console.log output for general information

### info
Console.info output for informational messages

### error
Console.error output for error conditions (always shows regardless of debug settings)

### trace
Console trace output for detailed debugging

## Advanced Features

### Conditional Logging
- Respects debug settings to prevent log spam in production
- Error logs always show regardless of debug state
- Customizable per-call with stoper parameter

### Stack Trace Integration
- Shows the calling location for each log
- Provides collapsible trace groups for detailed investigation
- Helps with debugging complex call chains

### Styled Output
- Supports CSS styling in console output
- Consistent styling through singleton configuration
- Enhanced readability for debug sessions

### Object Inspection
- Automatically provides directory view for objects
- JSON stringifies objects in the main log output
- Maintains object structure for detailed inspection

## Usage Patterns

This module is used throughout the library for:
- Error reporting and debugging
- Development-time logging
- Performance monitoring
- State inspection

## Error Handling

- Safe stack trace capture with fallbacks
- Graceful handling of missing configuration
- Non-blocking error reporting that doesn't break application flow

## Notes

- Error logs bypass debug settings for critical information
- Stack traces help identify the source of log calls
- Styled output improves debugging experience in modern browsers
- Object inspection provides both summary and detailed views
