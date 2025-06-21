# CSS Fonts & Typography Guide 🔤

A comprehensive guide to typography in CSS, covering font selection, loading, optimization, and best practices for modern web design.

---

## 🎯 Font Fundamentals

### Font Properties Overview

**Core Font Properties**
```css
.text {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: 1rem;
  font-weight: 400;
  font-style: normal;
  line-height: 1.5;
  letter-spacing: 0.01em;
  text-transform: none;
}
```

**Font Shorthand**
```css
.shorthand {
  /* font: [style] [variant] [weight] size/line-height family */
  font: italic small-caps bold 16px/1.4 'Helvetica Neue', sans-serif;
}
```

---

## 📚 Font Sources & Loading

### 1. System Fonts (Best Performance)

**Modern System Font Stack**
```css
.system-fonts {
  font-family: 
    /* San Francisco on macOS and iOS */
    -apple-system,
    /* Segoe UI on Windows */
    BlinkMacSystemFont,
    'Segoe UI',
    /* Roboto on Android */
    Roboto,
    /* Oxygen on KDE */
    Oxygen,
    /* Ubuntu on Ubuntu */
    Ubuntu,
    /* Cantarell on GNOME */
    Cantarell,
    /* Noto Sans on older Android */
    'Noto Sans',
    /* Helvetica and Arial fallbacks */
    'Helvetica Neue', Arial,
    /* Generic fallback */
    sans-serif,
    /* Emoji fonts */
    'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
}
```

**Serif System Stack**
```css
.system-serif {
  font-family: 
    /* New York on newer Apple systems */
    'New York',
    /* Georgia fallback */
    Georgia,
    /* Times fallback */
    'Times New Roman', Times,
    /* Generic serif */
    serif;
}
```

**Monospace System Stack**
```css
.system-mono {
  font-family: 
    /* SF Mono on macOS */
    'SF Mono',
    /* Cascadia Code on Windows */
    'Cascadia Code',
    /* Consolas on Windows */
    Consolas,
    /* Liberation Mono on Linux */
    'Liberation Mono',
    /* Menlo fallback */
    Menlo,
    /* Monaco fallback */
    Monaco,
    /* Generic monospace */
    monospace;
}
```

### 2. Google Fonts

**HTML Loading (Fastest)**
```html
<!-- Preconnect for faster loading -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Load specific font weights and styles -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

**CSS Import (Slower)**
```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
```

**CSS with font-display**
```css
@font-face {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 400;
  font-display: swap; /* Shows fallback font immediately */
  src: url('inter-regular.woff2') format('woff2'),
       url('inter-regular.woff') format('woff');
}
```

### 3. Self-Hosted Fonts

**Modern Font Loading**
```css
@font-face {
  font-family: 'CustomFont';
  src: url('./fonts/custom-font.woff2') format('woff2'),
       url('./fonts/custom-font.woff') format('woff'),
       url('./fonts/custom-font.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

/* Usage with fallback */
.custom-text {
  font-family: 'CustomFont', -apple-system, BlinkMacSystemFont, sans-serif;
}
```

**Preloading Critical Fonts**
```html
<link rel="preload" href="./fonts/inter-regular.woff2" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="./fonts/inter-bold.woff2" as="font" type="font/woff2" crossorigin>
```

---

## ⚖️ Font Weight & Style

### Font Weight Values
```css
.font-weights {
  font-weight: 100; /* Thin */
  font-weight: 200; /* Extra Light */
  font-weight: 300; /* Light */
  font-weight: 400; /* Normal/Regular */
  font-weight: 500; /* Medium */
  font-weight: 600; /* Semi Bold */
  font-weight: 700; /* Bold */
  font-weight: 800; /* Extra Bold */
  font-weight: 900; /* Black */
}

/* Named values */
.named-weights {
  font-weight: normal;    /* 400 */
  font-weight: bold;      /* 700 */
  font-weight: lighter;   /* Relative to parent */
  font-weight: bolder;    /* Relative to parent */
}
```

### Variable Fonts
```css
@font-face {
  font-family: 'InterVariable';
  src: url('Inter-Variable.woff2') format('woff2');
  font-weight: 100 900; /* Weight range */
  font-display: swap;
}

.variable-font {
  font-family: 'InterVariable', sans-serif;
  font-weight: 450; /* Any value between 100-900 */
  font-variation-settings: 'wght' 450, 'slnt' -10;
}
```

---

## 📏 Font Sizing & Units

### Responsive Font Sizing

**rem Units (Recommended)**
```css
:root {
  font-size: 16px; /* Base font size */
}

.text-sizes {
  font-size: 0.75rem;  /* 12px */
  font-size: 0.875rem; /* 14px */
  font-size: 1rem;     /* 16px - base */
  font-size: 1.125rem; /* 18px */
  font-size: 1.25rem;  /* 20px */
  font-size: 1.5rem;   /* 24px */
  font-size: 2rem;     /* 32px */
}
```

**Fluid Typography**
```css
.fluid-text {
  /* Scales from 16px to 24px between 320px and 1200px viewport */
  font-size: clamp(1rem, 0.5rem + 2vw, 1.5rem);
}

/* More control with CSS custom properties */
:root {
  --font-size-sm: clamp(0.8rem, 0.17vw + 0.76rem, 0.89rem);
  --font-size-base: clamp(1rem, 0.34vw + 0.91rem, 1.19rem);
  --font-size-lg: clamp(1.25rem, 0.61vw + 1.1rem, 1.58rem);
  --font-size-xl: clamp(1.56rem, 1vw + 1.31rem, 2.11rem);
}
```

**Media Query Scaling**
```css
.responsive-text {
  font-size: 1rem;
}

@media (min-width: 768px) {
  .responsive-text {
    font-size: 1.125rem;
  }
}

@media (min-width: 1024px) {
  .responsive-text {
    font-size: 1.25rem;
  }
}
```

---

## 📐 Line Height & Spacing

### Line Height Best Practices
```css
.line-heights {
  /* Headings: Tighter line height */
  line-height: 1.1;  /* Large headings */
  line-height: 1.2;  /* Medium headings */
  line-height: 1.3;  /* Small headings */
  
  /* Body text: Comfortable reading */
  line-height: 1.4;  /* Dense text */
  line-height: 1.5;  /* Optimal for most text */
  line-height: 1.6;  /* Loose, accessible */
  
  /* UI elements */
  line-height: 1;    /* Buttons, labels */
}
```

### Letter & Word Spacing
```css
.spacing {
  /* Letter spacing */
  letter-spacing: -0.02em; /* Tight, for large headings */
  letter-spacing: 0;       /* Normal */
  letter-spacing: 0.01em;  /* Slightly loose */
  letter-spacing: 0.1em;   /* Very loose, for small caps */
  
  /* Word spacing */
  word-spacing: normal;
  word-spacing: 0.2em;  /* Increase word gaps */
}
```

---

## 🎨 Typography Scale & Hierarchy

### Modular Scale
```css
:root {
  /* Perfect Fourth Scale (1.333) */
  --text-xs: 0.75rem;     /* 12px */
  --text-sm: 0.875rem;    /* 14px */
  --text-base: 1rem;      /* 16px */
  --text-lg: 1.125rem;    /* 18px */
  --text-xl: 1.25rem;     /* 20px */
  --text-2xl: 1.5rem;     /* 24px */
  --text-3xl: 1.875rem;   /* 30px */
  --text-4xl: 2.25rem;    /* 36px */
  --text-5xl: 3rem;       /* 48px */
  --text-6xl: 3.75rem;    /* 60px */
}

/* Typography classes */
.text-xs { font-size: var(--text-xs); }
.text-sm { font-size: var(--text-sm); }
.text-base { font-size: var(--text-base); }
.text-lg { font-size: var(--text-lg); }
.text-xl { font-size: var(--text-xl); }
.text-2xl { font-size: var(--text-2xl); }
.text-3xl { font-size: var(--text-3xl); }
.text-4xl { font-size: var(--text-4xl); }
.text-5xl { font-size: var(--text-5xl); }
.text-6xl { font-size: var(--text-6xl); }
```

### Semantic Typography
```css
/* Heading hierarchy */
h1 {
  font-size: var(--text-4xl);
  font-weight: 700;
  line-height: 1.1;
  letter-spacing: -0.02em;
}

h2 {
  font-size: var(--text-3xl);
  font-weight: 600;
  line-height: 1.2;
}

h3 {
  font-size: var(--text-2xl);
  font-weight: 600;
  line-height: 1.3;
}

h4 {
  font-size: var(--text-xl);
  font-weight: 500;
  line-height: 1.4;
}

/* Body text */
p {
  font-size: var(--text-base);
  line-height: 1.5;
  margin-bottom: 1rem;
}

/* Small text */
small, .small {
  font-size: var(--text-sm);
  line-height: 1.4;
}
```

---

## 🔤 Text Properties & Effects

### Text Transformation & Decoration
```css
.text-transforms {
  text-transform: uppercase;    /* ALL CAPS */
  text-transform: lowercase;    /* all lowercase */
  text-transform: capitalize;   /* Title Case */
  text-transform: none;         /* Original case */
}

.text-decorations {
  text-decoration: none;
  text-decoration: underline;
  text-decoration: line-through;
  text-decoration: overline;
  
  /* Advanced decorations */
  text-decoration: underline dotted red;
  text-decoration-thickness: 2px;
  text-underline-offset: 4px;
}
```

### Text Alignment & Overflow
```css
.text-alignment {
  text-align: left;
  text-align: center;
  text-align: right;
  text-align: justify;
}

.text-overflow {
  /* Single line truncation */
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  
  /* Multi-line truncation (webkit only) */
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.word-wrapping {
  word-wrap: break-word;
  word-break: break-all;     /* Break anywhere */
  word-break: keep-all;      /* Don't break */
  hyphens: auto;             /* Auto hyphenation */
}
```

### Advanced Text Effects
```css
.text-shadow {
  /* Basic shadow */
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
  
  /* Multiple shadows */
  text-shadow: 
    1px 1px 2px rgba(0,0,0,0.3),
    3px 3px 6px rgba(0,0,0,0.2);
  
  /* Glow effect */
  text-shadow: 0 0 10px #3498db;
}

.text-stroke {
  /* Webkit text stroke */
  -webkit-text-stroke: 1px #000;
  -webkit-text-fill-color: transparent;
}

.gradient-text {
  background: linear-gradient(45deg, #3498db, #e74c3c);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

---

## 📱 Responsive Typography

### Mobile-First Typography
```css
/* Mobile base styles */
body {
  font-size: 16px;
  line-height: 1.5;
}

h1 {
  font-size: 1.75rem; /* 28px */
  line-height: 1.1;
}

h2 {
  font-size: 1.5rem; /* 24px */
  line-height: 1.2;
}

/* Tablet and up */
@media (min-width: 768px) {
  body {
    font-size: 18px;
  }
  
  h1 {
    font-size: 2.5rem; /* 40px with 18px base */
  }
  
  h2 {
    font-size: 2rem; /* 32px with 18px base */
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  h1 {
    font-size: 3rem; /* 48px with 18px base */
  }
  
  h2 {
    font-size: 2.25rem; /* 36px with 18px base */
  }
}
```

### Container Query Typography
```css
.card {
  container-type: inline-size;
}

.card h2 {
  font-size: 1.25rem;
}

@container (min-width: 400px) {
  .card h2 {
    font-size: 1.5rem;
  }
}

@container (min-width: 600px) {
  .card h2 {
    font-size: 1.75rem;
  }
}
```

---

## ♿ Accessibility & Readability

### Accessible Typography
```css
/* High contrast mode support */
@media (prefers-contrast: high) {
  body {
    color: #000;
    background: #fff;
  }
}

/* Reduced motion support */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

/* Focus indicators */
:focus-visible {
  outline: 2px solid #3498db;
  outline-offset: 2px;
}
```

### Readable Typography
```css
.readable-text {
  /* Optimal line length: 45-75 characters */
  max-width: 65ch;
  
  /* Sufficient contrast */
  color: #2c3e50;
  background: #fff;
  
  /* Comfortable line height */
  line-height: 1.6;
  
  /* Adequate font size */
  font-size: 1rem; /* 16px minimum */
  
  /* Good letter spacing */
  letter-spacing: 0.01em;
}
```

---

## 🚀 Performance Optimization

### Font Loading Strategies

**Critical Font Loading**
```html
<!-- Preload critical fonts -->
<link rel="preload" href="fonts/inter-regular.woff2" as="font" type="font/woff2" crossorigin>

<!-- Use font-display: swap -->
<style>
  @font-face {
    font-family: 'Inter';
    src: url('fonts/inter-regular.woff2') format('woff2');
    font-display: swap; /* Show fallback immediately */
  }
</style>
```

**Font Loading API**
```javascript
// Check if font is loaded
if ('fonts' in document) {
  document.fonts.ready.then(() => {
    console.log('All fonts loaded');
    document.body.classList.add('fonts-loaded');
  });
}

// Load specific font
const font = new FontFace('CustomFont', 'url(custom-font.woff2)');
font.load().then(() => {
  document.fonts.add(font);
  document.body.classList.add('custom-font-loaded');
});
```

### Font Optimization
```css
/* Only load needed weights and styles */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

/* Use unicode-range for language-specific fonts */
@font-face {
  font-family: 'CustomFont';
  src: url('custom-latin.woff2') format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153;
}

/* Subset fonts for better performance */
@font-face {
  font-family: 'IconFont';
  src: url('icons-subset.woff2') format('woff2');
  unicode-range: U+E000-E0FF; /* Private use area */
}
```

---

## 💡 Best Practices & Tips

### Font Selection Guidelines

**1. Limit Font Families**
```css
/* Good: 1-2 font families max */
:root {
  --font-primary: 'Inter', system-ui, sans-serif;
  --font-mono: 'SF Mono', Consolas, monospace;
}
```

**2. Choose Weights Wisely**
```css
/* Good: Load only needed weights */
/* Regular (400) and Semibold (600) are usually sufficient */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');
```

**3. Fallback Strategy**
```css
.robust-font-stack {
  font-family: 
    /* Custom font */
    'Inter',
    /* System alternatives */
    -apple-system, BlinkMacSystemFont, 'Segoe UI',
    /* Generic fallback */
    sans-serif;
}
```

### Performance Best Practices

**1. Use font-display: swap**
```css
@font-face {
  font-family: 'CustomFont';
  src: url('font.woff2') format('woff2');
  font-display: swap; /* Critical for performance */
}
```

**2. Preload Critical Fonts**
```html
<link rel="preload" href="critical-font.woff2" as="font" type="font/woff2" crossorigin>
```

**3. Self-Host Google Fonts**
```css
/* Better privacy and performance */
@font-face {
  font-family: 'Inter';
  src: url('./fonts/inter-regular.woff2') format('woff2');
  font-display: swap;
}
```

### Typography Design Tips

**1. Establish Hierarchy**
```css
/* Clear visual hierarchy */
h1 { font-size: 2.5rem; font-weight: 700; }
h2 { font-size: 2rem; font-weight: 600; }
h3 { font-size: 1.5rem; font-weight: 600; }
p  { font-size: 1rem; font-weight: 400; }
```

**2. Maintain Consistency**
```css
/* Use consistent spacing */
.vertical-rhythm > * + * {
  margin-top: 1.5rem;
}

/* Consistent line heights */
h1, h2, h3 { line-height: 1.2; }
p, li, div { line-height: 1.5; }
```

**3. Consider Reading Experience**
```css
.article-text {
  /* Optimal line length */
  max-width: 65ch;
  
  /* Comfortable font size */
  font-size: clamp(1rem, 2.5vw, 1.125rem);
  
  /* Good contrast */
  color: #2c3e50;
  
  /* Adequate spacing */
  line-height: 1.6;
  margin-bottom: 1.5rem;
}
```

---

## 🔧 Debugging Typography

### Common Issues & Solutions

**1. Font Not Loading**
```css
/* Check font-face declaration */
@font-face {
  font-family: 'CustomFont';
  src: url('font.woff2') format('woff2'); /* Correct path? */
  font-display: swap;
}

/* Verify font-family usage */
.text {
  font-family: 'CustomFont', sans-serif; /* Exact name match? */
}
```

**2. FOIT (Flash of Invisible Text)**
```css
/* Solution: Use font-display */
@font-face {
  font-family: 'WebFont';
  src: url('font.woff2') format('woff2');
  font-display: swap; /* Shows fallback immediately */
}
```

**3. Layout Shift**
```css
/* Solution: Match fallback metrics */
@font-face {
  font-family: 'WebFont';
  src: url('font.woff2') format('woff2');
  font-display: swap;
  ascent-override: 90%;
  descent-override: 22%;
  line-gap-override: 0%;
  size-adjust: 100%;
}
```

### Developer Tools

**Inspect Fonts**
```css
/* Add temporary borders to see font rendering */
* {
  outline: 1px solid red;
}

/* Check computed font properties */
.debug-font {
  background: rgba(255, 0, 0, 0.1);
}
```

**Font Loading Detection**
```javascript
// Check if font is available
function isFontLoaded(fontFamily) {
  const canvas = document.createElement('canvas');
  const context = canvas.getContext('2d');
  
  context.font = '12px ' + fontFamily;
  const width = context.measureText('test').width;
  
  context.font = '12px serif';
  const fallbackWidth = context.measureText('test').width;
  
  return width !== fallbackWidth;
}
```

---

## 📋 Quick Reference

### Font Property Cheat Sheet
```css
/* Font family */
font-family: 'Font Name', fallback, generic;

/* Font size */
font-size: 16px | 1rem | 1em | clamp(1rem, 2vw, 2rem);

/* Font weight */
font-weight: 100-900 | normal | bold | lighter | bolder;

/* Font style */
font-style: normal | italic | oblique;

/* Line height */
line-height: 1.5 | 24px | 150%;

/* Text properties */
text-align: left | center | right | justify;
text-decoration: none | underline | line-through;
text-transform: none | uppercase | lowercase | capitalize;
letter-spacing: normal | 0.1em | 2px;
word-spacing: normal | 0.2em | 4px;
```

### Common Font Stacks
```css
/* Sans-serif */
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;

/* Serif */
font-family: Georgia, 'Times New Roman', Times, serif;

/* Monospace */
font-family: 'SF Mono', Consolas, 'Liberation Mono', Menlo, monospace;

/* System UI */
font-family: system-ui, -apple-system, sans-serif;
```

---

*Remember: Typography is the foundation of good design. Prioritize readability, performance, and accessibility in all your font choices.*
