# manage_bps.ts

## Overview

Manages breakpoint definitions for responsive CSS generation. This module provides CRUD operations for breakpoints and handles automatic CSS regeneration when breakpoints change.

## Purpose

- Manages responsive breakpoint configurations
- Provides breakpoint CRUD operations
- Handles automatic CSS updates when breakpoints change
- Supports Bootstrap-compatible breakpoint system

## Functions

### pushBPS(bps)

**Parameters:**
- `bps`: Array of breakpoint objects (IBPSWithBefs[])

**Purpose:** Adds or updates breakpoint definitions in the system.

**Process:**
1. Iterates through provided breakpoints
2. Checks if breakpoint already exists by name
3. Updates existing breakpoint values or adds new ones
4. Resets `class2Create` for updated breakpoints
5. Triggers CSS regeneration for all classes

**Features:**
- Updates existing breakpoints without duplication
- Automatically triggers CSS recreation
- Maintains breakpoint consistency
- Supports legacy `befs` property (deprecated)

### getBPS()

**Returns:** Array of breakpoint objects (IBPS[])

**Purpose:** Retrieves all current breakpoint definitions.

**Features:**
- Logs breakpoint information for debugging
- Returns complete breakpoint configuration
- Provides access to all breakpoint properties

## Data Structures

### IBPSWithBefs Interface

Extends the standard IBPS interface with deprecated properties:

```typescript
interface IBPSWithBefs extends IBPS, WithBefs {
  bp: string;        // Breakpoint name (e.g., "sm", "md")
  value: string;     // CSS value (e.g., "768px")
  class2Create?: string; // Optional class generation flag
  befs: string;      // DEPRECATED property
}
```

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `IBPS` interface from `../interfaces`
- `console_log` from `./console_log`
- `cssCreate` from `./cssCreate`

## Breakpoint System

### Default Breakpoints

The system comes with Bootstrap-compatible breakpoints:
- `sm`: 576px (small devices)
- `md`: 768px (medium devices)
- `lg`: 992px (large devices)
- `xl`: 1200px (extra large devices)
- `xxl`: 1400px (extra extra large devices)

### Responsive CSS Generation

When breakpoints are updated:
1. All existing CSS classes are marked for regeneration
2. Media queries are updated with new breakpoint values
3. Responsive variants of classes are recreated
4. CSS rules are updated in the stylesheet

## Integration with CSS Generation

### Automatic Updates
- Changes to breakpoints trigger immediate CSS regeneration
- Ensures all responsive classes use updated breakpoint values
- Maintains consistency across all generated CSS

### Media Query Generation
- Breakpoints are used to generate CSS media queries
- Supports mobile-first responsive design
- Compatible with Bootstrap's breakpoint system

## Usage Patterns

### Initial Setup
Configure breakpoints during library initialization:
```javascript
pushBPS([
  { bp: "mobile", value: "480px" },
  { bp: "tablet", value: "768px" },
  { bp: "desktop", value: "1024px" }
]);
```

### Dynamic Updates
Update breakpoints during runtime:
```javascript
// Update existing breakpoint
pushBPS([{ bp: "md", value: "800px" }]);

// Add new breakpoint
pushBPS([{ bp: "ultrawide", value: "1920px" }]);
```

### Querying Breakpoints
```javascript
const currentBreakpoints = getBPS();
console.log(currentBreakpoints);
```

## Error Handling

### Comprehensive Error Management
- Try-catch blocks around all operations
- Detailed error logging with stack traces
- Graceful error recovery without breaking CSS generation
- Non-blocking error handling

### Validation Features
- Automatic property normalization
- Safe handling of missing properties
- Backward compatibility with deprecated properties

## Performance Considerations

### Efficient Updates
- Only updates existing breakpoints when values change
- Minimizes unnecessary CSS regeneration
- Batches breakpoint updates for better performance

### Memory Management
- Reuses existing breakpoint objects when possible
- Clears generation flags to prevent memory leaks
- Maintains efficient breakpoint lookup

## Legacy Support

### Deprecated Properties
- Supports `befs` property for backward compatibility
- Gracefully handles legacy breakpoint formats
- Maintains compatibility with older versions

## State Management

### Singleton Integration
- Stores breakpoints in ValuesSingleton for global access
- Ensures consistent breakpoint data across the library
- Provides shared state for CSS generation

### CSS Regeneration
- Automatically triggers CSS updates when breakpoints change
- Ensures all responsive classes use current breakpoint values
- Maintains UI consistency during breakpoint updates

## Notes

- Essential for responsive design functionality
- Integrates seamlessly with CSS generation system
- Provides both programmatic and configuration-based breakpoint management
- Supports dynamic breakpoint updates without page reload
- Maintains backward compatibility while supporting modern responsive design patterns
