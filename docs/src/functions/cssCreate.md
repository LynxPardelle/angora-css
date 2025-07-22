# cssCreate.ts

## Overview

The core CSS creation module that handles the generation of CSS rules dynamically. This module orchestrates different strategies for CSS creation based on configuration options.

## Purpose

- Provides the main entry point for CSS rule creation
- Manages different CSS creation strategies (timer-based, recurrent, immediate)
- Handles stylesheet validation and error management

## Functions

### cssCreate(updateClasses2Create?, primordial?)

**Parameters:**
- `updateClasses2Create`: Optional array of specific classes to update
- `primordial`: Boolean flag indicating if this is a primary creation process

**Purpose:** Main function that creates CSS rules using the appropriate strategy.

**Process:**
1. Validates that a stylesheet exists (calls `manage_sheet.checkSheet()` if needed)
2. Determines creation strategy based on configuration:
   - If `useTimer` is enabled: Uses `doUseTimer()`
   - If `useRecurrentStrategy` is enabled: Uses `doUseRecurrentStrategy()`
   - Otherwise: Uses immediate creation with `doCssCreate.start()`
3. Handles errors with console logging

## Dependencies

### Core Dependencies
- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`
- `manage_sheet` from `./manage_sheet`

### Strategy Dependencies
- `doCssCreate` from `./main/doCssCreate`
- `doUseTimer` from `./private/doUseTimer`
- `doUseRecurrentStrategy` from `./private/doUseRecurrentStrategy`

## Error Handling

The function includes comprehensive error handling:
- Validates stylesheet existence
- Throws descriptive errors for missing stylesheets
- Logs all errors using the console_log utility
- Gracefully handles exceptions without breaking the application

## Configuration Options

The behavior is controlled by values from the singleton:
- `useTimer`: Enables timer-based CSS creation
- `useRecurrentStrategy`: Enables recurrent strategy
- `styleSheetToManage`: Specifies the target stylesheet name

## Usage

This module is typically called:
- From the main `index.ts` exports
- Through the `AngoraService` instance
- When classes need to be created or updated dynamically

## Notes

- This is the main orchestrator for CSS creation
- The actual CSS generation logic is delegated to strategy-specific modules
- The function ensures stylesheet availability before attempting creation
- Error handling prevents CSS creation failures from breaking the application
