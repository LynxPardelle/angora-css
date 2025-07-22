# Getting Started with Angora CSS

Welcome to Angora CSS! This guide will help you get up and running with the dynamic CSS generation library in just a few minutes.

## 📋 Prerequisites

Before you begin, make sure you have:

- Basic understanding of CSS and HTML
- A web development environment set up
- Node.js installed (for NPM installation)

## 🚀 Installation Options

### Option 1: NPM Install (Recommended)

Install Angora CSS via NPM:

```bash
npm install angora-css
```

#### For Vanilla JavaScript/TypeScript':'

```javascript
import { AngoraService } from 'angora-css';

// Initialize the service
const angoraService = new AngoraService();

// Start CSS generation
angoraService.cssCreate();
```

#### For Angular Applications':''

```typescript
import { AngoraService } from 'angora-css';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  constructor(private angoraService: AngoraService) {
    // Initialize CSS generation
    this.angoraService.cssCreate();
  }
  
  ngDoCheck(): void {
    // Regenerate CSS when DOM changes
    this.angoraService.cssCreate();
  }
}
```

### Option 2: CDN (Coming Soon)

CDN support is planned for future releases. For now, please use the NPM installation method.

### Option 3: Download and Include

1. Download the latest release from the GitHub repository
2. Copy the built files to your project
3. Include the JavaScript file in your HTML
4. Create a CSS file named `ank-styles.css` and link it to your HTML

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="ank-styles.css">
</head>
<body>
    <!-- Your content here -->
    <script src="angora-css.min.js"></script>
    <script>
        // Initialize Angora CSS
        const angoraService = new AngoraService();
        angoraService.cssCreate();
    </script>
</body>
</html>
```

## 🎯 First Steps

### 1. Create Your CSS Stylesheet

Create a CSS file named `ank-styles.css` in your project and link it to your HTML:

```html
<link rel="stylesheet" href="ank-styles.css">
```

**Important**: This file is where Angora CSS will inject the generated CSS rules. Make sure it's linked to your HTML file.

### 2. Basic HTML Structure

Use Angora CSS classes in your HTML with the `ank-` prefix:

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="ank-styles.css">
    <title>My Angora CSS App</title>
</head>
<body>
    <!-- Basic styling examples -->
    <div class="ank-bg-primary ank-color-white ank-p-20px">
        Primary colored box with white text and 20px padding
    </div>
    
    <button class="ank-bg-secondary ank-color-white ank-p-10px_20px ank-border-none ank-borderRadius-5px">
        Styled Button
    </button>
    
    <p class="ank-fontSize-18px ank-color-blue ank-marginTop-15px">
        Large blue text with top margin
    </p>
</body>
</html>
```

### 3. Initialize Angora CSS

Add the initialization code to make your classes work:

```javascript
import { AngoraService } from 'angora-css';

// Create service instance
const angoraService = new AngoraService();

// Initialize CSS generation
document.addEventListener('DOMContentLoaded', () => {
    angoraService.cssCreate();
});
```

## 🎨 Understanding the Basics

### Class Naming Convention

Angora CSS uses a simple pattern: `ank-property-value`

```html
<!-- Property: background-color, Value: red -->
<div class="ank-bg-red">Red background</div>

<!-- Property: font-size, Value: 24px -->
<span class="ank-fontSize-24px">Large text</span>

<!-- Property: margin, Value: 10px 20px -->
<div class="ank-margin-10px_20px">Margin top/bottom 10px, left/right 20px</div>
```

### Color System

Angora CSS comes with built-in colors:

```html
<div class="ank-bg-primary">Primary color background</div>
<div class="ank-bg-secondary">Secondary color background</div>
<div class="ank-bg-success">Success color background</div>
<div class="ank-bg-danger">Danger color background</div>
<div class="ank-bg-warning">Warning color background</div>
<div class="ank-bg-info">Info color background</div>
```

### Responsive Design

Use breakpoint prefixes for responsive design:

```html
<!-- Different margins on different screen sizes -->
<div class="ank-margin-10px ank-margin-sm-20px ank-margin-lg-30px">
    Responsive margins
</div>

<!-- Hide on small screens, show on large -->
<div class="ank-display-none ank-display-lg-block">
    Hidden on mobile, visible on desktop
</div>
```

## 🔧 Configuration

### Adding Custom Colors

```javascript
// Add custom colors to your palette
angoraService.pushColors({
    'brand-blue': '#1a73e8',
    'brand-green': '#34a853',
    'custom-purple': '#8b5cf6'
});

// Regenerate CSS with new colors
angoraService.cssCreate();
```

### Adding Custom Breakpoints

```javascript
// Add custom breakpoints
angoraService.pushBPS({
    'tablet': 768,
    'desktop': 1024,
    'ultrawide': 1920
});
```

### Creating Combos

Combos allow you to create reusable style combinations:

```javascript
// Define a button combo
angoraService.pushCombos({
    'btnPrimary': [
        'ank-bg-primary ank-color-white ank-p-12px_24px',
        'ank-border-none ank-borderRadius-6px ank-cursor-pointer',
        'ank-fontSize-16px abk-fontWeight-600'
    ]
});

// Use in HTML
<button class="btnPrimary">Styled Button</button>
```

## 🎯 Complete Example

Here's a complete working example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Angora CSS Demo</title>
    <link rel="stylesheet" href="ank-styles.css">
</head>
<body>
    <!-- Header -->
    <header class="ank-bg-primary ank-color-white ank-p-20px ank-textAlign-center">
        <h1 class="ank-fontSize-32px ank-margin-0">Welcome to Angora CSS</h1>
    </header>
    
    <!-- Main content -->
    <main class="ank-maxWidth-800px ank-margin-0_auto ank-p-20px">
        <!-- Card component -->
        <div class="ank-bg-white ank-borderRadius-8px ank-boxShadow-0_2px_4px_rgba(0,0,0,0.1) ank-p-30px ank-marginBottom-20px">
            <h2 class="ank-fontSize-24px ank-color-gray-800 ank-marginBottom-15px">Getting Started</h2>
            <p class="ank-fontSize-16px ank-lineHeight-1_6 ank-color-gray-600">
                This is a simple example showing how to use Angora CSS classes.
            </p>
            <button class="ank-bg-secondary ank-color-white ank-p-10px_20px ank-border-none ank-borderRadius-5px ank-cursor-pointer ank-marginTop-15px">
                Learn More
            </button>
        </div>
        
        <!-- Responsive grid -->
        <div class="ank-display-grid ank-gridTemplateColumns-1fr ank-md-gridTemplateColumns-repeat(2,1fr) ank-gap-20px">
            <div class="ank-bg-info ank-color-white ank-p-20px ank-borderRadius-5px">
                <h3 class="ank-fontSize-18px ank-marginBottom-10px">Feature 1</h3>
                <p class="ank-fontSize-14px">Dynamic CSS generation</p>
            </div>
            <div class="ank-bg-success ank-color-white ank-p-20px ank-borderRadius-5px">
                <h3 class="ank-fontSize-18px ank-marginBottom-10px">Feature 2</h3>
                <p class="ank-fontSize-14px">Responsive design support</p>
            </div>
        </div>
    </main>
    
    <script type="module">
        import { AngoraService } from './node_modules/angora-css/dist/index.js';
        
        const angoraService = new AngoraService();
        
        // Add custom colors
        angoraService.pushColors({
            'brand-primary': '#6366f1',
            'gray-800': '#1f2937',
            'gray-600': '#4b5563'
        });
        
        // Initialize CSS generation
        angoraService.cssCreate();
    </script>
</body>
</html>
```

## 🚨 Important Notes

1. **CSS File**: Always create and link the `ank-styles.css` file to your HTML
2. **DOM Ready**: Make sure to call `cssCreate()` after the DOM is loaded
3. **Dynamic Content**: Call `cssCreate()` again when adding new content dynamically
4. **Class Format**: Always use the `ank-property-value` || `ank-property-breakpoint-value` format for class names

## 🔄 Dynamic Updates

For single-page applications or dynamic content:

```javascript
// When adding new content dynamically
function addNewContent() {
    // Add your new HTML content
    document.body.innerHTML += '<div class="ank-bg-warning ank-p-15px">New content</div>';
    
    // Regenerate CSS for new classes
    angoraService.cssCreate();
}
```

## 🎉 What's Next?

Now that you have Angora CSS set up, explore these features:

1. **[Properties and Values](./properties-and-values.md)** - Learn the core class system
2. **[Pseudo-classes and Elements](./pseudo-classes-and-elements.md)** - Add interactive states
3. **[Combos System](./combos.md)** - Create reusable style combinations
4. **[Reserved Words](./reserved-words.md)** - Use special characters in values
5. **[Methods](./methods.md)** - Programmatic control and customization

Happy coding with Angora CSS! 🎨✨
