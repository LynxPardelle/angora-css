# Angora CSS

Angora CSS is a dynamic CSS generation library that provides utility-first CSS creation with advanced features like color management, abbreviation systems, responsive breakpoints, and pseudo-class handling. The library enables developers to create CSS rules dynamically at runtime with a powerful API and extensive customization options.

It is based on the [Boostrap Expanded Features Library](https://github.com/LynxPardelle/bootstrap-expanded-features) and the [Bootstrap](https://getbootstrap.com/) framework. It is designed to be easy to use and customize, responsive and mobile-first.

## Key Features

### 🚀 Dynamic CSS Generation
- Runtime CSS rule creation with multiple generation strategies
- Automatic class tracking and deduplication
- Media query support for responsive design
- Performance optimization with timer-based and batched generation

### 🎨 Advanced Color Management
- Comprehensive color palette with 100+ predefined colors (Bootstrap, brand, CSS basic colors)
- Support for multiple color formats (Hex, RGB, HSL, HWB)
- Color validation and conflict prevention
- Automatic CSS class updates when colors change
- Gradient support and color transformations

### ⚡ Abbreviation System
- Shorthand notation for CSS properties and values
- Conflict detection with color names
- Extensible abbreviation definitions
- Translation between abbreviated and full forms

### 📱 Responsive Design Support
- Bootstrap-compatible breakpoint system
- Configurable breakpoint values
- Media query generation
- Responsive class variants

### 🎯 Pseudo-Class and Pseudo-Element Support
- Comprehensive pseudo-class support (50+ pseudo-classes)
- Modern pseudo-element support
- Automatic camelCase to CSS conversion
- Special handling for pseudo-classes with parameters

### 🔧 Advanced Configuration
- Debug mode with enhanced logging
- Performance optimization options
- Customizable CSS generation strategies
- Extensive configuration through singleton pattern

### 📚 **Enterprise-Grade Documentation**

- **70+ documentation files** with comprehensive coverage
- **100% source code documentation** - every function explained
- **Professional markdown** with real-world examples
- **Complete architecture guides** for developers and contributors
- **Advanced system documentation** covering internal algorithms and strategies

## Architecture

### Core Components

#### Service Layer
- **AngoraService**: Main service class that aggregates all functionality
- Provides unified API through composition pattern
- Integrates all function modules and singleton state

#### State Management
- **ValuesSingleton**: Centralized state management using singleton pattern
- Manages colors, abbreviations, breakpoints, and configuration
- Provides consistent state across the entire library

#### Function Modules
Organized into specialized modules:

**Core CSS Generation**
- Dynamic CSS rule creation and management
- Stylesheet management and validation
- CSS class tracking and optimization

**Color System**
- Color format conversions (RGB, HSL, HWB, Hex)
- Color CRUD operations and validation
- Advanced color transformations

**Data Management**
- Abbreviation system management
- Breakpoint management
- CSS property name management

**Utilities**
- CSS ↔ camelCase property name conversion
- Enhanced debugging and logging
- Configuration management

#### Value Definitions
- Comprehensive color palette (Bootstrap, brand, CSS basic colors)
- CSS property mappings and abbreviations
- Configuration values and defaults

## API Design

### Main Entry Point
```javascript
// Core functionality
cssCreate(updateClasses?, primordial?)
createCSSRules(rule)

// Color operations
colorToRGB(color)
getColors()
pushColors(newColors)
updateColor(color, value)

// Utility functions
cssValidToCamel(property)
camelToCSSValid(property)

// Configuration
changeDebugOption()
setTimeBetweenReCreate(time)
```

## Installation

```bash
npm install angora-css
```

## Quick Start

```javascript
import { cssCreate, pushColors, getColors } from 'angora-css';

// Add custom colors
pushColors({
  primary: '#007bff',
  secondary: '#6c757d'
});

// Generate CSS rules
cssCreate();

// Get all available colors
const colors = getColors();
```

## CSS Generation Strategies

### Immediate Generation
Direct CSS rule creation for simple updates and initial setup.

### Timer-Based Generation
Batched CSS generation with configurable intervals for performance optimization.

### Recurrent Strategy
Advanced strategy for complex applications with frequent updates.

## Development Features

### Enhanced Debugging
- Stack trace integration in console logging
- Styled console output for better visualization
- Conditional logging based on debug settings
- Comprehensive error reporting

### Performance Optimization
- Deduplication of CSS classes
- Batched updates for efficiency
- Memory-efficient string operations
- Optimized regular expressions

### Type Safety
- Comprehensive TypeScript definitions
- Interface-based contracts
- Type-safe configuration options
- IntelliSense support

## Browser Support

- Modern browsers with CSS3 support
- Graceful fallbacks for older browsers
- No external dependencies
- Lightweight runtime footprint

## Documentation

### Comprehensive Documentation Available

This project includes **comprehensive documentation** covering every aspect of the library:

#### 📚 **Complete Coverage**

- **70+ documentation files** with detailed explanations
- **100% source code coverage** - every significant function documented
- **Professional markdown** with examples and technical details
- **Architecture documentation** showing component relationships

#### 🗂️ **Documentation Structure**

- **`docs/`** - Complete project documentation
  - **`src/`** - Source code documentation mirroring the project structure
    - **`functions/`** - All function modules with detailed explanations
      - **`main/`** - Core CSS generation functionality
      - **`private/`** - Internal implementation details
      - **`utilities/`** - Utility functions and helpers
    - **`singletons/`** - State management documentation
    - **`values/`** - Value definitions and configurations
  - **`DOCUMENTATION_SUMMARY.md`** - Complete overview of all documentation

#### 🎯 **What's Documented**

- **Every source file** with purpose, API, and examples
- **Complex algorithms** broken down step-by-step
- **CSS generation strategies** with timing and performance details
- **Advanced systems** like shadow/gradient processing
- **Integration patterns** between components
- **Extension guides** for customization

#### 🚀 **Getting Started with Documentation**

1. **Start with [`docs/README.md`](docs/README.md)** for project overview
2. **Use [`docs/src/PROJECT_STRUCTURE.md`](docs/src/PROJECT_STRUCTURE.md)** to understand the codebase
3. **Reference individual file documentation** for specific implementation details
4. **Follow directory READMEs** to understand component relationships

The documentation provides everything needed for developers to understand, maintain, extend, and contribute to the Angora CSS library effectively.

## Examples

### Basic Usage
```javascript
import { cssCreate, changeDebugOption } from 'angora-css';

// Enable debug mode
changeDebugOption(true);

// Generate CSS for existing classes
cssCreate();
```

### Color Management
```javascript
import { pushColors, updateColor, getColorValue } from 'angora-css';

// Add new colors
pushColors({
  brand: '#ff6b35',
  accent: '#4ecdc4'
});

// Update existing color
updateColor('primary', '#0056b3');

// Get color value
const brandColor = getColorValue('brand');
```

### Breakpoint Configuration
```javascript
import { pushBPS, getBPS } from 'angora-css';

// Add custom breakpoints
pushBPS([
  { bp: 'mobile', value: '480px' },
  { bp: 'desktop', value: '1200px' }
]);

// Get all breakpoints
const breakpoints = getBPS();
```

## Contributing

We welcome contributions! Our comprehensive documentation makes it easy to get started:

### For New Contributors

- Read the **[documentation overview](docs/README.md)** to understand the project
- Check **[project structure guide](docs/src/PROJECT_STRUCTURE.md)** for codebase navigation
- Review **individual function documentation** for implementation details
- Follow **extension guides** for adding new features

### How to Contribute

- Report bugs with detailed information
- Request features with use cases
- Submit pull requests following our coding standards
- Improve documentation and examples
- Add test coverage for new functionality

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Related Projects

- [Boostrap Expanded Features Library](https://github.com/LynxPardelle/bootstrap-expanded-features)
- [Bootstrap](https://getbootstrap.com/)

## Support

For support, please:

- Check the [documentation](docs/)
- Open an issue on GitHub
- Review existing issues and discussions
