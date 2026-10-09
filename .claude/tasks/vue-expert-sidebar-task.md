# Task: Create Modern SaaS Sidebar Navigation Component

Create `client/src/components/AppSidebar.vue` with the following requirements:

## Component Specifications

**Layout:**
- Fixed left sidebar, 260px width
- Indigo/purple color scheme (primary: #6366f1)
- Logo/brand section at top with company name and subtitle
- Navigation links with inline SVG icons (Heroicons style)
- Profile/user section at bottom
- Mobile drawer functionality with hamburger toggle

**Navigation Links (with SVG icons):**
1. Dashboard (/) - grid/dashboard icon
2. Inventory (/inventory) - box/package icon  
3. Orders (/orders) - clipboard/list icon
4. Finance (/spending) - currency/dollar icon
5. Demand (/demand) - trending-up/chart icon
6. Reports (/reports) - document/report icon

**Styling:**
- Active route: indigo background (#6366f1) with white text
- Inactive links: gray text (#64748b) with hover effect (lighter indigo #818cf8)
- Background: White with subtle shadow
- Text: Dark slate (#0f172a) for inactive, white for active
- Border-right: Light gray (#e2e8f0)
- Padding: Consistent 16px/24px spacing
- Border radius on active items: 8px
- Smooth transitions (150ms-200ms)

**Props & Events:**
- Props: `isOpen` (Boolean) for mobile drawer state
- Emits: `'toggle'` for mobile menu toggle

**Responsive:**
- Desktop (>=768px): Full sidebar visible
- Mobile (<768px): Drawer that slides in/out

**I18n:**
- Import `useI18n` from `'../composables/useI18n'`
- Use `t()` for text:
  - `t('nav.companyName')` - company name
  - `t('nav.subtitle')` - subtitle
  - `t('nav.overview')` - Dashboard link
  - `t('nav.inventory')` - Inventory link
  - `t('nav.orders')` - Orders link
  - `t('nav.finance')` - Finance link
  - `t('nav.demandForecast')` - Demand link
- For "Reports" link, use literal "Reports" (not in translation files yet)

**Technical:**
- Vue 3 Composition API with `<script setup>`
- Use vue-router's `useRoute()` to detect active route
- Use `computed()` for isActive checks
- Use vue-router's `router-link` with active-class styling
- Add comments explaining non-obvious logic (mobile drawer, active route detection)
- Professional inline SVG icons (24x24 size, stroke-width="2")

The component should be production-ready with smooth UX and follow all Vue 3 best practices.
