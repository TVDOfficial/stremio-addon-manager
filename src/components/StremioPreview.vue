<script setup>
import { computed } from 'vue'

const props = defineProps({
  addons: {
    type: Array,
    required: true,
    default: () => []
  },
  isVisible: {
    type: Boolean,
    default: false
  }
})

const previewAddons = computed(() => {
  return props.addons.slice(0, 6) // Show first 6 addons for preview
})

const hasMoreAddons = computed(() => {
  return props.addons.length > 6
})
</script>

<template>
  <div v-if="isVisible && addons.length > 0" class="preview-section">
    <div class="container">
      <div class="preview-header text-center mb-4">
        <h3 class="preview-title">
          <i class="uil uil-eye"></i>
          Preview Your Stremio Home Page
        </h3>
        <p class="preview-subtitle">See how your addons will appear after reordering</p>
      </div>

      <div class="stremio-preview">
        <!-- Stremio Header -->
        <div class="stremio-header">
          <div class="stremio-logo">
            <i class="uil uil-play-circle"></i>
            <span>Stremio</span>
          </div>
          <div class="stremio-nav">
            <span class="nav-item active">Home</span>
            <span class="nav-item">Discover</span>
            <span class="nav-item">Library</span>
          </div>
        </div>

        <!-- Continue Watching Section -->
        <div class="stremio-section">
          <h4 class="section-title">Continue Watching</h4>
          <div class="content-row">
            <div class="content-item">
              <div class="content-poster"></div>
              <div class="content-info">
                <div class="content-title">Your Recent Content</div>
                <div class="content-subtitle">Continue where you left off</div>
              </div>
            </div>
          </div>
        </div>

        <!-- Addon Catalogs -->
        <div class="stremio-section" v-for="(addon, index) in previewAddons" :key="addon.transportUrl">
          <h4 class="section-title">{{ addon.manifest.name }}</h4>
          <div class="content-row">
            <div class="content-item" v-for="i in 4" :key="i">
              <div class="content-poster">
                <div class="poster-placeholder">
                  <i class="uil uil-image"></i>
                </div>
              </div>
              <div class="content-info">
                <div class="content-title">Content {{ i }}</div>
                <div class="content-subtitle">From {{ addon.manifest.name }}</div>
              </div>
            </div>
          </div>
        </div>

        <!-- More Addons Indicator -->
        <div class="stremio-section" v-if="hasMoreAddons">
          <div class="more-addons">
            <i class="uil uil-ellipsis-h"></i>
            <span>{{ addons.length - 6 }} more addon{{ addons.length - 6 !== 1 ? 's' : '' }}</span>
          </div>
        </div>
      </div>

      <div class="preview-footer text-center mt-4">
        <p class="preview-note">
          <i class="uil uil-info-circle"></i>
          This is a preview. Click "Sync to Stremio" to apply these changes to your actual Stremio app.
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.preview-section {
  padding: 3rem 0;
  background: var(--bg-color);
}

.preview-header {
  margin-bottom: 2rem;
}

.preview-title {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  font-size: 1.75rem;
  font-weight: 600;
  color: var(--font-color);
  margin-bottom: 0.5rem;
}

.preview-title i {
  color: var(--primary-color);
  font-size: 1.5rem;
}

.preview-subtitle {
  color: var(--font-secondary);
  font-size: 1rem;
  margin: 0;
}

.stremio-preview {
  max-width: 800px;
  margin: 0 auto;
  background: var(--bg-secondary-color);
  border-radius: var(--radius-xl);
  overflow: hidden;
  box-shadow: var(--shadow-xl);
  border: 1px solid var(--border-color);
}

.stremio-header {
  background: linear-gradient(135deg, #1e293b, #334155);
  color: white;
  padding: 1rem 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.stremio-logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-weight: 600;
  font-size: 1.25rem;
}

.stremio-logo i {
  font-size: 1.5rem;
  color: #fbbf24;
}

.stremio-nav {
  display: flex;
  gap: 1.5rem;
}

.nav-item {
  font-size: 0.875rem;
  opacity: 0.7;
  cursor: pointer;
  transition: opacity 0.2s ease;
}

.nav-item:hover {
  opacity: 1;
}

.nav-item.active {
  opacity: 1;
  font-weight: 500;
}

.stremio-section {
  padding: 1.5rem;
  border-bottom: 1px solid var(--border-color);
}

.stremio-section:last-child {
  border-bottom: none;
}

.section-title {
  font-size: 1.125rem;
  font-weight: 600;
  color: var(--font-color);
  margin: 0 0 1rem 0;
}

.content-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1rem;
}

.content-item {
  background: var(--bg-color);
  border-radius: var(--radius-lg);
  overflow: hidden;
  transition: transform 0.2s ease;
  cursor: pointer;
}

.content-item:hover {
  transform: translateY(-2px);
}

.content-poster {
  width: 100%;
  height: 100px;
  background: var(--bg-tertiary-color);
  position: relative;
}

.poster-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--font-secondary);
}

.poster-placeholder i {
  font-size: 2rem;
}

.content-info {
  padding: 0.75rem;
}

.content-title {
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--font-color);
  margin-bottom: 0.25rem;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.content-subtitle {
  font-size: 0.75rem;
  color: var(--font-secondary);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.more-addons {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 1rem;
  color: var(--font-secondary);
  font-size: 0.875rem;
}

.more-addons i {
  font-size: 1rem;
}

.preview-footer {
  margin-top: 2rem;
}

.preview-note {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  color: var(--font-secondary);
  font-size: 0.875rem;
  margin: 0;
}

.preview-note i {
  color: var(--primary-color);
}

@media (max-width: 768px) {
  .preview-section {
    padding: 2rem 0;
  }
  
  .preview-title {
    font-size: 1.5rem;
  }
  
  .stremio-header {
    flex-direction: column;
    gap: 1rem;
    text-align: center;
  }
  
  .stremio-nav {
    gap: 1rem;
  }
  
  .content-row {
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 0.75rem;
  }
  
  .content-poster {
    height: 80px;
  }
}
</style>
