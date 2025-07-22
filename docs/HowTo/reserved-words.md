# Reserved Words in Angora CSS

## Overview

Angora CSS uses special character combinations for complex CSS values and selectors. These reserved words allow you to create complex CSS properties and selectors that would be impossible with regular class names.

## Basic Character Replacements

```javascript
// Reserved character delimiters
'per' → '%'         // Percentage symbol (with number prefix: 50per → 50%)
'COM' → ', '        // Comma with space
'CSP' → "'"         // Single quote
'CDB' → '"'         // Double quote
'MIN' → '-'         // Minus/hyphen
'PLUS' → '+'        // Plus symbol
'SD' → '('          // Start delimiter (opening parenthesis)
'ED' → ')'          // End delimiter (closing parenthesis)
'SE' → '['          // Start bracket (opening square bracket)
'EE' → ']'          // End bracket (closing square bracket)
'HASH' → '#'        // Hash symbol
'SLASH' → '/'       // Forward slash
'UND' → '_'         // Underscore
'__' → ' '          // Double underscore to space
'_' → '.'           // Single underscore to dot
'DPS' → ':'         // Double point (colon)
'PNC' → ';'         // Point and comma (semicolon)
'EQ' → '='          // Equal symbol
```

## CSS Selector Delimiters

```javascript
// CSS combinator delimiters
'CHILD' → ' > '     // Child combinator
'ADJ' → ' + '       // Adjacent sibling combinator
'SIBL' → ' ~ '      // General sibling combinator
'ALL' → '*'         // Universal selector
'ST' → '^'          // Starts with attribute selector
'INC' → '$'         // Includes/ends with attribute selector
```

## Special Function Delimiters

```javascript
// Special functional delimiters
'__OPA' → 'OPA'     // Opacity mode activation
'SEL'               // CSS selector prefix
'VAL', 'VALS', 'DEF' // Combo value patterns
```

## Usage Examples of Reserved Words

### Percentage Values

```html
<!-- Using 'per' for percentage (automatically converts numbers + per) -->
<div class="ank-width-50per">Width: 50%</div>
<div class="ank-height-100per">Height: 100%</div>
<div class="ank-opacity-75per">Opacity: 75%</div>
```

### Complex CSS Values with Delimiters

```html
<!-- Box shadow with commas -->
<div class="ank-boxShadow-0__2px__4px__lavenderCOM__inset__2px__0__4px__fairy">
  Complex box shadow: 0 2px 4px #D6BCFF, inset 2px 0 4px #D680FF
</div>

<!-- CSS calc() function -->
<div class="ank-width-calcSD50px__PLUS__10vwED">
  Width: calc(50px + 10vw)
</div>

<!-- RGBA colors -->
<div class="ank-color-rgbaSD255COM0COM0COM0_5ED">
  Color: rgba(255, 0, 0, 0.5)
</div>

<!-- Negative values -->
<div class="ank-marginTop-MIN1_5rem">
  Margin-top: -1.5rem
</div>

<!-- Hash colors -->
<div class="ank-color-HASHFF0000">
  Color: #FF0000
</div>
```

### CSS Selectors

```html
<!-- Child selector -->
<div class="ank-colorSELCHILDspan-red">
  Targets: .ank-colorSELCHILDspan-red > span { color: red; }
</div>

<!-- Adjacent sibling selector -->
<div class="ank-marginTopSELADJp-20px">
  Targets: .ank-marginTopSELADJp-20px + p { margin-top: 20px; }
</div>

<!-- General sibling selector -->
<div class="ank-colorSELSIBLdiv-blue">
  Targets: .ank-colorSELSIBLdiv-blue ~ div { color: blue; }
</div>

<!-- Universal selector -->
<div class="ank-marginSELALL-0">
  Targets: .ank-marginSELALL-0 * { margin: 0; }
</div>

<!-- Attribute selectors -->
<div class="ank-widthSEL__aSEtargetEQCDBUNDblankCDBEE-100px">
  Targets: a[target="_blank"] { width: 100px; }
</div>

<!-- Attribute starts with selector -->
<div class="ank-colorSEL__aSEhrefSTEQCDBhttpsCDBEE-blue">
  Targets: a[href^="https"] { color: blue; }
</div>

<!-- Attribute ends with selector -->
<div class="ank-fontWeightSEL__aSEhrefINCEQCDB_pdfCDBEE-bold">
  Targets: a[href$=".pdf"] { font-weight: bold; }
</div>

<!-- Complex URL example -->
<div class="ank-textDecorationSEL__aSEhrefEQCDBhttpsDPSSLASHSLASHlynxpardelle_comCDBEE-none">
  Targets: a[href="https://lynxpardelle.com"] { text-decoration: none; }
</div>
```

### Advanced Examples

```html
<!-- Multiple selectors with commas -->
<div class="ank-paddingSEL__h1COM__h2COM__h3-20px">
  Targets: h1, h2, h3 { padding: 20px; }
</div>

<!-- Complex calc with multiple operations -->
<div class="ank-width-calcSD100per__MIN__SDjava-sdSDSD2rem__PLUS__10pxEDEDEDED">
  Width: calc(100% - ((2rem + 10px)))
</div>

<!-- Box shadow with rgba -->
<div class="ank-boxShadow-0__4px__8px__rgbaSD0COM0COM0COM0_2EDCOM__inset__0__2px__4px__rgbaSD255COM255COM255COM0_1ED">
  Box-shadow: 0 4px 8px rgba(0,0,0,0.2), inset 0 2px 4px rgba(255,255,255,0.1)
</div>
```

## Reserved Words Reference

Based on the Angora CSS implementation, here are all available reserved words:

| Reserved Word | Translates To | Description | Example |
|---------------|---------------|-------------|---------|
| `per` | `%` | Percentage (with number) | `50per` → `50%` |
| `COM` | `, ` | Comma with space | `redCOMblue` → `red, blue` |
| `CSP` | `'` | Single quote | `CSPtextCSP` → `'text'` |
| `CDB` | `"` | Double quote | `CDBtextCDB` → `"text"` |
| `MIN` | `-` | Minus/hyphen | `MIN10px` → `-10px` |
| `PLUS` | `+` | Plus symbol | `PLUS5px` → `+5px` |
| `SD` | `(` | Start delimiter (opening parenthesis) | `calcSD...` → `calc(...` |
| `ED` | `)` | End delimiter (closing parenthesis) | `...100pxED` → `...100px)` |
| `SE` | `[` | Start bracket | `aSE...` → `a[...` |
| `EE` | `]` | End bracket | `...blankEE` → `...blank]` |
| `HASH` | `#` | Hash symbol | `HASHFF0000` → `#FF0000` |
| `SLASH` | `/` | Forward slash | `url/path` → `url/path` |
| `UND` | `_` | Underscore | `my_variable` → `my_variable` |
| `__` | ` ` | Double underscore to space | `margin__top` → `margin top` |
| `_` | `.` | Single underscore to dot | `1_5rem` → `1.5rem` |
| `CHILD` | ` > ` | Child combinator | `divCHILDspan` → `div > span` |
| `ADJ` | ` + ` | Adjacent sibling | `pADJdiv` → `p + div` |
| `SIBL` | ` ~ ` | General sibling | `h1SIBLp` → `h1 ~ p` |
| `ALL` | `*` | Universal selector | `ALL` → `*` |
| `EQ` | `=` | Equal symbol | `attrEQvalue` → `attr=value` |
| `ST` | `^` | Starts with | `hrefST` → `href^` |
| `INC` | `$` | Ends with | `hrefINC` → `href$` |
| `DPS` | `:` | Double point (colon) | `httpsDPS` → `https:` |
| `PNC` | `;` | Point and comma (semicolon) | `rulePNC` → `rule;` |

## Best Practices

1. **Use Reserved Words for Complex Values**: When you need special characters in CSS values
2. **Combine Multiple Reserved Words**: Create complex selectors and values
3. **Test Complex Combinations**: Verify that your reserved word combinations work as expected
4. **Document Complex Usage**: Add comments when using multiple reserved words together

## Common Patterns

### URL and Path Values

```html
<div class="ank-backgroundImage-urlCDBimagesSLASHbg_jpgCDB">
  Background-image: url("images/bg.jpg")
</div>
```

### CSS Functions

```html
<div class="ank-width-calcSD100vw__MIN__20pxED">
  Width: calc(100vw - 20px)
</div>
```

### Multi-value Properties

```html
<div class="ank-margin-10px__20px__30px__40px">
  Margin: 10px 20px 30px 40px
</div>
```
