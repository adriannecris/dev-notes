# CSS Layout & Styling Guide 🎨

A comprehensive guide to modern CSS layout techniques, covering everything from basic layouts to responsive design patterns.

---

## 🏗️ Layout Fundamentals

### Flexbox vs Grid: When to Use What

**Flexbox (1D Layout)**
- Best for: Component-level layouts, navigation bars, button groups
- Strengths: Content-based sizing, alignment, distribution
- Use when: Working with a single row or column

**Grid (2D Layout)**
- Best for: Page-level layouts, complex grid systems, overlapping content
- Strengths: Precise positioning, responsive design, gap control
- Use when: Working with both rows and columns simultaneously

---

## 📐 Common Layout Patterns

### 1. Navbar Layout

**Horizontal Navigation Bar**
```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background: #fff;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.nav-brand {
  font-weight: bold;
  font-size: 1.5rem;
}

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
  margin: 0;
  padding: 0;
}

/* Responsive: Mobile hamburger menu */
@media (max-width: 768px) {
  .nav-links {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    flex-direction: column;
    background: #fff;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  }
  
  .nav-links.active {
    display: flex;
  }
  
  .hamburger {
    display: block;
    cursor: pointer;
  }
}

.hamburger {
  display: none;
  flex-direction: column;
  gap: 4px;
}

.hamburger span {
  width: 25px;
  height: 3px;
  background: #333;
  transition: 0.3s;
}
```

**[📄 Live Example: Navbar Layout](./examples/navbar-layout.html)** - Interactive navbar with hamburger menu

### 2. Sidebar Layout

**Fixed Sidebar with Main Content**
```css
.app-layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  min-height: 100vh;
}

.sidebar {
  background: #2c3e50;
  color: white;
  padding: 1rem;
  overflow-y: auto; /* Scroll if content overflows */
}

.main-content {
  padding: 1rem;
  overflow-y: auto; /* Independent scrolling */
}

/* Responsive: Mobile stack */
@media (max-width: 768px) {
  .app-layout {
    grid-template-columns: 1fr;
    grid-template-rows: auto 1fr;
  }
  
  .sidebar {
    order: 2; /* Move sidebar below main content */
  }
}
```

**Collapsible Sidebar**
```css
.sidebar {
  width: 250px;
  transition: width 0.3s ease;
}

.sidebar.collapsed {
  width: 60px;
}

.sidebar.collapsed .sidebar-text {
  display: none;
}
```

**[📄 Live Example: Sidebar Layout](./examples/sidebar-layout.html)** - Collapsible sidebar with navigation

### 3. Two-Column Layout

**Equal Columns**
```css
.two-column {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  min-height: 100vh;
}

/* Responsive: Stack on mobile */
@media (max-width: 768px) {
  .two-column {
    grid-template-columns: 1fr;
  }
}
```

**Content + Sidebar (70/30 split)**
```css
.content-sidebar {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

@media (max-width: 768px) {
  .content-sidebar {
    grid-template-columns: 1fr;
  }
}
```

**[📄 Live Examples: Two-Column Layouts](./examples/two-column-layout.html)** - Complete two-column layout examples

**Equal Columns Layout:**
**[📄 Live Example: Equal Columns](./examples/equal-columns-layout.html)** - Responsive equal-width columns

**Content + Sidebar Layout:**
**[📄 Live Example: Content + Sidebar](./examples/content-sidebar-layout.html)** - 70/30 content and sidebar layout

### 4. Full Page Layout

**Holy Grail Layout (Header, Footer, Sidebar, Main)**
```css
.holy-grail {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
  grid-template-rows: auto 1fr auto;
  grid-template-columns: 200px 1fr 200px;
  min-height: 100vh;
  gap: 1rem;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.aside { grid-area: aside; }
.footer { grid-area: footer; }

/* Responsive: Mobile single column */
@media (max-width: 768px) {
  .holy-grail {
    grid-template-areas:
      "header"
      "main"
      "sidebar"
      "aside"
      "footer";
    grid-template-columns: 1fr;
  }
}
```

**Dashboard Layout**
```css
.dashboard {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main";
  grid-template-rows: 60px 1fr;
  grid-template-columns: 250px 1fr;
  height: 100vh;
}

.dashboard-header {
  grid-area: header;
  background: #fff;
  border-bottom: 1px solid #e0e0e0;
  display: flex;
  align-items: center;
  padding: 0 1rem;
}

.dashboard-sidebar {
  grid-area: sidebar;
  background: #f5f5f5;
  overflow-y: auto;
}

.dashboard-main {
  grid-area: main;
  padding: 1rem;
  overflow-y: auto;
}
```

**[📄 Live Example: Holy Grail Layout](./examples/holy-grail-layout.html)** - Classic 3-column layout with header and footer

**[📄 Live Example: Dashboard Layout](./examples/dashboard-layout.html)** - Modern dashboard interface with sidebar and main content

---

## 📱 Responsive Design Strategies

### Mobile-First Approach
```css
/* Mobile base styles */
.container {
  padding: 1rem;
}

/* Tablet and up */
@media (min-width: 768px) {
  .container {
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .container {
    padding: 3rem;
  }
}
```

### Responsive Grid System
```css
.grid {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

/* For more control */
.responsive-grid {
  display: grid;
  gap: 1rem;
  grid-template-columns: 1fr; /* Mobile: single column */
}

@media (min-width: 768px) {
  .responsive-grid {
    grid-template-columns: repeat(2, 1fr); /* Tablet: 2 columns */
  }
}

@media (min-width: 1024px) {
  .responsive-grid {
    grid-template-columns: repeat(3, 1fr); /* Desktop: 3 columns */
  }
}
```

### Container Queries (Modern Approach)
```css
.card-container {
  container-type: inline-size;
}

.card {
  padding: 1rem;
}

@container (min-width: 400px) {
  .card {
    padding: 2rem;
    display: flex;
    gap: 1rem;
  }
}
```

**[📄 Live Example: Responsive Grid](./examples/responsive-grid.html)** - Interactive responsive grid demonstration

---

## 📏 Height, Min-Height & Overflow: The Complete Guide

### Understanding Height Properties

**`height`** - Fixed height
```css
.fixed-height {
  height: 400px; /* Exactly 400px, content may overflow */
}
```

**`min-height`** - Minimum height, grows with content
```css
.flexible-height {
  min-height: 400px; /* At least 400px, grows if needed */
}
```

**`max-height`** - Maximum height, prevents growing too much
```css
.capped-height {
  max-height: 600px; /* No more than 600px */
  overflow-y: auto; /* Scroll if content exceeds */
}
```

### When to Use Each

**Use `height` when:**
- You need exact dimensions (modals, image containers)
- Working with absolute positioning
- Creating fixed-size components

**Use `min-height` when:**
- Content length varies (blog posts, comments)
- You want responsive height
- Ensuring minimum visual presence

**Use `max-height` when:**
- Preventing content from growing too large
- Creating scrollable regions
- Responsive design with upper limits

### Overflow and Scrolling Patterns

**Basic Scrollable Container**
```css
.scrollable-content {
  height: 400px; /* Fixed height */
  overflow-y: auto; /* Vertical scroll when needed */
  overflow-x: hidden; /* Hide horizontal scroll */
  padding: 1rem;
}
```

**Full-Height Scrollable Layout**
```css
.full-height-scroll {
  height: 100vh; /* Full viewport height */
  display: flex;
  flex-direction: column;
}

.header {
  flex-shrink: 0; /* Don't shrink */
  height: 60px;
}

.scrollable-main {
  flex: 1; /* Take remaining space */
  overflow-y: auto; /* Scroll this section */
  padding: 1rem;
}

.footer {
  flex-shrink: 0; /* Don't shrink */
  height: 40px;
}
```

**Sidebar with Independent Scrolling**
```css
.layout-with-scroll {
  display: grid;
  grid-template-columns: 250px 1fr;
  height: 100vh;
}

.sidebar {
  overflow-y: auto; /* Independent scrolling */
  padding: 1rem;
}

.main-content {
  overflow-y: auto; /* Independent scrolling */
  padding: 1rem;
}
```

### Advanced Scrolling Techniques

**Custom Scrollbar Styling**
```css
.custom-scroll {
  overflow-y: auto;
}

.custom-scroll::-webkit-scrollbar {
  width: 8px;
}

.custom-scroll::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 4px;
}

.custom-scroll::-webkit-scrollbar-thumb {
  background: #c1c1c1;
  border-radius: 4px;
}

.custom-scroll::-webkit-scrollbar-thumb:hover {
  background: #a1a1a1;
}
```

**Scroll Snap for Smooth Navigation**
```css
.scroll-snap-container {
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  display: flex;
}

.scroll-snap-item {
  scroll-snap-align: start;
  flex-shrink: 0;
  width: 100%;
}
```

---

## 🎯 Practical Examples

### Card Grid Layout
```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
  padding: 1rem;
}

.card {
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  padding: 1.5rem;
  min-height: 200px; /* Ensures consistent minimum height */
}
```

### Sticky Header with Scrollable Content
```css
.page-layout {
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.sticky-header {
  position: sticky;
  top: 0;
  background: white;
  z-index: 100;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  padding: 1rem;
}

.scrollable-content {
  flex: 1;
  overflow-y: auto;
  padding: 1rem;
}
```

### Centered Modal with Backdrop
```css
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal {
  background: white;
  border-radius: 8px;
  padding: 2rem;
  max-width: 500px;
  max-height: 90vh; /* Prevent modal from being too tall */
  width: 90%;
  overflow-y: auto; /* Scroll if content is long */
}
```

**[📄 Live Example: Height and Overflow Demo](./examples/height-overflow-demo.html)** - Interactive demonstrations of height properties and overflow behaviors

---

## 💡 Best Practices & Tips

### Performance Considerations
- Use `transform` and `opacity` for animations (GPU acceleration)
- Avoid animating `height` - use `max-height` instead
- Use `will-change` sparingly for performance-critical animations

### Accessibility
- Ensure sufficient color contrast (4.5:1 for normal text)
- Use semantic HTML with proper ARIA labels
- Test with keyboard navigation
- Provide focus indicators

### Modern CSS Features
```css
/* Logical properties for international layouts */
.container {
  padding-inline: 1rem; /* left/right in LTR, right/left in RTL */
  margin-block: 2rem; /* top/bottom */
}

/* Custom properties for theming */
:root {
  --sidebar-width: 250px;
  --header-height: 60px;
  --primary-color: #3498db;
}

.layout {
  grid-template-columns: var(--sidebar-width) 1fr;
}
```

### Debugging Tips
- Use browser dev tools grid/flexbox overlays
- Add temporary borders to visualize layout
- Use `* { outline: 1px solid red; }` to debug spacing issues
- Check for collapsing margins

---

## 🔗 Quick Reference

### Flexbox Cheat Sheet
```css
.flex-container {
  display: flex;
  flex-direction: row | column;
  justify-content: flex-start | center | space-between | space-around;
  align-items: stretch | center | flex-start | flex-end;
  flex-wrap: nowrap | wrap;
  gap: 1rem;
}

.flex-item {
  flex: 1; /* grow, shrink, basis */
  align-self: auto | center | flex-start | flex-end;
}
```

### Grid Cheat Sheet
```css
.grid-container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: auto 1fr auto;
  gap: 1rem;
  grid-template-areas: "header header header";
}

.grid-item {
  grid-column: 1 / 3; /* span columns */
  grid-row: 1 / 2; /* span rows */
  grid-area: header; /* use named area */
}
```

---

*Remember: Start with semantic HTML, then layer on CSS. Mobile-first approach with progressive enhancement works best for modern responsive design.*
