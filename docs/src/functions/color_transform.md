# color_transform.ts

## Overview

Comprehensive color transformation module that provides extensive color format conversion, manipulation, and processing capabilities. Supports multiple color formats including RGB, RGBA, HEX, HSL, HSLA, and HWB, with advanced features for opacity control, color shading/tinting, and gradient processing.

## Purpose

- Convert between different color formats (RGB, HEX, HSL, HWB)
- Apply opacity and transparency effects to colors
- Create shade and tint variations of colors
- Process complex color values including gradients
- Provide robust color parsing and validation
- Support CSS-compatible color output formats

## Core Functions

### colorToRGB(color: string): number[]

**Parameters:**
- `color`: Color value in any supported format

**Returns:** RGB array [R, G, B] or [R, G, B, A]

**Purpose:** Universal color converter that detects format and converts to RGB values.

**Supported Formats:**
- Named colors (from singleton color dictionary)
- RGB/RGBA notation: `rgb(255, 0, 0)`, `rgba(255, 0, 0, 0.5)`
- HEX notation: `#FF0000`, `#F00`, `#FF0000FF`
- HSL/HSLA notation: `hsl(0, 100%, 50%)`, `hsla(0, 100%, 50%, 0.5)`
- HWB notation: `hwb(0, 0%, 0%)`

**Error Handling:** Returns red color [255, 0, 0] on parsing errors.

### RGBToRGBA(rgb: number[], alpha: number): string

**Parameters:**
- `rgb`: RGB color array [R, G, B]
- `alpha`: Alpha value (0-1)

**Returns:** RGBA CSS string

**Purpose:** Converts RGB array to RGBA CSS notation with specified alpha.

## Format-Specific Converters

### parseRGB(rgba: string): number[]

**Parameters:**
- `rgba`: RGB or RGBA string notation

**Returns:** Array of color components

**Purpose:** Parses RGB/RGBA strings and extracts numeric components.

**Features:**
- Handles both RGB and RGBA formats
- Extracts integer values from string notation
- Maintains alpha channel when present

### HexToRGB(Hex: string): string

**Parameters:**
- `Hex`: Hexadecimal color string (#RGB, #RRGGBB, etc.)

**Returns:** RGB or RGBA CSS string

**Purpose:** Converts hexadecimal color notation to RGB format.

**Supported Formats:**
- 3-digit: `#F00` → `#FF0000`
- 4-digit: `#F00A` → `#FF0000AA` (with alpha)
- 6-digit: `#FF0000`
- 8-digit: `#FF0000FF` (with alpha)

**Process:**
1. Removes # prefix
2. Detects format based on length
3. Expands short formats to full precision
4. Converts to decimal values
5. Returns appropriate RGB/RGBA string

### HSLToRGB(HSL: string): string

**Parameters:**
- `HSL`: HSL or HSLA string notation

**Returns:** RGB or RGBA CSS string

**Purpose:** Converts HSL (Hue, Saturation, Lightness) to RGB format.

**Algorithm:**
1. Parses HSL components from string
2. Normalizes values to decimal ranges
3. Handles special case for zero saturation (grayscale)
4. Applies HSL-to-RGB conversion formula
5. Uses HueToRGB helper for color calculations
6. Preserves alpha channel if present

### HueToRGB(p: number, q: number, t: number): number

**Parameters:**
- `p`: Lower color boundary
- `q`: Upper color boundary  
- `t`: Hue position (0-1)

**Returns:** RGB component value

**Purpose:** Helper function for HSL-to-RGB conversion using standard algorithm.

### HWBToRGB(HWB: string): string

**Parameters:**
- `HWB`: HWB (Hue, Whiteness, Blackness) string notation

**Returns:** RGB or RGBA CSS string

**Purpose:** Converts HWB color format to RGB.

**Process:**
1. Parses HWB components
2. Normalizes whiteness and blackness values
3. Handles ratio normalization if sum > 1
4. Applies HWB-to-RGB conversion algorithm
5. Uses hue sectoring for color calculation
6. Returns formatted RGB/RGBA string

## Color Manipulation Functions

### shadeTintColor(rgb: number[], percent: number): number[]

**Parameters:**
- `rgb`: RGB color array
- `percent`: Shade/tint percentage (-100 to 100)

**Returns:** Modified RGB array

**Purpose:** Creates darker (shade) or lighter (tint) variations of colors.

**Features:**
- Positive percentages create tints (lighter colors)
- Negative percentages create shades (darker colors)
- Handles edge cases for pure black/white colors
- Maintains alpha channel when present
- Clamps values to valid RGB range (0-255)

**Algorithm:**
1. Handles edge cases for pure colors
2. Applies percentage-based transformation
3. Clamps results to valid range
4. Preserves alpha channel if present

### opacityCreator(value: string, opacity: number): string

**Parameters:**
- `value`: Color value or gradient string
- `opacity`: Desired opacity (0-1)

**Returns:** Color/gradient string with applied opacity

**Purpose:** Applies opacity to colors and complex gradient values.

**Features:**
- Handles simple color values
- Processes complex gradients with multiple colors
- Recursively applies opacity to gradient color stops
- Maintains gradient structure and syntax
- Converts colors to RGBA format with specified opacity

**Gradient Processing:**
1. Detects gradient syntax
2. Extracts individual color values
3. Recursively applies opacity to each color
4. Reconstructs gradient with modified colors

### getShadeTintColorOrGradient(tintValue: number, value: string): string

**Parameters:**
- `tintValue`: Shade/tint percentage
- `value`: Color value or gradient string

**Returns:** Modified color/gradient string

**Purpose:** Applies shade/tint transformations to colors and gradients.

**Process:**
- Simple colors: Applies shadeTintColor transformation
- Gradients: Recursively processes each color stop
- Maintains gradient syntax and structure
- Returns RGBA format for consistency

## Utility Functions

### separateColor4Transform(value: string): RegExpMatchArray | null

**Parameters:**
- `value`: String containing color values (potentially in gradients)

**Returns:** Array of matched color strings or null

**Purpose:** Extracts individual color values from complex strings like gradients.

**Regular Expression Pattern:**
- Matches HEX colors: `#[A-Fa-f0-9]{3,8}`
- Matches RGB/RGBA: `rgb(a)?\([0-9\.\,\s%]*\)`
- Matches HSL/HSLA: `hsl(a)?\([0-9\.\,\s%]*\)`
- Matches HWB: `hwb\([0-9\.\,\s%]*\)`

## Dependencies

- `ValuesSingleton` from `../singletons/valuesSingleton`
- `console_log` from `./console_log`

## Integration Points

### With Color Management
- Uses singleton color dictionary for named colors
- Provides standardized color processing across library
- Supports all CSS color formats

### With CSS Generation
- Outputs CSS-compatible color strings
- Handles complex gradient processing
- Maintains proper formatting for CSS rules

### With Debug System
- Comprehensive logging for transformation steps
- Error tracking for invalid color formats
- Performance monitoring for complex operations

## Error Handling

### Input Validation
- Graceful handling of invalid color formats
- Fallback to red color for parsing errors
- Comprehensive error logging

### Format Detection
- Automatic format detection and conversion
- Support for malformed input with best-effort parsing
- Consistent output format regardless of input

## Performance Considerations

### Efficient Processing
- Optimized regular expressions for color matching
- Minimal string allocations during conversion
- Cached singleton access for color lookup

### Memory Management
- Stateless operations for thread safety
- No memory leaks in recursive gradient processing
- Efficient array operations for color components

## Advanced Features

### Gradient Support
- Full CSS gradient syntax support
- Recursive color processing in complex gradients
- Maintains gradient structure during transformation

### Color Space Accuracy
- Proper color space conversion algorithms
- Accurate HSL and HWB implementations
- Preservation of color fidelity across formats

### Alpha Channel Handling
- Consistent alpha channel support across formats
- Proper RGBA generation and processing
- Transparency preservation in transformations

## Usage Patterns

### Basic Color Conversion
```javascript
// Convert any color format to RGB
const rgb = color_transform.colorToRGB("#FF0000");
// Result: [255, 0, 0]
```

### Color Manipulation
```javascript
// Create lighter tint
const tinted = color_transform.shadeTintColor([255, 0, 0], 20);
// Apply opacity
const transparent = color_transform.opacityCreator("red", 0.5);
```

### Gradient Processing
```javascript
// Apply opacity to entire gradient
const transparentGradient = color_transform.opacityCreator(
  "linear-gradient(red, blue)", 
  0.7
);
```

## Notes

- Supports all major CSS color formats
- Handles complex gradient syntax
- Provides robust error handling and fallbacks
- Optimized for performance and accuracy
- Comprehensive debug logging for development
- Thread-safe stateless operations
- Maintains color fidelity across conversions
