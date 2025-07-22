# main/ Directory

## Overview

The main directory contains the core CSS creation implementations that handle the primary functionality of the Angora CSS library. These modules implement the actual CSS generation pipeline and coordinate the entire creation process.

## Files

### doCssCreate.ts

The primary CSS creation implementation that orchestrates the complete CSS generation pipeline.

**Key Features:**
- Main entry point for CSS rule creation
- Performance monitoring and optimization
- Class discovery and processing pipeline
- Breakpoint-aware CSS generation
- Asynchronous processing for better performance

**Process Flow:**
1. Validates stylesheet existence
2. Discovers classes that need CSS rules
3. Processes each class through parsing pipeline
4. Generates CSS rules with breakpoint support
5. Updates stylesheet and tracks created classes

### Subdirectories

#### private_types/
Contains private type definitions used specifically by the main CSS creation process. These types are internal implementation details not exposed in the public API.

#### private_utilities/
Contains utility functions that support the main CSS creation process:

- **getNewClasses2Create**: Discovers new classes that need CSS rules by scanning the DOM
- **parseClass**: Processes individual classes through the transformation pipeline
- **send2CreateRules**: Generates and inserts actual CSS rules into the stylesheet

## Architecture

### Processing Pipeline

The main directory implements a multi-stage processing pipeline:

1. **Discovery Stage**: Identifies classes that need CSS rules
2. **Parsing Stage**: Transforms class names into CSS property definitions
3. **Generation Stage**: Creates actual CSS rules and media queries
4. **Insertion Stage**: Updates the stylesheet with new rules

### Performance Optimization

The main implementations focus on performance through:

- **Asynchronous Processing**: Non-blocking operations for better UI responsiveness
- **Batched Operations**: Processing multiple classes together for efficiency
- **Caching**: Maintaining lists of already processed classes
- **Deduplication**: Preventing redundant rule creation

### Error Handling

Comprehensive error handling includes:

- Stylesheet validation before processing
- Graceful error recovery
- Detailed error logging for debugging
- Fail-safe operation that doesn't break the application

## Integration Points

### With Strategy Implementations
The main implementations are called by different CSS creation strategies:
- Immediate creation for simple updates
- Timer-based creation for performance optimization
- Recurrent strategy for complex applications

### With Utility Systems
Integrates with various utility systems:
- Class discovery utilities for DOM scanning
- Parsing utilities for class transformation
- Rule generation utilities for CSS creation

### With State Management
Coordinates with the ValuesSingleton for:
- Accessing configuration values
- Tracking created classes
- Managing breakpoint definitions
- Maintaining library state

## Design Principles

### Modularity
Each function has a specific responsibility and well-defined interfaces, making the system easy to understand and maintain.

### Extensibility
The pipeline design allows for easy addition of new processing stages or modification of existing ones.

### Performance
Optimized for high-performance operation with large numbers of classes and frequent updates.

### Reliability
Robust error handling ensures the system continues to function even when individual operations fail.

## Usage Patterns

The main directory modules are used for:

### Initial CSS Generation
When the page loads and needs CSS rules for existing classes.

### Dynamic CSS Creation
When new classes are added to the DOM during user interaction.

### Batch Processing
When multiple classes need to be processed together for efficiency.

### Performance-Critical Updates
When CSS generation needs to be optimized for speed and responsiveness.

## Future Enhancements

The main directory is designed to support future enhancements such as:
- Additional CSS generation strategies
- Enhanced performance optimizations
- Extended rule generation capabilities
- Advanced caching mechanisms
