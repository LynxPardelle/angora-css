# debugg_options.ts

## Overview

Provides debug and performance configuration functions for the Angora CSS library. This module manages debugging options, timer settings, and performance optimization configurations.

## Purpose

- Controls debug mode and logging behavior
- Manages timer-based CSS generation options
- Configures performance optimization settings
- Provides runtime configuration changes

## Functions

### changeDebugOption(option?)

**Parameters:**
- `option`: Optional boolean to set specific debug state

**Purpose:** Toggles or sets the debug mode for the library.

**Behavior:**
- If `option` is provided: Sets debug mode to that value
- If `option` is undefined: Toggles current debug state
- Updates `values.isDebug` in the singleton

**Effects:**
- Controls console logging throughout the library
- Affects error reporting verbosity
- Influences performance monitoring output

### changeUseTimerOption(option?)

**Parameters:**
- `option`: Optional boolean to set specific timer state

**Purpose:** Toggles or sets the timer-based CSS generation mode.

**Behavior:**
- If `option` is provided: Sets timer mode to that value
- If `option` is undefined: Toggles current timer state
- Updates `values.useTimer` in the singleton

**Effects:**
- Switches between immediate and timer-based CSS generation
- Affects performance characteristics of CSS creation
- Controls batching behavior for CSS updates

### setTimeBetweenReCreate(time)

**Parameters:**
- `time`: Number representing milliseconds between CSS recreations

**Purpose:** Sets the interval for timer-based CSS recreation.

**Behavior:**
- Updates `values.timeBetweenReCreate` with the provided time
- Controls how frequently CSS is regenerated in timer mode
- Affects performance and responsiveness balance

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`

## Configuration Options

### Debug Mode (`isDebug`)

**Default:** `false`

**When Enabled:**
- Detailed console logging throughout the library
- Performance timing information
- Stack trace information in logs
- Enhanced error reporting

**When Disabled:**
- Minimal console output
- Reduced performance overhead
- Production-ready logging levels

### Timer Mode (`useTimer`)

**Default:** Configurable in ValuesSingleton

**When Enabled:**
- CSS generation is batched and delayed
- Better performance for frequent updates
- Reduced browser reflow/repaint operations
- Smoother user experience during intensive operations

**When Disabled:**
- Immediate CSS generation
- Real-time updates
- Higher performance overhead for frequent changes
- More responsive for individual changes

### Timer Interval (`timeBetweenReCreate`)

**Default:** Configurable in ValuesSingleton

**Purpose:** Controls the delay between CSS regeneration cycles in timer mode.

**Considerations:**
- Lower values: More responsive but higher CPU usage
- Higher values: Better performance but less responsive
- Typical range: 100-1000 milliseconds

## Usage Patterns

### Development Configuration
```javascript
// Enable debug mode for development
changeDebugOption(true);

// Use immediate updates for debugging
changeUseTimerOption(false);
```

### Production Configuration
```javascript
// Disable debug mode for production
changeDebugOption(false);

// Enable timer mode for better performance
changeUseTimerOption(true);
setTimeBetweenReCreate(250);
```

### Runtime Toggling
```javascript
// Toggle debug mode
changeDebugOption();

// Toggle timer mode
changeUseTimerOption();
```

## Performance Impact

### Debug Mode Impact
- **Enabled**: Increased logging overhead, slower execution
- **Disabled**: Minimal overhead, optimized for production

### Timer Mode Impact
- **Enabled**: Batched updates, reduced DOM manipulation
- **Disabled**: Immediate updates, higher DOM manipulation frequency

### Timer Interval Impact
- **Short intervals** (50-100ms): More responsive, higher CPU usage
- **Medium intervals** (200-300ms): Balanced performance and responsiveness
- **Long intervals** (500ms+): Better performance, potentially less responsive

## Integration Points

### With Console Logging
Debug option directly affects all console_log function calls throughout the library.

### With CSS Generation
Timer options control the CSS generation strategy used by cssCreate functions.

### With Performance Monitoring
Debug mode enables detailed performance timing and reporting.

## State Management

### Singleton Integration
All configuration values are stored in ValuesSingleton:
- Ensures consistent configuration across the library
- Provides global access to debug settings
- Maintains state persistence during library operation

### Runtime Changes
Configuration changes take effect immediately:
- Debug mode changes affect subsequent log calls
- Timer mode changes affect next CSS generation cycle
- Timer interval changes apply to future timer operations

## Development vs Production

### Development Settings
- Debug mode enabled for detailed logging
- Immediate CSS generation for real-time feedback
- Verbose error reporting for troubleshooting

### Production Settings
- Debug mode disabled for performance
- Timer mode enabled for optimization
- Balanced timer intervals for user experience

## Notes

- Simple, focused module for configuration management
- Direct singleton integration for immediate effect
- Flexible parameter handling (toggle or set)
- Essential for both development and production optimization
- Provides foundation for performance tuning and debugging
