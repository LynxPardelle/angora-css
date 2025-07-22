# cssNamesParsed.ts

## Overview

Defines a comprehensive mapping of CSS property abbreviations to their full CSS property names. This file serves as the core translation dictionary for the library's abbreviation system, enabling shorthand CSS property notation.

## Purpose

- Provides abbreviated CSS property names for faster development
- Maps shorthand notation to standard CSS properties
- Supports both single and multi-property abbreviations
- Enables consistent abbreviation patterns across the library

## Structure

The `cssNamesParsed` object contains mappings in the format:
```typescript
{
  abbreviation: "css-property-name" | ["property1", "property2"]
}
```

## Abbreviation Categories

### Display and Layout
- `d`: "display" - Element display type
- `pos`: "position" - Element positioning method
- `t`: "top" - Top position
- `bot`, `b`: "bottom" - Bottom position
- `start`, `s`: "left" - Left position (start for RTL support)
- `end`, `e`: "right" - Right position (end for RTL support)
- `z`, `zi`: "z-index" - Stacking order

### Flexbox Properties
- `fb`: "flex-basis" - Flex item initial size
- `fd`: "flex-direction" - Flex container direction
- `fwr`: "flex-wrap" - Flex wrapping behavior
- `fg`: "flex-grow" - Flex grow factor
- `fsh`: "flex-shrink" - Flex shrink factor
- `flex`: "flex" - Flex shorthand
- `jc`: "justify-content" - Main axis alignment
- `ai`: "align-items" - Cross axis alignment
- `as`: "align-self" - Individual item alignment
- `ac`: "align-content" - Multi-line alignment

### CSS Grid Properties
- `gtc`: "grid-template-columns" - Grid column template
- `gtr`: "grid-template-rows" - Grid row template
- `gta`: "grid-template-areas" - Grid area template
- `gt`: "grid-template" - Grid template shorthand
- `gg`: "grid-gap" - Grid gap spacing
- `gc`: "grid-column" - Grid column placement
- `gr`: "grid-row" - Grid row placement
- `gcs`: "grid-column-start" - Grid column start
- `gce`: "grid-column-end" - Grid column end
- `grs`: "grid-row-start" - Grid row start
- `gre`: "grid-row-end" - Grid row end
- `ga`: "grid-area" - Grid area placement
- `gac`: "grid-auto-columns" - Auto column sizing
- `gar`: "grid-auto-rows" - Auto row sizing
- `gaf`: "grid-auto-flow" - Auto placement flow

### Dimensions
- `w`: "width" - Element width
- `h`: "height" - Element height
- `wmn`, `minw`: "min-width" - Minimum width
- `hmn`, `minh`: "min-height" - Minimum height
- `wmx`, `maxw`: "max-width" - Maximum width
- `hmx`, `maxh`: "max-height" - Maximum height

### Box Model Properties

#### Padding
- `p`: "padding" - All sides padding
- `pt`: "padding-top" - Top padding
- `pb`: "padding-bottom" - Bottom padding
- `ps`: "padding-left" - Left padding (start)
- `pe`: "padding-right" - Right padding (end)
- `py`: ["padding-top", "padding-bottom"] - Vertical padding
- `px`: ["padding-left", "padding-right"] - Horizontal padding

#### Margin
- `m`: "margin" - All sides margin
- `mt`: "margin-top" - Top margin
- `mb`: "margin-bottom" - Bottom margin
- `ms`: "margin-left" - Left margin (start)
- `me`: "margin-right" - Right margin (end)
- `my`: ["margin-top", "margin-bottom"] - Vertical margin
- `mx`: ["margin-left", "margin-right"] - Horizontal margin

### Border Properties

#### Border Width
- `bw`: "border-width" - All sides border width
- `bwt`: "border-top-width" - Top border width
- `bwb`: "border-bottom-width" - Bottom border width
- `bws`: "border-left-width" - Left border width
- `bwe`: "border-right-width" - Right border width
- `bwy`: ["border-top-width", "border-bottom-width"] - Vertical borders
- `bwx`: ["border-left-width", "border-right-width"] - Horizontal borders

#### Border Style
- `bst`: "border-style" - All sides border style
- `bstt`: "border-top-style" - Top border style
- `bstb`: "border-bottom-style" - Bottom border style
- `bsts`: "border-left-style" - Left border style
- `bste`: "border-right-style" - Right border style
- `bsty`: ["border-top-style", "border-bottom-style"] - Vertical borders
- `bstx`: ["border-left-style", "border-right-style"] - Horizontal borders

#### Border Color
- `bco`: "border-color" - All sides border color
- `bcot`: "border-top-color" - Top border color
- `bcob`: "border-bottom-color" - Bottom border color
- `bcos`: "border-left-color" - Left border color
- `bcoe`: "border-right-color" - Right border color
- `bcoy`: ["border-top-color", "border-bottom-color"] - Vertical borders
- `bcox`: ["border-left-color", "border-right-color"] - Horizontal borders

## Multi-Property Abbreviations

Some abbreviations map to multiple CSS properties for convenience:

### Directional Groupings
- `py`: Applies to both top and bottom (vertical)
- `px`: Applies to both left and right (horizontal)
- `my`: Applies to both top and bottom margins
- `mx`: Applies to both left and right margins

### Border Groupings
- `bwy`: Top and bottom border widths
- `bwx`: Left and right border widths
- `bsty`: Top and bottom border styles
- `bstx`: Left and right border styles
- `bcoy`: Top and bottom border colors
- `bcox`: Left and right border colors

## Usage in Library

### CSS Generation
These abbreviations are used during CSS class parsing to:
1. Recognize abbreviated property names in class strings
2. Generate appropriate CSS rules with full property names
3. Support both single and multi-property rules

### Property Validation
The mappings serve as a validation dictionary:
- Validates that abbreviated properties are recognized
- Ensures consistent property name usage
- Supports property name normalization

### Development Experience
Provides developers with:
- Shorter class names for faster development
- Consistent abbreviation patterns
- Familiar naming conventions similar to utility frameworks

## Integration Points

### With Class Parsing
Used by class parsing functions to:
- Translate abbreviated property names
- Generate CSS rules with proper property names
- Handle multi-property abbreviations

### With CSS Generation
Integrated into CSS rule creation to:
- Expand abbreviations into full CSS properties
- Generate valid CSS syntax
- Support responsive and pseudo-class variants

### With Validation Systems
Used for:
- Property name validation
- Abbreviation conflict detection
- CSS property normalization

## Extensibility

### Adding New Abbreviations
New abbreviations can be easily added:
```typescript
export const cssNamesParsed = {
  // existing abbreviations...
  newAbbr: "new-css-property",
  multiAbbr: ["property1", "property2"]
};
```

### Naming Conventions
The abbreviation system follows patterns:
- Single letters for common properties (w, h, m, p)
- Two-letter combinations for specific properties (mt, mb)
- Directional suffixes (t=top, b=bottom, s=start, e=end)
- Logical groupings (y=vertical, x=horizontal)

## Performance Considerations

### Lookup Efficiency
- Object literal provides O(1) lookup time
- No complex processing required
- Memory-efficient storage

### Build Optimization
- Static object can be optimized by bundlers
- Tree-shaking friendly structure
- Minimal runtime overhead

## Browser Compatibility

### CSS Property Support
- Uses standard CSS property names
- Compatible with all modern browsers
- Graceful degradation for unsupported properties

### RTL Support
- Uses logical properties where appropriate (start/end)
- Supports right-to-left layouts
- Maintains consistency across text directions

## Notes

- Essential for the library's abbreviation system
- Provides comprehensive coverage of common CSS properties
- Balances brevity with clarity in abbreviations
- Supports both single and multi-property mappings
- Designed for easy extension and maintenance
- Follows consistent naming patterns for developer experience
