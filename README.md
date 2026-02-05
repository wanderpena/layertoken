# 🎨 LayerToken Framework

> A modern CSS framework combining **Design Tokens** + **Layer Architecture** for predictable, scalable styling.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![CSS](https://img.shields.io/badge/CSS-Modern-orange.svg)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Size](https://img.shields.io/badge/Size-~25KB-green.svg)](layertoken.css)

---

## ✨ Features

- 🎯 **Token-First Design** - Centralized configuration via CSS Custom Properties
- 📦 **Layer Architecture** - Predictable specificity using `@layer`
- 🌓 **Dark Mode Built-in** - Automatic theme switching with manual override
- 📱 **Container Queries** - Truly responsive components
- 🚀 **Zero JavaScript** - Pure CSS with modern browser features
- ⚡ **Performance** - Minimal footprint (~25KB gzipped)
- ♿ **Accessible** - WCAG 2.1 AA compliant, respects user preferences
- 🎨 **Themeable** - Runtime theme switching without recompilation

---

## 📦 Installation

### CDN (Fastest)

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/layertoken@1.0.0/layertoken.css">
```

### NPM

```bash
npm install layertoken
```

```css
@import 'layertoken';
```

### Download

Download the latest release from [GitHub](https://github.com/yourusername/layertoken/releases).

---

## 🚀 Quick Start

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="layertoken.css">
  <title>My App</title>
</head>
<body>
  <div class="container-5xl">
    <h1 class="text-4xl font-bold mb-4">Welcome to LayerToken</h1>
    
    <div class="grid-auto gap-6">
      <div class="card">
        <h2 class="card-title">Card Title</h2>
        <p class="card-content">This is a card component.</p>
        <button class="btn btn-primary">Action</button>
      </div>
    </div>
  </div>
</body>
</html>
```

---

## 🏗️ Architecture

LayerToken uses CSS `@layer` to create a predictable cascade:

```css
@layer tokens,    /* 1. Design tokens (variables) */
       reset,     /* 2. CSS reset */
       base,      /* 3. Base element styles */
       layout,    /* 4. Layout utilities (grid, flex) */
       components,/* 5. UI components */
       utilities, /* 6. Atomic utilities */
       themes;    /* 7. Theme overrides */
```

### Why Layers?

- **Predictable Specificity** - Later layers override earlier ones
- **No `!important`** - Layer order determines priority
- **Modular** - Import only what you need
- **Clear Intent** - Each layer has a single responsibility

---

## 🎨 Design Tokens

### Customization

Override tokens in your own stylesheet:

```css
:root {
  /* Change Primary Color */
  --color-primary-h: 280;
  --color-primary-s: 85%;
  --color-primary-l: 60%;
  
  /* Adjust Spacing Scale */
  --space-unit: 0.5rem; /* 8px base instead of 4px */
  
  /* Custom Font */
  --font-sans: "Inter", sans-serif;
  
  /* Border Radius Style */
  --radius-base: 0; /* Sharp corners */
}
```

### Available Token Categories

| Category | Examples | Count |
|----------|----------|-------|
| **Spacing** | `--space-1` to `--space-24` | 13 |
| **Colors** | `--color-primary`, `--color-neutral-*` | 20+ |
| **Typography** | `--text-xs` to `--text-5xl` | 9 |
| **Layout** | `--container-*`, `--radius-*` | 15+ |
| **Shadows** | `--shadow-sm` to `--shadow-2xl` | 6 |
| **Transitions** | `--transition-fast`, `--ease-*` | 8 |

---

## 🌓 Dark Mode

### Automatic (Respects System Preference)

```html
<!-- Automatically switches based on OS setting -->
<body>
  <p>This respects prefers-color-scheme</p>
</body>
```

### Manual Control

```html
<!-- Force dark mode -->
<body data-theme="dark">
  <p>Always dark</p>
</body>

<!-- Force light mode -->
<body data-theme="light">
  <p>Always light</p>
</body>
```

### JavaScript Theme Switcher

```javascript
// Toggle theme
const toggle = () => {
  const current = document.body.dataset.theme;
  document.body.dataset.theme = current === 'dark' ? 'light' : 'dark';
};

// Save preference
localStorage.setItem('theme', document.body.dataset.theme);
```

### Preset Themes

```html
<body data-theme="ocean">    <!-- Blue theme -->
<body data-theme="forest">   <!-- Green theme -->
<body data-theme="sunset">   <!-- Orange theme -->
<body data-theme="purple">   <!-- Purple theme -->
<body data-theme="monochrome"><!-- Black & white -->
```

---

## 📐 Layout System

### Constraint-Based Grid (No Media Queries!)

```html
<!-- Auto-fits columns based on container width -->
<div class="grid-auto">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>

<!-- Customize minimum column width -->
<div class="grid-auto" style="--grid-min: 300px;">
  <div>Wider columns</div>
</div>
```

### Container Queries

```html
<!-- Enable container queries -->
<div class="cq-container">
  <div class="grid cq-grid-md gap-4">
    <!-- Adapts based on container width, not viewport -->
  </div>
</div>
```

### Layout Patterns

```html
<!-- Stack (vertical spacing) -->
<div class="stack stack-lg">
  <p>Item with automatic spacing</p>
  <p>No manual margins needed</p>
</div>

<!-- Cluster (horizontal wrapping) -->
<div class="cluster cluster-sm">
  <button>Tag 1</button>
  <button>Tag 2</button>
</div>

<!-- Sidebar Layout -->
<div class="sidebar-layout" style="--sidebar-width: 300px;">
  <aside>Sidebar</aside>
  <main>Main content</main>
</div>

<!-- Center (perfect centering) -->
<div class="center">
  <div>Perfectly centered content</div>
</div>
```

---

## 🧩 Components

### Buttons

```html
<button class="btn btn-primary">Primary</button>
<button class="btn btn-secondary">Secondary</button>
<button class="btn btn-ghost">Ghost</button>
<button class="btn btn-danger">Danger</button>

<!-- Sizes -->
<button class="btn btn-primary btn-sm">Small</button>
<button class="btn btn-primary btn-lg">Large</button>

<!-- Icon button -->
<button class="btn btn-icon btn-primary">
  <svg><!-- icon --></svg>
</button>
```

### Cards

```html
<div class="card">
  <div class="card-header">
    <h3 class="card-title">Card Title</h3>
    <p class="card-description">Optional description</p>
  </div>
  <div class="card-content">
    <p>Main content goes here</p>
  </div>
  <div class="card-footer">
    <button class="btn btn-primary">Action</button>
  </div>
</div>

<!-- Interactive card -->
<div class="card card-interactive">
  <p>Hover for effect</p>
</div>
```

### Forms

```html
<div class="form-group">
  <label class="form-label" for="email">Email</label>
  <input class="input" type="email" id="email" placeholder="you@example.com">
  <span class="form-hint">We'll never share your email</span>
</div>

<div class="form-group">
  <label class="form-label" for="message">Message</label>
  <textarea class="textarea" id="message"></textarea>
</div>

<!-- Checkbox -->
<label class="checkbox">
  <input type="checkbox">
  <span>Accept terms</span>
</label>
```

### Alerts

```html
<div class="alert alert-info">
  <p class="alert-title">Information</p>
  <p>This is an informational message.</p>
</div>

<div class="alert alert-success">Success message</div>
<div class="alert alert-warning">Warning message</div>
<div class="alert alert-error">Error message</div>
```

### Badges

```html
<span class="badge">Default</span>
<span class="badge badge-primary">Primary</span>
<span class="badge badge-success">Success</span>
<span class="badge badge-warning">Warning</span>
<span class="badge badge-error">Error</span>
```

### Navigation

```html
<nav class="nav">
  <a class="nav-item" href="/" aria-current="page">Home</a>
  <a class="nav-item" href="/about">About</a>
  <a class="nav-item" href="/contact">Contact</a>
</nav>

<!-- Vertical navigation -->
<nav class="nav nav-vertical">
  <a class="nav-item" href="#">Dashboard</a>
  <a class="nav-item" href="#">Settings</a>
</nav>
```

---

## ⚡ Utilities

### Spacing

```html
<!-- Margin -->
<div class="m-4">Margin all sides</div>
<div class="mx-auto">Center horizontally</div>
<div class="mt-8 mb-4">Margin top & bottom</div>

<!-- Padding -->
<div class="p-6">Padding all sides</div>
<div class="px-4 py-2">Padding horizontal & vertical</div>
```

### Typography

```html
<p class="text-xl font-bold">Large bold text</p>
<p class="text-sm text-muted">Small muted text</p>
<p class="leading-relaxed">Relaxed line height</p>
<p class="truncate">This text will be truncated...</p>
<p class="line-clamp-3">Multi-line truncation at 3 lines</p>
```

### Colors

```html
<p class="text-primary">Primary color text</p>
<div class="bg-neutral-100 text-neutral-900">Background color</div>
```

### Borders & Shadows

```html
<div class="border rounded-lg shadow-md">
  Card with border and shadow
</div>

<div class="border-t border-b">
  Top and bottom borders only
</div>
```

### Display & Layout

```html
<div class="flex items-center justify-between">
  <span>Left</span>
  <span>Right</span>
</div>

<div class="grid grid-cols-3 gap-4">
  <div>Col 1</div>
  <div>Col 2</div>
  <div>Col 3</div>
</div>
```

---

## 🎯 Advanced Usage

### Fluid Typography

All text sizes use `clamp()` for fluid scaling:

```css
/* Automatically scales between viewport sizes */
--text-base: clamp(1rem, 0.95rem + 0.25vw, 1.125rem);
```

### Container Queries Example

```html
<div class="cq-container">
  <!-- This grid adapts based on container width -->
  <div class="grid cq-grid-sm cq-grid-md cq-grid-lg gap-4">
    <div>Item 1</div>
    <div>Item 2</div>
    <!-- More items... -->
  </div>
</div>
```

### Custom Theme Creation

```css
[data-theme="my-brand"] {
  /* Colors */
  --color-primary-h: 330;
  --color-primary-s: 95%;
  --color-primary-l: 55%;
  
  /* Typography */
  --font-sans: "YourFont", sans-serif;
  --text-base: 1.125rem;
  
  /* Spacing */
  --space-unit: 0.5rem;
  
  /* Borders */
  --radius-base: 0;
  --radius-lg: 0;
}
```

### Zero Specificity Utilities

Utilities use `:where()` for zero specificity, making them easy to override:

```html
<p class="text-primary" style="color: red;">
  <!-- style wins because utilities have 0,0,0 specificity -->
  Red text, not primary color
</p>
```

---

## ♿ Accessibility

LayerToken respects user preferences:

- **Reduced Motion**: Disables animations for users with motion sensitivity
- **High Contrast**: Increases border contrast automatically
- **Focus Visible**: Clear focus indicators for keyboard navigation
- **Semantic HTML**: Components use proper ARIA attributes

```css
/* Automatically applied */
@media (prefers-reduced-motion: reduce) {
  * { animation-duration: 0.01ms !important; }
}

@media (prefers-contrast: high) {
  .btn { border-width: 2px; }
}
```

---

## 📊 Browser Support

| Browser | Version |
|---------|---------|
| Chrome  | 105+    |
| Firefox | 110+    |
| Safari  | 16.4+   |
| Edge    | 105+    |

**Required Features:**
- CSS `@layer`
- CSS `@property`
- Container Queries
- `:has()` selector
- `clamp()` function

---

## 📦 Modular Imports

Import only what you need:

```css
/* Core only (tokens, reset, base styles) */
@import 'layertoken/layertoken-core.css';

/* Add layout utilities */
@import 'layertoken/layertoken-layout.css';

/* Add UI components */
@import 'layertoken/layertoken-components.css';

/* Add atomic utilities */
@import 'layertoken/layertoken-utilities.css';

/* Add themes */
@import 'layertoken/layertoken-themes.css';
```

---

## 🤝 Contributing

Contributions welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) first.

---

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

Inspired by:
- [Tailwind CSS](https://tailwindcss.com) - Utility-first approach
- [Open Props](https://open-props.style) - Design tokens
- [Pico CSS](https://picocss.com) - Minimal framework philosophy
- [Every Layout](https://every-layout.dev) - Layout patterns

---

## 📚 Resources

- [Documentation](https://layertoken.dev)
- [Component Examples](https://layertoken.dev/examples)
- [GitHub Repository](https://github.com/yourusername/layertoken)
- [NPM Package](https://npmjs.com/package/layertoken)

---

**Made with ❤️ by the LayerToken Team**
