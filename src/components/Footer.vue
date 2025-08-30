<script setup>
</script>

<template>
  <footer class="footer-section">
    <div class="container">
      <div class="footer-content">
        <div class="footer-text">
          <p>Made with ❤️, 🤖 and 🥞's - enjoy!</p>
        </div>
        <div class="footer-links">
          <a href="https://github.com/pancake3000/stremio-addon-manager" target="_blank" class="footer-link">
            <i class="uil uil-github"></i>
            Source Code
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer-section {
  padding: 2rem 0;
  background: var(--bg-secondary-color);
  border-top: 1px solid var(--border-color);
  margin-top: 4rem;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}

.footer-text p {
  margin: 0;
  color: var(--font-secondary);
  font-size: 0.875rem;
}

.footer-links {
  display: flex;
  gap: 1rem;
}

.footer-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: var(--font-secondary);
  text-decoration: none;
  font-size: 0.875rem;
  font-weight: 500;
  transition: all 0.2s ease;
  padding: 0.5rem 1rem;
  border-radius: var(--radius-md);
}

.footer-link:hover {
  color: var(--primary-color);
  background: var(--bg-tertiary-color);
  transform: translateY(-1px);
}

.footer-link i {
  font-size: 1rem;
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    text-align: center;
    gap: 1rem;
  }
  
  .footer-links {
    justify-content: center;
  }
}
</style>
