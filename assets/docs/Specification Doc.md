# Mark Tucker Brand - Component Development Specification

## Overview
This specification defines the visual design system, component architecture, and development patterns for creating reusable web components in the Mark Tucker brand style.

---

## Color Palette

### Current Palette (Default)
```css
--primary-blue-light: #6BA3D8;
--primary-blue-medium: #4A7FBF;
--primary-blue-deep: #2B4A9E;
--primary-blue-dark: #1E3A7D;
--accent-cyan: #00D9FF;
--background-dark: #0A0F1A;
--background-darker: #0D1525;
--text-primary: #FFFFFF;
--text-secondary: #E5E5E5;
```

### Brand Palette (Alternative)
```css
--brand-red: #CC194D;
--brand-brown: #7A5948;
--brand-orange: #DC4419;
--brand-yellow: #DEB72C;
--brand-green: #44A543;
--brand-blue: #1296E6;
--brand-white: #FFFFFF;
--brand-black: #000000;
```

**Usage**: Default to current palette for consistency. Use brand palette for standalone components, new projects, or when specifically requested.

---

## Typography

**Font Stack**: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif`

**Hierarchy**:
- H1: 48-56px, Bold (700)
- H2: 36-42px, Bold (700)
- H3: 20-24px, Bold (700)
- Body: 16-18px, Regular (400), line-height 1.6-1.8
- Small/Code: 14px, Medium (500)

---

## Component Architecture

### File Structure (Per Component)
```
component-name/
├── index.html          # Standalone demo with inline CSS
├── component-name.js   # Web Component for reusability
├── example.html        # Usage examples and documentation
└── README.md           # Component documentation
```

### Required Files

#### 1. `index.html` - Standalone Implementation
**Purpose**: Self-contained demo that works independently

**Structure**:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Component Name</title>
    <style>
        /* CSS Variables for theming */
        :root {
            /* Brand color palette */
            --brand-red: #CC194D;
            --brand-brown: #7A5948;
            /* ... all brand colors ... */
            
            /* Component-specific variables */
            --component-color: var(--brand-blue);
            --animation-duration: 1s;
            /* ... all customizable properties ... */
        }

        /* Base styles */
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #353535;
        }

        /* Component styles using CSS variables */
        .component-container {
            /* styles here */
        }

        /* Animations */
        @keyframes animationName {
            from { /* ... */ }
            to { /* ... */ }
        }
    </style>
</head>
<body>
    <div class="component-container">
        <!-- Component markup -->
    </div>
</body>
</html>
```

**Requirements**:
- All CSS inline in `<style>` tag
- Use CSS custom properties for ALL customizable values
- Center component on page for demo
- Clean, semantic HTML
- Self-contained (no external dependencies)

#### 2. `component-name.js` - Web Component
**Purpose**: Reusable component for integration into any website

**Structure**:
```javascript
class ComponentName extends HTMLElement {
    constructor() {
        super();
        this.attachShadow({ mode: 'open' });
    }

    connectedCallback() {
        // Extract all customizable attributes with defaults
        const attribute1 = this.getAttribute('attribute-1') || 'default-value';
        const attribute2 = this.getAttribute('attribute-2') || 'default-value';
        
        // Build component with template literals
        this.shadowRoot.innerHTML = `
            <style>
                :host {
                    display: inline-block;
                }

                /* Component styles with attribute-driven values */
                .component-container {
                    property: ${attribute1};
                }

                /* All animations and keyframes */
                @keyframes animationName {
                    from { /* ... */ }
                    to { /* ... */ }
                }
            </style>
            <div class="component-container">
                <!-- Component markup with interpolated attributes -->
            </div>
        `;
    }

    // Optional: Public methods for component interaction
    methodName() {
        // Implementation
    }
}

// Define the custom element
customElements.define('component-name', ComponentName);
```

**Requirements**:
- Use Shadow DOM for encapsulation
- All customizable values exposed as HTML attributes
- Sensible defaults for all attributes
- kebab-case attribute names (e.g., `letters-fill`, `draw-duration`)
- Template literal for HTML structure
- Inline styles within shadow root
- Optional public methods for interaction

**Attribute Naming Convention**:
- Use kebab-case: `attribute-name`
- Be descriptive: `letters-fill-color` not `lfc`
- Group related attributes: `letters-*`, `globe-*`, `animation-*`
- Include units in attribute names when ambiguous: `duration`, `delay`

#### 3. `example.html` - Usage Examples
**Purpose**: Comprehensive demonstration of all component features

**Structure**:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Component Name - Examples</title>
    <style>
        body {
            margin: 0;
            padding: 40px;
            background-color: #353535;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            color: #ffffff;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        h1 {
            text-align: center;
            margin-bottom: 40px;
        }

        .example {
            background-color: #2a2a2a;
            padding: 30px;
            margin-bottom: 30px;
            border-radius: 8px;
        }

        .example h2 {
            margin-top: 0;
            color: #1296E6;
        }

        .example-content {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 200px;
            background-color: #353535;
            border-radius: 4px;
            padding: 20px;
        }

        code {
            background-color: #1a1a1a;
            padding: 2px 6px;
            border-radius: 3px;
            font-size: 14px;
        }

        pre {
            background-color: #1a1a1a;
            padding: 15px;
            border-radius: 4px;
            overflow-x: auto;
        }

        pre code {
            background: none;
            padding: 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Component Name Examples</h1>

        <div class="example">
            <h2>Basic Usage (Default)</h2>
            <div class="example-content">
                <component-name></component-name>
            </div>
            <pre><code>&lt;component-name&gt;&lt;/component-name&gt;</code></pre>
        </div>

        <div class="example">
            <h2>Custom Configuration 1</h2>
            <div class="example-content">
                <component-name attribute="value"></component-name>
            </div>
            <pre><code>&lt;component-name attribute="value"&gt;&lt;/component-name&gt;</code></pre>
        </div>

        <!-- More examples demonstrating all features -->
    </div>

    <script src="component-name.js"></script>
</body>
</html>
```

**Requirements**:
- Dark background (#353535)
- Examples in card containers (#2a2a2a)
- Blue headings (#1296E6)
- Show component + code for each example
- Demonstrate:
  - Basic usage (defaults)
  - Size variations
  - Color customization
  - Animation timing changes
  - Any other customizable features
- Include centered h1 title
- Semantic structure

#### 4. `README.md` - Documentation
**Purpose**: Complete component documentation for users

**Required Sections**:
```markdown
# Component Name

Brief description of what the component does and its key features.

## Features

- Feature 1
- Feature 2
- Technology stack used

## Usage

### Web Component (Recommended)

```html
<!-- Include the web component script -->
<script src="component-name.js"></script>

<!-- Use the component -->
<component-name></component-name>
```

### Customization

#### Size
```html
<component-name width="200" height="200"></component-name>
```

#### Colors
```html
<component-name
    attribute-1="#CC194D"
    attribute-2="#44A543">
</component-name>
```

### All Available Attributes

- `attribute-1` - Description (default: value)
- `attribute-2` - Description (default: value)
- ...list ALL attributes with defaults...

## Examples

See `example.html` for live examples of all customization options.

## Direct Integration

Copy the styles and markup directly from `index.html` into your webpage for full control over the implementation.
```

---

## Development Standards

### CSS Practices

**Use CSS Custom Properties**:
- Define ALL customizable values as CSS variables
- Group related variables logically
- Use semantic naming
- Include brand palette in `:root`

**Example**:
```css
:root {
    /* Brand colors */
    --brand-blue: #1296E6;
    
    /* Component colors */
    --component-primary: var(--brand-blue);
    --component-secondary: #FFFFFF;
    
    /* Component sizing */
    --component-width: 434px;
    --component-height: 434px;
    
    /* Animation timing */
    --animation-delay: 0s;
    --animation-duration: 1s;
}
```

**Animation Standards**:
- Use `@keyframes` for all animations
- Name animations descriptively: `drawPath`, `fadeIn`, `fillFadeIn`
- Use `ease-out` or `ease-in-out` timing functions
- Set sensible defaults for duration and delay
- Allow full customization of timing via variables/attributes

**Style Organization**:
1. CSS variables (`:root` or in component)
2. Base/layout styles
3. Component-specific styles
4. Animation keyframes
5. Animation applications

### JavaScript Practices

**Web Component Pattern**:
```javascript
class ComponentName extends HTMLElement {
    constructor() {
        super();
        this.attachShadow({ mode: 'open' });
    }

    connectedCallback() {
        // 1. Extract all attributes
        const attr = this.getAttribute('attr') || 'default';
        
        // 2. Build component
        this.shadowRoot.innerHTML = `
            <style>/* styles */</style>
            <div>/* markup */</div>
        `;
    }
    
    // 3. Optional public methods
    publicMethod() {
        // Implementation
    }
}

customElements.define('component-name', ComponentName);
```

**Attribute Extraction Pattern**:
```javascript
// Group related attributes
const width = this.getAttribute('width') || '434';
const height = this.getAttribute('height') || '434';

// Color attributes
const primaryColor = this.getAttribute('primary-color') || '#FFFFFF';
const secondaryColor = this.getAttribute('secondary-color') || '#1296E6';

// Timing attributes  
const delay = this.getAttribute('animation-delay') || '0s';
const duration = this.getAttribute('animation-duration') || '1s';
```

**Requirements**:
- Always use Shadow DOM
- Provide defaults for ALL attributes
- Use template literals for HTML structure
- Keep logic minimal (components should be declarative)
- Include comments for clarity

### HTML Practices

**Semantic Structure**:
- Use semantic HTML5 elements when appropriate
- Use descriptive class names
- Keep markup clean and minimal
- Group related elements logically

**SVG Best Practices**:
- Use `viewBox` for scalability
- Organize paths in logical groups with `<g>`
- Use descriptive class names for targetable elements
- Preserve SVG attributes needed for styling/animation

---

## Visual Design Standards

### Layout Principles
- Center components for demo pages
- Use 8px spacing system (8, 16, 24, 32, 40, etc.)
- Generous padding in example cards (30px)
- Consistent border-radius (8px for cards, 4px for small elements)

### Color Usage
- Dark backgrounds for demos (#353535)
- Card backgrounds slightly lighter (#2a2a2a)
- Code blocks darkest (#1a1a1a)
- Brand blue for headings and accents (#1296E6)
- High contrast text (white on dark)

### Typography in Examples
- Use system font stack
- Clear hierarchy with sizing
- Consistent spacing
- Code styling for technical content

---

## Component Checklist

Before considering a component complete, verify:

### Files
- [ ] `index.html` - Standalone demo works independently
- [ ] `component-name.js` - Web component with Shadow DOM
- [ ] `example.html` - Multiple usage examples with code
- [ ] `README.md` - Complete documentation

### Functionality
- [ ] Component works in both standalone and web component form
- [ ] All customizable values exposed as attributes
- [ ] Sensible defaults for all attributes
- [ ] CSS variables used throughout
- [ ] Animations smooth and performant
- [ ] No external dependencies (unless documented)

### Code Quality
- [ ] Clean, readable code
- [ ] Descriptive variable/class names
- [ ] Comments where needed
- [ ] Consistent formatting
- [ ] No console errors

### Documentation
- [ ] README lists all attributes with defaults
- [ ] Examples demonstrate all major features
- [ ] Code examples are copy-paste ready
- [ ] Clear usage instructions

### Visual Quality
- [ ] Matches brand aesthetic
- [ ] Professional appearance
- [ ] Responsive if applicable
- [ ] Good contrast and readability

---

## Quick Reference: Component Patterns

### Basic Web Component Template
```javascript
class MyComponent extends HTMLElement {
    constructor() {
        super();
        this.attachShadow({ mode: 'open' });
    }

    connectedCallback() {
        const color = this.getAttribute('color') || '#1296E6';
        const size = this.getAttribute('size') || '100px';
        
        this.shadowRoot.innerHTML = `
            <style>
                :host { display: inline-block; }
                .container { 
                    width: ${size};
                    background: ${color};
                }
            </style>
            <div class="container">
                <!-- Component content -->
            </div>
        `;
    }
}

customElements.define('my-component', MyComponent);
```

### CSS Variable Pattern
```css
:root {
    /* Brand palette */
    --brand-blue: #1296E6;
    
    /* Component variables */
    --component-color: var(--brand-blue);
    --component-size: 100px;
}

.component {
    background: var(--component-color);
    width: var(--component-size);
}
```

### Animation Pattern
```css
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.element {
    animation: fadeIn var(--animation-duration) ease-out var(--animation-delay) forwards;
}
```

---

## Design Principles

1. **Reusability First**: Every component should work standalone AND as a web component
2. **Customization**: Expose all visual and timing properties as attributes/variables
3. **Sensible Defaults**: Component should look good out of the box
4. **No Dependencies**: Components should be self-contained (pure HTML/CSS/JS)
5. **Clear Documentation**: Users should understand usage without reading code
6. **Professional Polish**: High-quality code and visual presentation
7. **Brand Consistency**: Follow color palette and visual standards

---

## Example Component Structure

```
animated-logo/
├── index.html           # Standalone demo
├── animated-logo.js     # Web component
├── example.html         # Usage examples
└── README.md            # Full documentation

button-component/
├── index.html
├── button-component.js
├── example.html
└── README.md
```

Each component is a self-contained module following this exact pattern.