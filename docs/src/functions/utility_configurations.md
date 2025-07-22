# utility_configurations.ts

## Overview

Provides utility configuration management for the Angora CSS library, specifically handling the global `!important` setting that affects all generated CSS rules. This module enables runtime configuration changes with automatic CSS regeneration to maintain consistency.

## Purpose

- Manage global CSS generation configurations
- Control the `!important` flag for all generated CSS rules
- Provide runtime configuration changes with automatic updates
- Maintain consistency between configuration changes and generated CSS

## Core Functions

### changeImportantActive(option: boolean | undefined): void

**Parameters:**
- `option`: Boolean to set the important flag, or undefined to toggle

**Purpose:** Changes the global `!important` setting and regenerates all CSS rules.

**Behavior:**
- **Explicit Boolean**: Sets `importantActive` to the provided boolean value
- **Undefined/No Parameter**: Toggles the current `importantActive` state
- **Automatic Regeneration**: Triggers full CSS regeneration after configuration change

**Process:**
1. Updates `values.importantActive` with new setting
2. Uses logical OR with toggle behavior for undefined values
3. Triggers `cssCreate.cssCreate()` to regenerate all CSS with new setting
4. Ensures immediate visual consistency with new configuration

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `cssCreate` from `./cssCreate`

## Configuration Management

### Important Flag Control

**Global Impact:**
- Affects all generated CSS rules
- Applied consistently across entire stylesheet
- Immediate effect through automatic regeneration

**Toggle Behavior:**
```javascript
// Explicit setting
changeImportantActive(true);   // Sets to true
changeImportantActive(false);  // Sets to false

// Toggle current state
changeImportantActive();       // Toggles current value
changeImportantActive(undefined); // Also toggles current value
```

### CSS Regeneration

**Automatic Updates:**
- Full CSS regeneration after configuration change
- Ensures all existing rules reflect new setting
- Maintains visual consistency immediately

**Performance Consideration:**
- Full regeneration may be expensive for large stylesheets
- Consider usage in production environments
- Useful for development and runtime configuration

## Integration Points

### With CSS Generation
- Direct integration with CSS creation process
- Influences all generated CSS rules
- Maintains consistency across rule generation

### With Singleton Management
- Uses singleton for global state management
- Ensures consistent configuration across library
- Provides centralized configuration control

### Development Workflow
- Useful for debugging CSS rule importance
- Testing different importance configurations
- Runtime CSS behavior modification

## Usage Patterns

### Enable Important Rules
```javascript
// Explicitly enable !important for all rules
utility_configurations.changeImportantActive(true);
```

### Disable Important Rules
```javascript
// Explicitly disable !important for all rules
utility_configurations.changeImportantActive(false);
```

### Toggle Current Setting
```javascript
// Toggle the current important setting
utility_configurations.changeImportantActive();
```

### Development Testing
```javascript
// Test different importance configurations
utility_configurations.changeImportantActive(true);
// Test with important rules

utility_configurations.changeImportantActive(false);
// Test without important rules
```

## Configuration Impact

### CSS Rule Generation

**With Important Active (true):**
```css
.m-10 { margin: 10px !important; }
.p-5 { padding: 5px !important; }
```

**With Important Inactive (false):**
```css
.m-10 { margin: 10px; }
.p-5 { padding: 5px; }
```

### CSS Specificity
- `!important` rules have higher specificity
- Can override inline styles and other important rules
- Affects CSS cascade behavior significantly

## Performance Considerations

### Full Regeneration
- Changes trigger complete CSS regeneration
- May be expensive for large stylesheets
- Consider frequency of configuration changes

### Runtime Impact
- Immediate visual effect of configuration changes
- Potential layout shifts if cascade changes
- Monitor performance in production environments

## Error Handling

### Safe Operations
- Simple boolean operations with minimal error surface
- Defaults to toggle behavior for invalid inputs
- Maintains system stability

### Fallback Behavior
- Graceful handling of undefined values
- Consistent toggle behavior
- Predictable configuration state

## Development Support

### Debug and Testing
- Easy configuration switching for testing
- Runtime CSS behavior modification
- Development-friendly configuration control

### Configuration Inspection
- Configuration state available through singleton
- Easy to check current important setting
- Visibility into configuration state

## Advanced Usage

### Conditional Important Rules
```javascript
// Apply important rules in specific contexts
if (productionMode) {
  utility_configurations.changeImportantActive(false);
} else {
  utility_configurations.changeImportantActive(true);
}
```

### Dynamic Configuration
```javascript
// Toggle based on user preference or context
const userPreference = getUserPreference('cssImportant');
utility_configurations.changeImportantActive(userPreference);
```

## Best Practices

### Usage Guidelines
- Use sparingly in production environments
- Consider performance impact of full regeneration
- Test thoroughly when changing importance settings
- Document configuration decisions

### Development Workflow
- Useful for debugging CSS specificity issues
- Testing different cascade behaviors
- Isolating CSS rule conflicts

## Future Extensibility

### Configuration System
- Foundation for additional utility configurations
- Extensible pattern for other global settings
- Modular configuration management

### Potential Enhancements
- Granular important control per rule type
- Conditional important rules based on context
- Performance optimizations for selective regeneration

## Notes

- Simple but powerful configuration control
- Provides global CSS behavior modification
- Essential for debugging and testing CSS specificity
- Immediate effect through automatic regeneration
- Foundation for extensible configuration system
- Runtime CSS behavior control capability
- Development-friendly configuration management
