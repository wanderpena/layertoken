# LayerToken Framework - Technical Architecture

## 🏗️ Design Philosophy

LayerToken is built on three core principles:

1. **Token-First Configuration** - All design decisions centralized in CSS Custom Properties
2. **Layer-Based Cascade** - Predictable specificity using `@layer`
3. **Modern CSS Features** - Zero-dependency, leveraging cutting-edge browser APIs

---

## 📐 Layer Architecture

### The Seven Layers

```
┌─────────────────────────────────────────────┐
│ 7. THEMES        (Runtime overrides)        │ ← Highest Priority
├─────────────────────────────────────────────┤
│ 6. UTILITIES     (Atomic classes)           │
├─────────────────────────────────────────────┤
│ 5. COMPONENTS    (UI building blocks)       │
├─────────────────────────────────────────────┤
│ 4. LAYOUT        (Grid, Flexbox)            │
├─────────────────────────────────────────────┤
│ 3. BASE          (Element defaults)         │
├─────────────────────────────────────────────┤
│ 2. RESET         (Normalize)                │
├─────────────────────────────────────────────┤
│ 1. TOKENS        (Design variables)         │ ← Lowest Priority
└─────────────────────────────────────────────┘
```

### Why This Order?

Each layer builds upon the previous:

- **Tokens** define the language (variables)
- **Reset** provides a clean slate
- **Base** styles semantic HTML
- **Layout** adds structural patterns
- **Components** create reusable UI
- **Utilities** enable rapid customization
- **Themes** allow runtime reconfiguration

---

## 🎨 Token System

### Architecture

```
:root
  └── Design Tokens
       ├── Spacing      (--space-*)
       ├── Colors       (--color-*)
       ├── Typography   (--text-*, --font-*, --leading-*)
       ├── Layout       (--container-*, --radius-*, --shadow-*)
       └── Transitions  (--transition-*, --ease-*)
```

### HSL Color System

Colors use HSL (Hue, Saturation, Lightness) for runtime manipulation:

```css
/* Base color as HSL components */
--color-primary-h: 220;
--color-primary-s: 90%;
--color-primary-l: 55%;

/* Computed color */
--color-primary: hsl(var(--color-primary-h), var(--color-primary-s), var(--color-primary-l));

/* Automatic shade generation */
--color-primary-light: hsl(var(--color-primary-h), var(--color-primary-s), 70%);
--color-primary-dark: hsl(var(--color-primary-h), var(--color-primary-s), 40%);

/* Alpha variants */
--color-primary-alpha-10: hsla(var(--color-primary-h), var(--color-primary-s), var(--color-primary-l), 0.1);
```

**Benefits:**
- Easy shade generation by adjusting lightness
- Theme switching by changing hue
- Alpha variants without recalculation
- Dark mode by inverting lightness values

### Enhanced Properties with `@property`

```css
@property --color-primary-h {
  syntax: "<number>";      /* Type safety */
  inherits: true;          /* Cascade behavior */
  initial-value: 220;      /* Fallback */
}
```

**Benefits:**
- Type safety (prevents invalid values)
- Animatable (smooth color transitions)
- Better performance (browser optimization)
- Inheritance control

---

## 📊 Spacing System

### Mathematical Progression

```
Base Unit: 4px (0.25rem)
Scale: Linear increments

--space-1:  4px   (1 × 4)
--space-2:  8px   (2 × 4)
--space-3:  12px  (3 × 4)
--space-4:  16px  (4 × 4)
--space-5:  20px  (5 × 4)
--space-6:  24px  (6 × 4)
--space-8:  32px  (8 × 4)
--space-10: 40px  (10 × 4)
--space-12: 48px  (12 × 4)
--space-16: 64px  (16 × 4)
--space-20: 80px  (20 × 4)
--space-24: 96px  (24 × 4)
```

### Customization

Change the base unit to scale the entire system:

```css
:root {
  --space-unit: 0.5rem; /* 8px base instead of 4px */
}

/* All spacing automatically doubles */
--space-4: calc(var(--space-unit) * 4); /* Now 32px instead of 16px */
```

---

## 📱 Fluid Typography

### Responsive Scaling with `clamp()`

```css
--text-base: clamp(
  1rem,              /* Minimum size (mobile) */
  0.95rem + 0.25vw,  /* Preferred size (scales with viewport) */
  1.125rem           /* Maximum size (desktop) */
);
```

**How It Works:**

1. Below minimum viewport → `1rem`
2. Between min/max → Scales fluidly with viewport
3. Above maximum viewport → `1.125rem`

**Benefits:**
- No media queries needed
- Smooth scaling across all screen sizes
- Better typography rhythm
- Reduced maintenance

### Complete Type Scale

```
Mobile → Desktop
--text-xs:   0.75rem  → 0.875rem
--text-sm:   0.875rem → 1rem
--text-base: 1rem     → 1.125rem
--text-lg:   1.125rem → 1.25rem
--text-xl:   1.25rem  → 1.5rem
--text-2xl:  1.5rem   → 1.875rem
--text-3xl:  1.875rem → 2.25rem
--text-4xl:  2.25rem  → 3rem
--text-5xl:  3rem     → 3.75rem
```

---

## 🎯 Zero-Specificity Utilities

### The `:where()` Strategy

```css
/* Traditional approach (0,0,1 specificity) */
.text-primary { color: var(--color-primary); }

/* LayerToken approach (0,0,0 specificity) */
:where(.text-primary) { color: var(--color-primary); }
```

**Benefits:**
- Inline styles always win
- Easy to override without `!important`
- Predictable cascade behavior
- No specificity wars

### Example Usage

```html
<!-- Utility class is easily overridden -->
<p class="text-primary" style="color: red;">
  Red text (inline style wins due to 0 specificity)
</p>

<!-- Component class can override utility -->
<p class="text-primary my-component-text">
  Custom color (component CSS wins)
</p>
```

---

## 📦 Container Queries

### Component-Aware Responsiveness

Traditional approach (viewport-based):
```css
@media (min-width: 768px) {
  .grid { grid-template-columns: repeat(3, 1fr); }
}
```

LayerToken approach (container-based):
```css
@container component (min-width: 600px) {
  .cq-grid-md { grid-template-columns: repeat(3, 1fr); }
}
```

### Setting Up Container Queries

```html
<!-- 1. Create container context -->
<div class="cq-container">
  
  <!-- 2. Child adapts to container width, not viewport -->
  <div class="grid cq-grid-sm cq-grid-md cq-grid-lg gap-4">
    <div>Item 1</div>
    <div>Item 2</div>
  </div>
</div>
```

**Benefits:**
- Components responsive regardless of placement
- Reusable across different layouts
- No viewport-specific code
- True component encapsulation

---

## 🌐 Constraint-Based Grid

### Auto-Adaptive Layout

```css
.grid-auto {
  display: grid;
  gap: var(--space-4);
  grid-template-columns: repeat(
    auto-fit,
    minmax(min(100%, var(--grid-min, 250px)), 1fr)
  );
}
```

**How It Works:**

1. `auto-fit` - Automatically fits as many columns as possible
2. `minmax()` - Each column is at least 250px (or custom value)
3. `min(100%, ...)` - Prevents overflow on narrow screens
4. `1fr` - Columns expand to fill available space

### Usage

```html
<!-- Default: minimum 250px columns -->
<div class="grid-auto">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>

<!-- Custom: minimum 350px columns -->
<div class="grid-auto" style="--grid-min: 350px;">
  <div>Wider columns</div>
</div>
```

**Result:**
- 1000px container → 4 columns @ 250px each
- 600px container → 2 columns @ 300px each
- 400px container → 1 column @ 400px
- No media queries required!

---

## 🌓 Dark Mode Implementation

### Three-Tier Approach

1. **Automatic Detection** (respects OS preference)
```css
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --surface-background: var(--color-neutral-900);
    --surface-foreground: var(--color-neutral-50);
  }
}
```

2. **Manual Override** (user choice persists)
```html
<body data-theme="dark">
```

3. **Priority System**
```
data-theme="light"  → Force light  (highest priority)
data-theme="dark"   → Force dark   (highest priority)
No attribute        → Auto detect  (respects OS)
```

### Color Inversion Strategy

```css
/* Light Mode */
--surface-background: hsl(220, 10%, 98%);  /* Very light */
--surface-foreground: hsl(220, 10%, 10%);  /* Very dark */

/* Dark Mode */
--surface-background: hsl(220, 10%, 10%);  /* Very dark */
--surface-foreground: hsl(220, 10%, 98%);  /* Very light */
```

**Key Insight:** Maintain same hue and saturation, only invert lightness.

---

## ♿ Accessibility Features

### Respecting User Preferences

#### Reduced Motion
```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

#### High Contrast
```css
@media (prefers-contrast: high) {
  :root {
    --surface-border: currentColor;
  }
  
  .btn,
  .card,
  .input {
    border-width: 2px;
  }
}
```

### Focus Management

```css
/* Remove default focus (replaced with custom) */
:focus {
  outline: none;
}

/* Better focus for keyboard navigation */
:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
}
```

---

## ⚡ Performance Optimization

### CSS Containment

```css
.card {
  contain: layout style paint;
}
```

**Benefits:**
- Browser can isolate rendering
- Faster paint operations
- Improved scroll performance

### Will-Change Hints

```css
.btn:hover {
  will-change: transform;
  transform: translateY(-1px);
}
```

### Critical CSS Strategy

1. **Core** - Include inline in `<head>`
2. **Components** - Load async after page load
3. **Utilities** - Lazy load for interactive elements

---

## 🎨 Theme System Architecture

### Token Override Cascade

```
User Theme
    ↓
Preset Theme
    ↓
Dark/Light Mode
    ↓
Default Tokens
```

### Creating Custom Themes

```css
/* Define custom theme */
[data-theme="my-brand"] {
  /* Override tokens */
  --color-primary-h: 330;
  --color-primary-s: 95%;
  --color-primary-l: 55%;
  
  /* Cascade generates shades automatically */
  /* --color-primary-light and --color-primary-dark auto-compute */
}
```

### Runtime Theme Switching

```javascript
// Change theme
document.body.dataset.theme = 'ocean';

// Tokens update immediately
// All components re-render with new colors
// No page reload needed
```

---

## 🔧 Browser Support Strategy

### Progressive Enhancement

```css
/* Fallback for older browsers */
.grid-auto {
  display: flex;
  flex-wrap: wrap;
}

/* Enhancement for modern browsers */
@supports (grid-template-columns: subgrid) {
  .grid-auto {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  }
}
```

### Feature Detection

```css
/* Container queries */
@supports (container-type: inline-size) {
  .cq-container {
    container-type: inline-size;
  }
}

/* :has() selector */
@supports selector(:has(*)) {
  .card:has(.card-image) {
    padding-top: 0;
  }
}
```

---

## 📏 File Structure

```
layertoken/
├── layertoken.css              # Complete bundle
├── layertoken-core.css         # Tokens + Reset + Base
├── layertoken-layout.css       # Layout utilities
├── layertoken-components.css   # UI components
├── layertoken-utilities.css    # Atomic classes
├── layertoken-themes.css       # Theme system
└── README.md                   # Documentation
```

---

## 🚀 Build & Optimization

### Development
```bash
# Use uncompressed files for debugging
<link rel="stylesheet" href="layertoken.css">
```

### Production
```bash
# Minify and compress
npx clean-css-cli layertoken.css -o layertoken.min.css

# Gzip for serving
gzip layertoken.min.css

# Result: ~8KB (from ~45KB uncompressed)
```

### CDN Strategy
```html
<!-- Production -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/layertoken@1.0.0/layertoken.min.css">

<!-- Development -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/layertoken@1.0.0/layertoken.css">
```

---

## 🎓 Advanced Patterns

### Composing Utilities

```html
<!-- Spacing + Typography + Colors -->
<p class="mt-4 text-lg font-semibold text-primary">
  Composed from multiple utilities
</p>
```

### Component + Utility Mixing

```html
<!-- Component with utility overrides -->
<button class="btn btn-primary px-8 rounded-full">
  Modified button
</button>
```

### Dynamic Tokens

```html
<!-- Custom spacing on element level -->
<div class="stack" style="--stack-space: 2rem;">
  <p>Custom spacing between items</p>
  <p>Without creating new classes</p>
</div>
```

---

## 📚 Design Decisions

### Why Not Tailwind?
- **Build Step:** LayerToken requires zero compilation
- **File Size:** Tailwind generates thousands of classes; LayerToken is minimal
- **Learning Curve:** Semantic component names vs. memorizing utilities

### Why Not Bootstrap?
- **Modern CSS:** Bootstrap uses older techniques; LayerToken uses cutting-edge features
- **Specificity:** Bootstrap has specificity issues; LayerToken uses layers
- **Customization:** Bootstrap requires SASS; LayerToken uses CSS variables

### Why Not CSS-in-JS?
- **Performance:** No runtime overhead
- **SSR-Friendly:** Works without JavaScript
- **Caching:** Standard CSS caching applies
- **Debugging:** Standard DevTools work perfectly

---

## 🔮 Future Roadmap

- [ ] CSS Nesting support
- [ ] Anchor Positioning API integration
- [ ] View Transitions API
- [ ] Scroll-driven animations
- [ ] Component library (React, Vue, Svelte)
- [ ] Figma plugin for token sync

---

**Last Updated:** 2026-02-05  
**Framework Version:** 1.0.0  
**Maintained by:** LayerToken Team
