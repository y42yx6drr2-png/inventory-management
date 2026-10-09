<template>
  <div class="sidebar-wrapper">
    <!-- Mobile overlay - clicks on backdrop close the drawer -->
    <div
      v-if="isOpen"
      class="mobile-overlay"
      @click="$emit('toggle')"
    ></div>

    <!-- Sidebar container - slides in/out on mobile, always visible on desktop -->
    <!-- Collapse state applies to desktop only, reducing width to 64px (icons-only mode) -->
    <aside class="sidebar" :class="{ 'sidebar-open': isOpen, 'collapsed': isCollapsed }">
      <!-- Logo/Brand Section -->
      <div class="sidebar-header">
        <div class="logo-container">
          <div class="logo-icon">
            <!-- Company logo icon - simple geometric shape -->
            <svg width="32" height="32" viewBox="0 0 32 32" fill="none">
              <rect x="4" y="4" width="24" height="24" rx="4" stroke="#6366f1" stroke-width="2"/>
              <path d="M12 16L14 18L20 12" stroke="#6366f1" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
          <div class="brand-text">
            <h2 class="company-name">{{ t('nav.companyName') }}</h2>
            <p class="company-subtitle">{{ t('nav.subtitle') }}</p>
          </div>
        </div>

        <!-- Collapse toggle button (desktop only) -->
        <!-- Chevron icon rotates 180deg when collapsed to indicate expand direction -->
        <button
          class="collapse-toggle"
          @click="$emit('toggle-collapse')"
          :title="isCollapsed ? 'Expand sidebar' : 'Collapse sidebar'"
        >
          <svg
            width="20"
            height="20"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            :class="{ 'chevron-collapsed': isCollapsed }"
          >
            <polyline points="15 18 9 12 15 6"></polyline>
          </svg>
        </button>
      </div>

      <!-- Navigation Links -->
      <nav class="sidebar-nav">
        <router-link
          v-for="link in navLinks"
          :key="link.path"
          :to="link.path"
          class="nav-link"
          :class="{ 'nav-link-active': isActiveRoute(link.path) }"
          :title="link.label"
          @click="handleLinkClick"
        >
          <!-- Inline SVG icons for each navigation item -->
          <component :is="link.icon" class="nav-icon" />
          <span class="nav-text">{{ link.label }}</span>
        </router-link>
      </nav>

      <!-- Profile/User Section at Bottom -->
      <div class="sidebar-footer">
        <div class="user-profile">
          <div class="user-avatar">
            {{ userInitials }}
          </div>
          <div class="user-info">
            <p class="user-name">{{ currentUser.name }}</p>
            <p class="user-role">{{ currentUser.role }}</p>
          </div>
        </div>
      </div>
    </aside>
  </div>
</template>

<script setup>
import { computed, h } from 'vue'
import { useRoute } from 'vue-router'
import { useI18n } from '../composables/useI18n'
import { useAuth } from '../composables/useAuth'

// Props for mobile drawer state and collapse state
defineProps({
  isOpen: {
    type: Boolean,
    default: false
  },
  isCollapsed: {
    type: Boolean,
    default: false
  }
})

// Emit toggle event for mobile menu and collapse toggle
const emit = defineEmits(['toggle', 'toggle-collapse'])

const route = useRoute()
const { t } = useI18n()
const { currentUser } = useAuth()

// SVG Icon Components (Heroicons style - 24x24, stroke-width 2)
const DashboardIcon = () => h('svg', {
  width: 24,
  height: 24,
  viewBox: '0 0 24 24',
  fill: 'none',
  stroke: 'currentColor',
  'stroke-width': '2',
  'stroke-linecap': 'round',
  'stroke-linejoin': 'round'
}, [
  h('rect', { x: '3', y: '3', width: '7', height: '7' }),
  h('rect', { x: '14', y: '3', width: '7', height: '7' }),
  h('rect', { x: '14', y: '14', width: '7', height: '7' }),
  h('rect', { x: '3', y: '14', width: '7', height: '7' })
])

const InventoryIcon = () => h('svg', {
  width: 24,
  height: 24,
  viewBox: '0 0 24 24',
  fill: 'none',
  stroke: 'currentColor',
  'stroke-width': '2',
  'stroke-linecap': 'round',
  'stroke-linejoin': 'round'
}, [
  h('path', { d: 'M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z' }),
  h('polyline', { points: '3.27 6.96 12 12.01 20.73 6.96' }),
  h('line', { x1: '12', y1: '22.08', x2: '12', y2: '12' })
])

const OrdersIcon = () => h('svg', {
  width: 24,
  height: 24,
  viewBox: '0 0 24 24',
  fill: 'none',
  stroke: 'currentColor',
  'stroke-width': '2',
  'stroke-linecap': 'round',
  'stroke-linejoin': 'round'
}, [
  h('path', { d: 'M9 5H7a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2h-2' }),
  h('rect', { x: '9', y: '3', width: '6', height: '4', rx: '1' }),
  h('path', { d: 'M9 12h6' }),
  h('path', { d: 'M9 16h6' })
])

const FinanceIcon = () => h('svg', {
  width: 24,
  height: 24,
  viewBox: '0 0 24 24',
  fill: 'none',
  stroke: 'currentColor',
  'stroke-width': '2',
  'stroke-linecap': 'round',
  'stroke-linejoin': 'round'
}, [
  h('line', { x1: '12', y1: '1', x2: '12', y2: '23' }),
  h('path', { d: 'M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6' })
])

const DemandIcon = () => h('svg', {
  width: 24,
  height: 24,
  viewBox: '0 0 24 24',
  fill: 'none',
  stroke: 'currentColor',
  'stroke-width': '2',
  'stroke-linecap': 'round',
  'stroke-linejoin': 'round'
}, [
  h('polyline', { points: '23 6 13.5 15.5 8.5 10.5 1 18' }),
  h('polyline', { points: '17 6 23 6 23 12' })
])

const ReportsIcon = () => h('svg', {
  width: 24,
  height: 24,
  viewBox: '0 0 24 24',
  fill: 'none',
  stroke: 'currentColor',
  'stroke-width': '2',
  'stroke-linecap': 'round',
  'stroke-linejoin': 'round'
}, [
  h('path', { d: 'M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z' }),
  h('polyline', { points: '14 2 14 8 20 8' }),
  h('line', { x1: '16', y1: '13', x2: '8', y2: '13' }),
  h('line', { x1: '16', y1: '17', x2: '8', y2: '17' }),
  h('line', { x1: '10', y1: '9', x2: '8', y2: '9' })
])

// Navigation links configuration
const navLinks = computed(() => [
  {
    path: '/',
    label: t('nav.overview'),
    icon: DashboardIcon
  },
  {
    path: '/inventory',
    label: t('nav.inventory'),
    icon: InventoryIcon
  },
  {
    path: '/orders',
    label: t('nav.orders'),
    icon: OrdersIcon
  },
  {
    path: '/spending',
    label: t('nav.finance'),
    icon: FinanceIcon
  },
  {
    path: '/demand',
    label: t('nav.demandForecast'),
    icon: DemandIcon
  },
  {
    path: '/reports',
    label: 'Reports', // Not in translation files yet
    icon: ReportsIcon
  }
])

// Active route detection - checks if current route path matches link
// This is needed because vue-router's active-class doesn't work well with our custom styling
const isActiveRoute = (path) => {
  return route.path === path
}

// Get user initials for avatar display
const userInitials = computed(() => {
  if (!currentUser.value?.name) return 'U'
  const names = currentUser.value.name.split(' ')
  if (names.length >= 2) {
    return (names[0][0] + names[names.length - 1][0]).toUpperCase()
  }
  return names[0][0].toUpperCase()
})

// Close mobile drawer when a link is clicked
// This improves mobile UX by auto-closing the drawer after navigation
const handleLinkClick = () => {
  if (window.innerWidth < 768) {
    emit('toggle')
  }
}
</script>

<style scoped>
/* Sidebar wrapper - handles mobile overlay */
.sidebar-wrapper {
  position: relative;
}

/* Mobile overlay - darkens background when drawer is open */
.mobile-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  z-index: 998;
  display: none;
}

/* Main sidebar container */
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 260px;
  height: 100vh;
  background: white;
  border-right: 1px solid #e2e8f0;
  display: flex;
  flex-direction: column;
  z-index: 999;
  transition: transform 200ms ease-in-out, width 200ms ease-in-out;
  box-shadow: 2px 0 8px rgba(0, 0, 0, 0.05);
}

/* Collapsed sidebar state - icons-only mode (desktop only) */
/* Width reduces to 64px, all text hidden, icons centered */
.sidebar.collapsed {
  width: 64px;
}

/* Sidebar Header - Logo and Brand */
.sidebar-header {
  padding: 24px;
  border-bottom: 1px solid #e2e8f0;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo-container {
  display: flex;
  align-items: center;
  gap: 12px;
  min-width: 0;
  flex: 1;
}

.logo-icon {
  flex-shrink: 0;
}

.brand-text {
  min-width: 0;
  transition: opacity 200ms ease-in-out;
}

/* Hide brand text when collapsed */
.sidebar.collapsed .brand-text {
  opacity: 0;
  width: 0;
  overflow: hidden;
}

.company-name {
  font-size: 18px;
  font-weight: 700;
  color: #0f172a;
  margin: 0;
  line-height: 1.2;
}

.company-subtitle {
  font-size: 12px;
  color: #64748b;
  margin: 4px 0 0 0;
  line-height: 1.2;
}

/* Collapse toggle button - desktop only */
.collapse-toggle {
  flex-shrink: 0;
  width: 32px;
  height: 32px;
  border: none;
  background: transparent;
  color: #64748b;
  border-radius: 6px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 150ms ease-in-out;
  padding: 0;
}

.collapse-toggle:hover {
  background: #eef2ff;
  color: #6366f1;
}

/* Rotate chevron icon 180deg when collapsed to point right */
.chevron-collapsed {
  transform: rotate(180deg);
}

/* Hide collapse toggle on mobile */
@media (max-width: 767px) {
  .collapse-toggle {
    display: none;
  }
}

/* Center logo when collapsed */
.sidebar.collapsed .logo-container {
  justify-content: center;
}

.sidebar.collapsed .collapse-toggle {
  position: absolute;
  right: 8px;
  top: 50%;
  transform: translateY(-50%);
}

/* Navigation Section */
.sidebar-nav {
  flex: 1;
  padding: 16px;
  overflow-y: auto;
}

.nav-link {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  margin-bottom: 4px;
  border-radius: 8px;
  text-decoration: none;
  color: #64748b;
  font-size: 15px;
  font-weight: 500;
  transition: all 150ms ease-in-out;
  cursor: pointer;
}

.nav-link:hover {
  background: #eef2ff;
  color: #4f46e5;
}

/* Active link styling - indigo background with white text */
.nav-link-active {
  background: #6366f1;
  color: white;
}

.nav-link-active:hover {
  background: #4f46e5;
  color: white;
}

.nav-icon {
  flex-shrink: 0;
  width: 24px;
  height: 24px;
}

.nav-text {
  flex: 1;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  transition: opacity 200ms ease-in-out;
}

/* Hide nav text when collapsed, center nav items */
.sidebar.collapsed .nav-text {
  opacity: 0;
  width: 0;
  overflow: hidden;
}

.sidebar.collapsed .nav-link {
  justify-content: center;
  padding: 12px;
  gap: 0;
}

/* Sidebar Footer - User Profile */
.sidebar-footer {
  padding: 16px;
  border-top: 1px solid #e2e8f0;
}

.user-profile {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 8px;
  border-radius: 8px;
  transition: background 150ms ease-in-out;
  cursor: pointer;
}

.user-profile:hover {
  background: #f8fafc;
}

.user-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: linear-gradient(135deg, #6366f1, #8b5cf6);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 14px;
  flex-shrink: 0;
}

.user-info {
  min-width: 0;
  flex: 1;
}

.user-name {
  font-size: 14px;
  font-weight: 600;
  color: #0f172a;
  margin: 0;
  line-height: 1.2;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.user-role {
  font-size: 12px;
  color: #64748b;
  margin: 4px 0 0 0;
  line-height: 1.2;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Hide user info text when collapsed, center user section */
.sidebar.collapsed .user-info {
  opacity: 0;
  width: 0;
  overflow: hidden;
}

.sidebar.collapsed .user-profile {
  justify-content: center;
  padding: 12px;
}

/* Mobile Responsive - drawer slides in from left on mobile */
@media (max-width: 767px) {
  .sidebar {
    transform: translateX(-100%);
  }

  .sidebar-open {
    transform: translateX(0);
  }

  .mobile-overlay {
    display: block;
  }
}

/* Desktop - sidebar always visible, no overlay */
@media (min-width: 768px) {
  .sidebar {
    transform: translateX(0);
  }

  .mobile-overlay {
    display: none;
  }
}
</style>
