# SaaS UI Redesign Skill

Transform a Vue 3 application into a modern SaaS-style interface with vertical sidebar navigation, consistent spacing, and professional polish.

## Overview

This skill redesigns Vue applications to match modern SaaS standards with:
- **Vertical sidebar navigation** (left side) instead of top navbar
- **Consistent spacing system** (4px/8px/16px/24px/32px)
- **Modern color palette** with proper contrast
- **Professional typography** with clear hierarchy
- **Polished components** with subtle shadows and transitions
- **Responsive layout** that adapts to screen sizes

## When to Use

Use this skill when you want to:
- Redesign an existing Vue app with modern SaaS aesthetics
- Replace top navigation with a sidebar layout
- Implement consistent design system spacing
- Create a more professional, polished interface
- Match the look of products like Stripe, Linear, or Notion

## Process

### Step 1: Analyze Current Structure

**IMPORTANT: You MUST delegate all Vue component analysis and modifications to the vue-expert agent.**

1. Read `client/src/App.vue` to understand current layout structure
2. List all view components in `client/src/views/`
3. Check `client/src/components/` for navigation components
4. Review `client/src/router/index.js` or routing in `main.js`
5. Identify current color scheme and spacing patterns

### Step 2: Design System Planning

Before making changes, create a design system specification:

**Color Palette:**
- Primary: Modern accent color (e.g., indigo/purple/blue)
- Background: Light gray (#f8fafc, #f1f5f9)
- Surface: White with subtle shadows
- Text: Dark slate (#0f172a primary, #64748b secondary)
- Borders: Light gray (#e2e8f0)
- Success: Green (#10b981)
- Warning: Amber (#f59e0b)
- Error: Red (#ef4444)
- Info: Blue (#3b82f6)

**Spacing Scale:**
```css
--space-1: 4px;
--space-2: 8px;
--space-3: 12px;
--space-4: 16px;
--space-5: 20px;
--space-6: 24px;
--space-8: 32px;
--space-10: 40px;
--space-12: 48px;
--space-16: 64px;
```

**Typography:**
```css
--font-sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
--text-xs: 0.75rem;    /* 12px */
--text-sm: 0.875rem;   /* 14px */
--text-base: 1rem;     /* 16px */
--text-lg: 1.125rem;   /* 18px */
--text-xl: 1.25rem;    /* 20px */
--text-2xl: 1.5rem;    /* 24px */
--text-3xl: 1.875rem;  /* 30px */
```

**Shadows:**
```css
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
--shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
--shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
```

**Border Radius:**
```css
--radius-sm: 4px;
--radius: 6px;
--radius-md: 8px;
--radius-lg: 12px;
```

### Step 3: Create Sidebar Navigation Component

**Delegate to vue-expert to create:**

Create `client/src/components/AppSidebar.vue` with:
- Fixed position sidebar (240px-280px width)
- Logo/brand at top
- Navigation links with icons
- Active state highlighting
- Hover effects
- Collapse/expand functionality (optional)
- User profile section at bottom

**Sidebar Structure:**
```
┌─────────────────┐
│  Logo/Brand     │
├─────────────────┤
│  Nav Item 1     │
│  Nav Item 2     │
│  Nav Item 3     │
│  ...            │
├─────────────────┤
│  User Profile   │
└─────────────────┘
```

**Features:**
- Icons for each navigation item (use simple SVG or Unicode icons)
- Active route highlighting
- Smooth transitions on hover/active states
- Nested navigation support (if needed)
- Responsive: collapse to icon-only on smaller screens

### Step 4: Update App Layout

**Delegate to vue-expert to modify `client/src/App.vue`:**

Transform from:
```
┌──────────────────────────┐
│     Top Navigation       │
├──────────────────────────┤
│                          │
│      Main Content        │
│                          │
└──────────────────────────┘
```

To:
```
┌─────┬────────────────────┐
│  S  │                    │
│  I  │   Main Content     │
│  D  │                    │
│  E  │                    │
│  B  │                    │
│  A  │                    │
│  R  │                    │
└─────┴────────────────────┘
```

**Layout Requirements:**
- Sidebar: Fixed position, full height
- Main content: Margin-left equal to sidebar width
- Main content: Padding for breathing room (24px-32px)
- Background: Light gray (#f8fafc or #f1f5f9)
- Content cards: White background with subtle shadow

### Step 5: Redesign View Components

**For each view in `client/src/views/`, delegate to vue-expert to:**

1. **Add consistent page structure:**
   ```vue
   <template>
     <div class="page-container">
       <!-- Page header -->
       <div class="page-header">
         <h1 class="page-title">Page Title</h1>
         <div class="page-actions">
           <!-- Action buttons -->
         </div>
       </div>
       
       <!-- Page content -->
       <div class="page-content">
         <!-- Cards, tables, etc. -->
       </div>
     </div>
   </template>
   ```

2. **Apply spacing system:**
   - Use consistent padding/margin from spacing scale
   - Add gaps between elements using CSS Grid or Flexbox gap property
   - Ensure cards have proper spacing (16px-24px padding)

3. **Style cards/panels:**
   - White background
   - Border radius (6px-8px)
   - Subtle shadow (box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1))
   - Padding: 24px
   - Margin bottom: 24px for spacing between cards

4. **Improve typography:**
   - Clear heading hierarchy (h1, h2, h3)
   - Proper font weights (600-700 for headings, 400-500 for body)
   - Line height: 1.5 for body, 1.2 for headings
   - Color contrast: Dark text on light backgrounds

5. **Enhance interactive elements:**
   - Buttons: Solid background, 8px padding, 6px border radius, smooth transitions
   - Inputs: Border, padding, focus states with primary color
   - Hover states: Subtle background color change or shadow increase
   - Transitions: 150ms-200ms ease for smooth interactions

### Step 6: Update Global Styles

**Delegate to vue-expert to update global styles in `client/src/App.vue` or create `client/src/styles/global.css`:**

```css
/* CSS Variables */
:root {
  /* Colors */
  --color-primary: #6366f1;
  --color-primary-dark: #4f46e5;
  --color-bg: #f8fafc;
  --color-surface: #ffffff;
  --color-text: #0f172a;
  --color-text-secondary: #64748b;
  --color-border: #e2e8f0;
  
  /* Spacing */
  --space-2: 8px;
  --space-4: 16px;
  --space-6: 24px;
  --space-8: 32px;
  
  /* Typography */
  --font-sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.125rem;
  --text-xl: 1.25rem;
  --text-2xl: 1.5rem;
  
  /* Shadows */
  --shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  
  /* Border Radius */
  --radius: 6px;
  --radius-md: 8px;
}

/* Base Styles */
body {
  font-family: var(--font-sans);
  background: var(--color-bg);
  color: var(--color-text);
  margin: 0;
  line-height: 1.5;
}

/* Utility Classes */
.page-container {
  padding: var(--space-6);
  max-width: 1400px;
}

.page-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-6);
}

.page-title {
  font-size: var(--text-2xl);
  font-weight: 700;
  color: var(--color-text);
  margin: 0;
}

.card {
  background: var(--color-surface);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow);
  padding: var(--space-6);
  margin-bottom: var(--space-6);
}

.btn {
  padding: 10px 16px;
  border-radius: var(--radius);
  font-weight: 500;
  cursor: pointer;
  transition: all 150ms ease;
  border: none;
  font-size: var(--text-sm);
}

.btn-primary {
  background: var(--color-primary);
  color: white;
}

.btn-primary:hover {
  background: var(--color-primary-dark);
  box-shadow: var(--shadow-md);
}
```

### Step 7: Add Navigation Icons

**Common icons needed (use simple SVG or Unicode):**
- Dashboard: 📊 or ▦
- Inventory: 📦 or ☰
- Orders: 📋 or ≡
- Reports: 📈 or ⊞
- Settings: ⚙ or ⚙️
- Spending: 💰 or $
- Demand: 📊 or ↗
- Backlog: ⏳ or ⟲

**For better icons, consider:**
- Using SVG icons from Heroicons, Lucide, or Feather
- Inline SVG in components
- Icon component wrapper for consistency

### Step 8: Responsive Design

**Delegate to vue-expert to add responsive breakpoints:**

```css
/* Mobile: Sidebar becomes top bar or drawer */
@media (max-width: 768px) {
  .sidebar {
    width: 100%;
    height: 60px;
    /* Or transform to drawer that slides in */
  }
  
  .main-content {
    margin-left: 0;
    margin-top: 60px;
  }
  
  .page-container {
    padding: var(--space-4);
  }
}

/* Tablet */
@media (min-width: 769px) and (max-width: 1024px) {
  .sidebar {
    width: 200px; /* Narrower sidebar */
  }
}
```

### Step 9: Polish & Refinements

**Final touches to delegate to vue-expert:**

1. **Transitions:**
   - Add transitions to all interactive elements
   - Page transitions between routes (optional)
   - Loading states with subtle animations

2. **Focus States:**
   - Keyboard navigation support
   - Visible focus rings on interactive elements
   - Accessible color contrast

3. **Micro-interactions:**
   - Hover effects on cards (slight lift)
   - Button press states
   - Success/error feedback animations

4. **Loading States:**
   - Skeleton screens or spinners
   - Disabled states for buttons during actions
   - Loading indicators for async data

5. **Empty States:**
   - Friendly messages when no data
   - Suggestions for next actions
   - Illustrations or icons

## Testing Checklist

After redesign, verify:
- [ ] Sidebar navigation works and highlights active route
- [ ] All views are accessible from sidebar
- [ ] Spacing is consistent across all pages
- [ ] Colors have proper contrast (WCAG AA)
- [ ] Buttons and links have hover/focus states
- [ ] Layout is responsive on mobile/tablet/desktop
- [ ] No console errors or warnings
- [ ] Smooth transitions on interactions
- [ ] Typography hierarchy is clear
- [ ] White space feels balanced (not cramped or too sparse)

## Example Before/After

**Before:**
- Top navigation bar
- Inconsistent spacing
- Basic styling
- Limited visual hierarchy

**After:**
- Modern sidebar navigation
- Consistent 8px spacing grid
- Polished components with shadows
- Clear visual hierarchy
- Professional SaaS aesthetic

## Notes

- **CRITICAL:** Always delegate Vue component work to vue-expert agent per CLAUDE.md rules
- Preserve existing functionality while improving aesthetics
- Add comments explaining non-obvious design decisions (per Code Standards)
- Test in browser after each major change
- Consider user preferences (dark mode can be added later)
- Keep performance in mind (avoid excessive shadows/effects)

## Common Pitfalls to Avoid

1. **Inconsistent spacing:** Use CSS variables, not hard-coded values
2. **Poor color contrast:** Test with accessibility tools
3. **Over-styling:** Keep it clean and functional, not flashy
4. **Breaking responsive:** Test on mobile throughout process
5. **Ignoring loading states:** Add skeletons/spinners for async data
6. **No focus states:** Ensure keyboard navigation works
7. **Too much animation:** Subtle is better than distracting

## Post-Redesign

After completing the redesign:
1. Ask user to test in browser at http://localhost:3000
2. Gather feedback on spacing, colors, layout
3. Make adjustments as needed
4. Consider creating a style guide document
5. Update any screenshots in README if applicable
