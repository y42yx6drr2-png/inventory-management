<template>
  <!-- Modern sidebar layout: sidebar on left, content on right -->
  <div class="app">
    <!-- AppSidebar handles navigation, mobile drawer, user profile, and collapse state -->
    <AppSidebar
      :is-open="isMobileMenuOpen"
      :is-collapsed="isSidebarCollapsed"
      @toggle="toggleMobileMenu"
      @toggle-collapse="toggleSidebarCollapse"
    />

    <!-- Main layout container: holds filter bar and page content -->
    <!-- Margin adjusts dynamically based on sidebar collapsed state (desktop only) -->
    <div class="main-layout" :class="{ 'sidebar-collapsed': isSidebarCollapsed }">
      <FilterBar />
      <main class="main-content">
        <router-view />
      </main>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import FilterBar from './components/FilterBar.vue'
import AppSidebar from './components/AppSidebar.vue'

export default {
  name: 'App',
  components: {
    FilterBar,
    AppSidebar
  },
  setup() {
    // Mobile menu state management
    // Controls whether the sidebar drawer is visible on mobile devices (<768px)
    const isMobileMenuOpen = ref(false)

    // Sidebar collapse state (desktop only)
    // Controls whether sidebar is in icons-only mode (64px) or full width (260px)
    // Persisted in localStorage to maintain user preference across sessions
    const isSidebarCollapsed = ref(false)

    // Toggle mobile menu drawer
    const toggleMobileMenu = () => {
      isMobileMenuOpen.value = !isMobileMenuOpen.value
    }

    // Toggle sidebar collapse state
    // Saves preference to localStorage for persistence across page reloads
    const toggleSidebarCollapse = () => {
      isSidebarCollapsed.value = !isSidebarCollapsed.value
      localStorage.setItem('sidebarCollapsed', isSidebarCollapsed.value.toString())
    }

    // Load collapse state from localStorage on mount
    // This restores the user's sidebar preference from their last session
    onMounted(() => {
      const savedState = localStorage.getItem('sidebarCollapsed')
      if (savedState !== null) {
        isSidebarCollapsed.value = savedState === 'true'
      }
    })

    return {
      isMobileMenuOpen,
      isSidebarCollapsed,
      toggleMobileMenu,
      toggleSidebarCollapse
    }
  }
}
</script>

<style>
/* Import design system variables and base styles */
@import './styles/design-system.css';

/* Main app container - uses flexbox to position sidebar and content */
/* Layout structure: sidebar (fixed left) + main-layout (scrollable right) */
.app {
  display: flex;
  min-height: 100vh;
}

/* Main layout container - holds filter bar and page content */
/* On desktop: shifted right by sidebar width */
/* On mobile: full width with sidebar as overlay drawer */
/* Margin adjusts dynamically based on sidebar collapsed state */
.main-layout {
  flex: 1;
  margin-left: var(--sidebar-width); /* 260px on desktop */
  transition: margin-left 200ms ease;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* Adjust margin when sidebar is collapsed (64px instead of 260px) */
.main-layout.sidebar-collapsed {
  margin-left: 64px;
}

/* Main content area - where router-view renders pages */
.main-content {
  flex: 1;
  padding: var(--space-6);
  max-width: 1400px;
  width: 100%;
}

/* Mobile responsive: remove sidebar margin, let sidebar be overlay drawer */
@media (max-width: 768px) {
  .main-layout {
    margin-left: 0;
  }

  .main-content {
    padding: var(--space-4);
  }
}
</style>
