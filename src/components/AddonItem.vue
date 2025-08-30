<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true
  },
  idx: {
    type: Number,
    required: true
  },
  manifestURL: {
    type: String,
    required: true
  },
  logoURL: {
    type: String,
    required: false
  },
  isDeletable: {
    type: Boolean,
    required: false,
    default: true
  },
  isConfigurable: {
    type: Boolean,
    required: false,
    default: false
  }
})

const emits = defineEmits(['delete-addon'])

const defaultLogo = 'https://icongr.am/feather/box.svg?size=48&color=ffffff'

function copyManifestURLToClipboard() {
  navigator.clipboard.writeText(props.manifestURL).then(() => {
    console.log('Text copied to clipboard')
  }).catch((error) => {
    console.error('Error copying text to clipboard', error)
  })
}

function openAddonConfigurationPage() {
  const configureURL = props.manifestURL.replace("stremio://", "https://").replace("/manifest.json", "/configure");
  window.open(configureURL);
}

function removeAddon() {
  emits('delete-addon', props.idx)
}
</script>

<template>
  <div class="addon-item">
    <div class="addon-content">
      <div class="addon-info">
        <div class="addon-logo">
          <img :src="logoURL || defaultLogo" :alt="name" />
        </div>
        <div class="addon-details">
          <h4 class="addon-name">{{ name }}</h4>
          <p class="addon-position">Position {{ idx + 1 }}</p>
        </div>
      </div>
      
      <div class="addon-actions">
        <button 
          class="button icon-only action-btn configure-btn" 
          title="Open addon configuration page in new window"
          :disabled="!isConfigurable" 
          @click="openAddonConfigurationPage"
        >
          <i class="uil uil-setting"></i>
        </button>
        
        <button 
          class="button icon-only action-btn copy-btn" 
          title="Copy addon manifest URL to clipboard"
          @click="copyManifestURLToClipboard"
        >
          <i class="uil uil-copy"></i>
        </button>
        
        <button 
          class="button icon-only action-btn delete-btn" 
          title="Remove addon from list"
          :disabled="!isDeletable"
          @click="removeAddon"
        >
          <i class="uil uil-trash-alt"></i>
        </button>
      </div>
    </div>
    
    <div class="drag-handle">
      <i class="uil uil-draggabledots"></i>
    </div>
  </div>
</template>

<style scoped>
.addon-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: var(--bg-color);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-lg);
  padding: 1.25rem;
  transition: all 0.3s ease;
  cursor: move;
  position: relative;
  overflow: hidden;
}

.addon-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 4px;
  height: 100%;
  background: linear-gradient(135deg, var(--primary-color), var(--primary-hover));
  border-radius: var(--radius-sm) 0 0 var(--radius-sm);
}

.addon-item:hover {
  box-shadow: var(--shadow-lg);
  transform: translateY(-2px);
  border-color: var(--primary-color);
}

.addon-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex: 1;
  gap: 1rem;
}

.addon-info {
  display: flex;
  align-items: center;
  gap: 1rem;
  flex: 1;
}

.addon-logo {
  width: 60px;
  height: 60px;
  border-radius: var(--radius-lg);
  background: var(--bg-tertiary-color);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  flex-shrink: 0;
}

.addon-logo img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  padding: 0.5rem;
}

.addon-details {
  flex: 1;
  min-width: 0;
}

.addon-name {
  font-size: 1.125rem;
  font-weight: 600;
  color: var(--font-color);
  margin: 0 0 0.25rem 0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.addon-position {
  font-size: 0.875rem;
  color: var(--font-secondary);
  margin: 0;
  font-weight: 500;
}

.addon-actions {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  flex-shrink: 0;
}

.action-btn {
  width: 2.5rem;
  height: 2.5rem;
  border-radius: var(--radius-md);
  transition: all 0.2s ease;
  border: 1px solid var(--border-color);
  background: var(--bg-tertiary-color);
  color: var(--font-secondary);
}

.action-btn:hover {
  transform: translateY(-1px);
  box-shadow: var(--shadow-md);
}

.action-btn.configure-btn:hover {
  background: var(--primary-color);
  color: white;
  border-color: var(--primary-color);
}

.action-btn.copy-btn:hover {
  background: var(--success-color);
  color: white;
  border-color: var(--success-color);
}

.action-btn.delete-btn:hover {
  background: var(--error-color);
  color: white;
  border-color: var(--error-color);
}

.action-btn:disabled {
  opacity: 0.4;
  cursor: not-allowed;
  transform: none;
}

.action-btn:disabled:hover {
  background: var(--bg-tertiary-color);
  color: var(--font-secondary);
  border-color: var(--border-color);
  transform: none;
  box-shadow: none;
}

.drag-handle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 2rem;
  height: 2rem;
  color: var(--font-secondary);
  cursor: move;
  border-radius: var(--radius-sm);
  transition: all 0.2s ease;
  margin-left: 0.5rem;
}

.drag-handle:hover {
  background: var(--bg-tertiary-color);
  color: var(--primary-color);
}

.drag-handle i {
  font-size: 1.25rem;
}

/* Dark mode adjustments */
.dark .addon-item {
  background: var(--bg-secondary-color);
}

.dark .addon-logo {
  background: var(--bg-tertiary-color);
}

/* Responsive design */
@media (max-width: 768px) {
  .addon-item {
    padding: 1rem;
  }
  
  .addon-content {
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
  }
  
  .addon-actions {
    width: 100%;
    justify-content: flex-end;
  }
  
  .addon-logo {
    width: 50px;
    height: 50px;
  }
  
  .addon-name {
    font-size: 1rem;
  }
}
</style>
