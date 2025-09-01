<script setup>
</script>

<template>
  <footer class="footer-section">
    <div class="container">
      <!-- AdSense Ad Unit at Bottom -->
      <div class="ads-section">
        <div class="ad-note">
          <i class="uil uil-info-circle"></i>
          <span>This website is free to use. Ads help cover hosting costs and keep the service running.</span>
        </div>
        <div class="ad-container">
          <ins class="adsbygoogle"
               style="display:block"
               data-ad-client="ca-pub-7868501272007775"
               data-ad-slot="auto"
               data-ad-format="auto"
               data-full-width-responsive="true"></ins>
          <script>
               (adsbygoogle = window.adsbygoogle || []).push({});
          </script>
        </div>
      </div>
      
      <div class="footer-content">
        <div class="footer-text">
          <p>Made with ❤️, 🤖, 🥞 and 🐉's - enjoy!</p>
        </div>
        <div class="footer-links">
          <a href="https://github.com/TVDOfficial/stremio-addon-manager" target="_blank" class="footer-link">
            <i class="uil uil-github"></i>
            Source Code
          </a>
          <a href="https://github.com/pancake3000/stremio-addon-manager" target="_blank" class="footer-link">
            <i class="uil uil-code-branch"></i>
            Forked from pancake3000
          </a>
          <a href="https://paypal.me/mathewarpittard" target="_blank" class="footer-link coffee-link">
            <i class="uil uil-coffee"></i>
            Buy Me a Coffee
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

.coffee-link {
  background: linear-gradient(135deg, #ff6b35, #f7931e);
  color: white;
  border: none;
  font-weight: 600;
}

.coffee-link:hover {
  background: linear-gradient(135deg, #e55a2b, #e8851a);
  color: white;
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}

.ads-section {
  margin-bottom: 2rem;
  padding: 1.5rem;
  background: var(--bg-tertiary-color);
  border-radius: var(--radius-lg);
  border: 1px solid var(--border-color);
}

.ad-note {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
  padding: 0.75rem 1rem;
  background: var(--bg-secondary-color);
  border-radius: var(--radius-md);
  font-size: 0.875rem;
  color: var(--font-secondary);
}

.ad-note i {
  color: var(--primary-color);
  font-size: 1rem;
}

.ad-container {
  display: flex;
  justify-content: center;
  min-height: 90px;
  background: var(--bg-secondary-color);
  border-radius: var(--radius-md);
  overflow: hidden;
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
