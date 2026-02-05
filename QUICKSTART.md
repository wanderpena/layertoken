# LayerToken - Quick Start Guide

Get up and running with LayerToken in 5 minutes.

---

## Installation

### Option 1: CDN (Fastest)

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
  <!-- Your content here -->
</body>
</html>
```

### Option 2: NPM

```bash
npm install layertoken
```

```css
/* In your CSS file */
@import 'layertoken';
```

---

## Your First Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <link rel="stylesheet" href="layertoken.css">
</head>
<body>
  <div class="container-5xl">
    <h1 class="text-4xl font-bold mb-4">Hello LayerToken!</h1>
    <p class="text-lg text-muted mb-6">
      Build beautiful interfaces with minimal code.
    </p>
    <button class="btn btn-primary">Get Started</button>
  </div>
</body>
</html>
```

---

## Common Patterns

### Card Grid

```html
<div class="grid-auto gap-6">
  <div class="card">
    <h3 class="card-title">Feature 1</h3>
    <p class="card-content">Description here</p>
  </div>
  
  <div class="card">
    <h3 class="card-title">Feature 2</h3>
    <p class="card-content">Description here</p>
  </div>
  
  <div class="card">
    <h3 class="card-title">Feature 3</h3>
    <p class="card-content">Description here</p>
  </div>
</div>
```

### Form

```html
<form>
  <div class="form-group">
    <label class="form-label">Email</label>
    <input class="input" type="email" placeholder="you@example.com">
  </div>
  
  <div class="form-group">
    <label class="form-label">Message</label>
    <textarea class="textarea"></textarea>
  </div>
  
  <button class="btn btn-primary">Submit</button>
</form>
```

### Navigation

```html
<nav class="nav">
  <a class="nav-item" href="/" aria-current="page">Home</a>
  <a class="nav-item" href="/about">About</a>
  <a class="nav-item" href="/contact">Contact</a>
</nav>
```

---

## Customization

### Change Primary Color

```html
<style>
  :root {
    --color-primary-h: 280;  /* Purple hue */
    --color-primary-s: 85%;
    --color-primary-l: 60%;
  }
</style>
```

### Adjust Spacing

```html
<style>
  :root {
    --space-unit: 0.5rem;  /* 8px base instead of 4px */
  }
</style>
```

### Custom Font

```html
<style>
  :root {
    --font-sans: "Inter", -apple-system, sans-serif;
  }
</style>
```

---

## Dark Mode

### Automatic (Respects System)

```html
<!-- No code needed - automatic! -->
<body>
  <p>This automatically switches based on OS setting</p>
</body>
```

### Manual Control

```html
<!-- Force dark mode -->
<body data-theme="dark">
  <button onclick="toggleTheme()">Toggle Theme</button>
</body>

<script>
  function toggleTheme() {
    const current = document.body.dataset.theme;
    document.body.dataset.theme = current === 'dark' ? 'light' : 'dark';
  }
</script>
```

### Preset Themes

```html
<body data-theme="ocean">    <!-- Blue theme -->
<body data-theme="forest">   <!-- Green theme -->
<body data-theme="sunset">   <!-- Orange theme -->
<body data-theme="purple">   <!-- Purple theme -->
```

---

## Layout Examples

### Responsive Grid (No Media Queries)

```html
<!-- Automatically adjusts columns based on space -->
<div class="grid-auto" style="--grid-min: 300px;">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
  <div>Item 4</div>
</div>
```

### Flexbox

```html
<div class="flex items-center justify-between">
  <div>Left content</div>
  <div>Right content</div>
</div>
```

### Centered Content

```html
<div class="center">
  <div>Perfectly centered</div>
</div>
```

### Stack (Vertical Spacing)

```html
<div class="stack stack-lg">
  <p>Item with automatic spacing</p>
  <p>No manual margins needed</p>
  <p>Consistent gaps throughout</p>
</div>
```

---

## Component Showcase

### Alert Messages

```html
<div class="alert alert-success">
  ✓ Success! Your changes have been saved.
</div>

<div class="alert alert-error">
  ✗ Error: Something went wrong.
</div>

<div class="alert alert-warning">
  ⚠ Warning: Action cannot be undone.
</div>
```

### Badges

```html
<span class="badge badge-primary">New</span>
<span class="badge badge-success">Active</span>
<span class="badge badge-warning">Pending</span>
```

### Progress Bar

```html
<div class="progress">
  <div class="progress-bar" style="width: 75%"></div>
</div>
```

---

## Utility Classes

### Spacing

```html
<!-- Margin -->
<div class="m-4">      Margin all sides
<div class="mx-auto">  Center horizontally
<div class="mt-8">     Margin top

<!-- Padding -->
<div class="p-6">      Padding all sides
<div class="px-4">     Padding horizontal
<div class="py-2">     Padding vertical
```

### Typography

```html
<p class="text-xs">    Extra small
<p class="text-base">  Base size
<p class="text-xl">    Extra large
<p class="font-bold">  Bold weight
<p class="text-center"> Centered text
```

### Colors

```html
<p class="text-primary">     Primary color
<p class="text-muted">       Muted color
<div class="bg-neutral-100"> Background color
```

---

## Tips & Tricks

### Combine Utilities

```html
<div class="flex items-center gap-4 p-6 bg-white rounded-lg shadow-md">
  Combined utilities for rapid prototyping
</div>
```

### Override Component Styles

```html
<!-- Components can be customized with utilities -->
<button class="btn btn-primary px-8 rounded-full">
  Modified button
</button>
```

### Custom Token Values

```html
<!-- Set custom values on specific elements -->
<div class="stack" style="--stack-space: 3rem;">
  <p>Custom spacing for this stack only</p>
</div>
```

### Responsive Grid Width

```html
<!-- Adjust minimum column width -->
<div class="grid-auto" style="--grid-min: 200px;">
  Narrower columns that fit more per row
</div>

<div class="grid-auto" style="--grid-min: 400px;">
  Wider columns that fit fewer per row
</div>
```

---

## Next Steps

1. **Read the Documentation:** [Full README](README.md)
2. **Explore Components:** [Example Page](example.html)
3. **Learn Architecture:** [Technical Guide](ARCHITECTURE.md)
4. **View Examples:** Open `example.html` in your browser
5. **Customize:** Override tokens to match your brand

---

## Common Questions

**Q: Do I need to compile anything?**  
A: No! LayerToken is pure CSS. Just link the file and start building.

**Q: Can I use only parts of the framework?**  
A: Yes! Import individual files:
```css
@import 'layertoken-core.css';      /* Required */
@import 'layertoken-components.css'; /* Optional */
```

**Q: How do I change colors?**  
A: Override the HSL variables:
```css
:root {
  --color-primary-h: 200;  /* Hue (0-360) */
  --color-primary-s: 80%;  /* Saturation */
  --color-primary-l: 50%;  /* Lightness */
}
```

**Q: Is it mobile-friendly?**  
A: Yes! Everything is responsive by default using fluid sizing and auto-adaptive grids.

**Q: Does it work with React/Vue/Svelte?**  
A: Yes! It's framework-agnostic. Just add the class names to your components.

---

## Get Help

- **Documentation:** [README.md](README.md)
- **Examples:** [example.html](example.html)
- **Architecture:** [ARCHITECTURE.md](ARCHITECTURE.md)
- **GitHub Issues:** [Report bugs or request features](#)
- **Discussions:** [Ask questions](#)

---

**Happy Building! 🎨**
