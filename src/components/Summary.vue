<template>
  <section id="features" class="features-section">
    <div class="container">
      <div class="section-header text-center mb-5">
        <h2 class="section-title">Why Use This Tool?</h2>
        <p class="section-subtitle">A powerful solution for managing your Stremio addon order</p>
      </div>

      <div class="features-grid">
        <!-- Problem Card -->
        <div class="feature-card card">
          <div class="card-header">
            <div class="card-header-content">
              <i class="uil uil-exclamation-triangle card-icon warning"></i>
              <div>
                <h3 class="card-title">The Problem</h3>
                <p class="card-subtitle">Current limitations in Stremio</p>
              </div>
            </div>
          </div>
          <div class="card-body">
            <p>
              Stremio currently doesn't allow users to change the order that their
              installed addons appear on the home screen. As a workaround, users often
              remove and re-install addons in the order they want them to appear.
              This is a tedious and cumbersome process.
            </p>
            <div class="warning-box">
              <i class="uil uil-exclamation-circle"></i>
              <p><strong>Important:</strong> This is a <strong>workaround</strong> and not a <strong>solution</strong>.
              It is not recommended to use this tool unless you are comfortable with the
              risks involved. <strong>No support or warranty is given.</strong></p>
            </div>
          </div>
        </div>

        <!-- Solution Card -->
        <div class="feature-card card">
          <div class="card-header">
            <div class="card-header-content">
              <i class="uil uil-lightbulb card-icon success"></i>
              <div>
                <h3 class="card-title">Our Solution</h3>
                <p class="card-subtitle">Smart addon management</p>
              </div>
            </div>
          </div>
          <div class="card-body">
            <p>
              This addon uses the internal Stremio API to manipulate addon order without having to
              add/remove them. Simply drag and drop to reorder your addons and sync the changes
              back to your profile.
            </p>
            <div class="benefits-list">
              <div class="benefit-item">
                <i class="uil uil-check-circle"></i>
                <span>No need to reinstall addons</span>
              </div>
              <div class="benefit-item">
                <i class="uil uil-check-circle"></i>
                <span>Drag and drop interface</span>
              </div>
              <div class="benefit-item">
                <i class="uil uil-check-circle"></i>
                <span>Instant sync to Stremio</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Security Card -->
        <div class="feature-card card">
          <div class="card-header">
            <div class="card-header-content">
              <i class="uil uil-shield-check card-icon primary"></i>
              <div>
                <h3 class="card-title">Security & Privacy</h3>
                <p class="card-subtitle">Your data is safe with us</p>
              </div>
            </div>
          </div>
          <div class="card-body">
            <p>
              We take your privacy seriously. Your credentials and data are handled securely and only used for their intended purpose.
            </p>
            <div class="security-list">
              <div class="security-item">
                <i class="uil uil-lock"></i>
                <div>
                  <h4>Direct to Stremio</h4>
                  <p>All data goes directly to Stremio's official API (api.strem.io)</p>
                </div>
              </div>
              <div class="security-item">
                <i class="uil uil-eye-slash"></i>
                <div>
                  <h4>No Storage</h4>
                  <p>Credentials are never stored - they're only kept in memory during your session</p>
                </div>
              </div>
              <div class="security-item">
                <i class="uil uil-server"></i>
                <div>
                  <h4>No Backend</h4>
                  <p>This app has no server - everything happens in your browser</p>
                </div>
              </div>
              <div class="security-item">
                <i class="uil uil-code-branch"></i>
                <div>
                  <h4>Open Source</h4>
                  <p>View the source code to verify there's no hidden functionality</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- How It Works Card -->
        <div class="feature-card card">
          <div class="card-header">
            <div class="card-header-content">
              <i class="uil uil-process card-icon primary"></i>
              <div>
                <h3 class="card-title">How It Works</h3>
                <p class="card-subtitle">Simple 4-step process</p>
              </div>
            </div>
          </div>
          <div class="card-body">
            <div class="steps-list">
              <div class="step-item">
                <div class="step-number">1</div>
                <div class="step-content">
                  <h4>Connect Account</h4>
                  <p>Use your Stremio credentials or AuthKey to connect</p>
                </div>
              </div>
              <div class="step-item">
                <div class="step-number">2</div>
                <div class="step-content">
                  <h4>Load Addons</h4>
                  <p>Fetch your current addon collection</p>
                </div>
              </div>
              <div class="step-item">
                <div class="step-number">3</div>
                <div class="step-content">
                  <h4>Reorder</h4>
                  <p>Drag and drop to arrange addons as desired</p>
                </div>
              </div>
              <div class="step-item">
                <div class="step-number">4</div>
                <div class="step-content">
                  <h4>Sync</h4>
                  <p>Apply changes back to your Stremio profile</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.features-section {
  padding: 4rem 0;
  background: var(--bg-secondary-color);
}

.section-header {
  margin-bottom: 3rem;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, var(--primary-color), var(--primary-hover));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  font-size: 1.125rem;
  color: var(--font-secondary);
  max-width: 600px;
  margin: 0 auto;
}

.features-grid {
  display: grid;
  gap: 2rem;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
}

.feature-card {
  height: fit-content;
  backdrop-filter: blur(10px);
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.dark .feature-card {
  background: rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.card-header-content {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.card-icon {
  font-size: 1.5rem;
  padding: 0.75rem;
  border-radius: var(--radius-lg);
  background: var(--bg-tertiary-color);
}

.card-icon.primary {
  color: var(--primary-color);
}

.card-icon.success {
  color: var(--success-color);
}

.card-icon.warning {
  color: var(--warning-color);
}

.card-body {
  padding-top: 1rem;
}

.warning-box {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  padding: 1rem;
  background: rgba(245, 158, 11, 0.1);
  border: 1px solid rgba(245, 158, 11, 0.2);
  border-radius: var(--radius-md);
  margin-top: 1rem;
}

.warning-box i {
  color: var(--warning-color);
  font-size: 1.25rem;
  margin-top: 0.125rem;
}

.warning-box p {
  margin: 0;
  font-size: 0.875rem;
  color: var(--font-color);
}

.benefits-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  margin-top: 1rem;
}

.benefit-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 0.875rem;
  color: var(--font-color);
}

.benefit-item i {
  color: var(--success-color);
  font-size: 1rem;
}

.security-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 1rem;
}

.security-item {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  padding: 0.75rem;
  background: rgba(99, 102, 241, 0.05);
  border-radius: var(--radius-md);
  border: 1px solid rgba(99, 102, 241, 0.1);
}

.security-item i {
  color: var(--primary-color);
  font-size: 1.25rem;
  margin-top: 0.125rem;
  flex-shrink: 0;
}

.security-item h4 {
  font-size: 0.875rem;
  font-weight: 600;
  color: var(--font-color);
  margin: 0 0 0.25rem 0;
}

.security-item p {
  font-size: 0.75rem;
  color: var(--font-secondary);
  margin: 0;
  line-height: 1.4;
}

.steps-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.step-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.step-number {
  width: 2rem;
  height: 2rem;
  background: var(--primary-color);
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 0.875rem;
  flex-shrink: 0;
}

.step-content h4 {
  font-size: 1rem;
  font-weight: 600;
  color: var(--font-color);
  margin: 0 0 0.25rem 0;
}

.step-content p {
  font-size: 0.875rem;
  color: var(--font-secondary);
  margin: 0;
}

@media (max-width: 768px) {
  .features-section {
    padding: 2rem 0;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .features-grid {
    grid-template-columns: 1fr;
  }
  
  .card-header-content {
    flex-direction: column;
    text-align: center;
    gap: 0.75rem;
  }
}
</style>
