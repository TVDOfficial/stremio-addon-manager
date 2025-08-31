<script setup>
defineProps({
  addonName: {
    type: String,
    required: true
  },
  addonLogo: {
    type: String,
    required: false
  },
  addonSummary: {
    type: String,
    required: false
  },
  addonTagline: {
    type: String,
    required: false
  }
})
</script>

<template>
  <section class="hero-section">
    <div class="hero-card card fade-in">
      <div class="hero-content text-center">
        <div class="hero-logo mb-4">
          <img v-if="addonLogo" :src="addonLogo" alt="Addon logo" class="logo-image" />
          <div v-else class="logo-placeholder">
            <i class="uil uil-puzzle-piece"></i>
          </div>
        </div>
        
        <h1 class="hero-title mb-3">{{ addonName }}</h1>
        
        <p class="hero-summary mb-4">
          {{ addonSummary }}
        </p>
        
        <div class="hero-tagline">
          <span class="tagline-badge">
            <i class="uil uil-check-circle"></i>
            {{ addonTagline }}
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  padding: 3rem 0;
  min-height: 60vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-card {
  max-width: 800px;
  width: 100%;
  text-align: center;
  background: linear-gradient(135deg, var(--bg-secondary-color) 0%, var(--bg-tertiary-color) 100%);
  border: none;
  box-shadow: var(--shadow-xl);
}

.hero-content {
  padding: 3rem 2rem;
}

.hero-logo {
  margin-bottom: 2rem;
}

.logo-image {
  width: 180px;
  height: 180px;
  object-fit: contain;
  border-radius: var(--radius-xl);
  background: var(--bg-color);
  padding: 1.5rem;
  box-shadow: var(--shadow-lg);
}

.logo-placeholder {
  width: 180px;
  height: 180px;
  margin: 0 auto;
  background: linear-gradient(135deg, var(--primary-color), var(--primary-hover));
  border-radius: var(--radius-xl);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: var(--shadow-lg);
}

.logo-placeholder i {
  font-size: 4rem;
  color: white;
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  background: linear-gradient(135deg, var(--primary-color), var(--primary-hover));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 1.5rem;
}

.hero-summary {
  font-size: 1.25rem;
  font-weight: 400;
  color: var(--font-secondary);
  max-width: 600px;
  margin: 0 auto 2rem auto;
  line-height: 1.6;
}

.hero-tagline {
  display: flex;
  justify-content: center;
}

.tagline-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: var(--bg-color);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-xl);
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--font-secondary);
  box-shadow: var(--shadow-sm);
}

.tagline-badge i {
  color: var(--success-color);
  font-size: 1rem;
}

@media (max-width: 768px) {
  .hero-section {
    padding: 2rem 0;
    min-height: 50vh;
  }
  
  .hero-content {
    padding: 2rem 1rem;
  }
  
  .hero-title {
    font-size: 2rem;
  }
  
  .hero-summary {
    font-size: 1.125rem;
  }
  
  .logo-image,
  .logo-placeholder {
    width: 120px;
    height: 120px;
  }
  
  .logo-placeholder i {
    font-size: 2.5rem;
  }
}
</style>
