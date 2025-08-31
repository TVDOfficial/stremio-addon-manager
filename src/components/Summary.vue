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
               <p><strong>Important:</strong> This tool has been tested and is safe to use, but we recommend <strong>backing up your addon list</strong> before making any changes. You can use the backup/restore feature in the configuration section below. <strong>We are not liable if anything breaks on your account.</strong></p>
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
              <div class="benefit-item">
                <i class="uil uil-check-circle"></i>
                <span>Backup and restore functionality</span>
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
        <div class="feature-card card how-it-works-card">
          <div class="card-header">
            <div class="card-header-content">
              <i class="uil uil-process card-icon primary"></i>
              <div>
                <h3 class="card-title">How It Works</h3>
                <p class="card-subtitle">Simple 3-step process</p>
              </div>
            </div>
          </div>
          <div class="card-body">
            <div class="process-flow">
              <div class="process-step">
                <div class="step-icon-wrapper">
                  <i class="uil uil-shield-check"></i>
                </div>
                <div class="step-content">
                  <h4>1. Authenticate</h4>
                  <p>Connect your Stremio account securely</p>
                </div>
              </div>
              
              <div class="process-arrow">
                <i class="uil uil-arrow-right"></i>
              </div>
              
              <div class="process-step">
                <div class="step-icon-wrapper">
                  <i class="uil uil-sort-amount-down"></i>
                </div>
                <div class="step-content">
                  <h4>2. Reorder</h4>
                  <p>Drag and drop to arrange addons</p>
                </div>
              </div>
              
              <div class="process-arrow">
                <i class="uil uil-arrow-right"></i>
              </div>
              
              <div class="process-step">
                <div class="step-icon-wrapper">
                  <i class="uil uil-sync"></i>
                </div>
                <div class="step-content">
                  <h4>3. Sync</h4>
                  <p>Apply changes to your Stremio profile</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Authentication Guide Card -->
        <div class="feature-card card auth-guide-card">
          <div class="card-header">
            <div class="card-header-content">
              <i class="uil uil-key-skeleton card-icon primary"></i>
              <div>
                <h3 class="card-title">How to Connect</h3>
                <p class="card-subtitle">Step-by-step authentication guide</p>
              </div>
            </div>
          </div>
          <div class="card-body">
            <div class="auth-guide">
                             <div class="guide-intro">
                 <p>Connect your Stremio account. We support 2 different authentication methods:</p>
                 <ul>
                   <li>Login using your Stremio account (Facebook login is <strong>not supported</strong>)</li>
                   <li>Login using an authentication key</li>
                 </ul>
                 <div class="backup-note">
                   <i class="uil uil-save"></i>
                   <p><strong>Pro Tip:</strong> You can also backup and restore your addon list using the export/import feature in the configuration section below!</p>
                 </div>
               </div>
              
              <div class="guide-steps">
                <div class="guide-step">
                  <div class="step-number">1</div>
                  <div class="step-content">
                    <h4>Login to Stremio Web</h4>
                    <p>Login to <a href="https://web.stremio.com/" target="_blank" rel="noopener">https://web.stremio.com/</a> using your Stremio credentials in your browser.</p>
                  </div>
                </div>
                
                                 <div class="guide-step">
                   <div class="step-number">2</div>
                   <div class="step-content">
                     <h4>Open Developer Console</h4>
                     <p>Open the developer console using one of these methods:</p>
                     <div class="console-methods">
                       <div class="method-item">
                         <strong>Windows/Linux:</strong> Press <kbd>F12</kbd> or <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd>
                       </div>
                       <div class="method-item">
                         <strong>Mac:</strong> Press <kbd>Cmd</kbd> + <kbd>Option</kbd> + <kbd>I</kbd>
                       </div>
                       <div class="method-item">
                         <strong>Alternative:</strong> Right-click anywhere on the page and select "Inspect" or "Inspect Element"
                       </div>
                     </div>
                     <p>Then paste the following code snippet in the console:</p>
                     <div class="code-block">
                       <code>JSON.parse(localStorage.getItem("profile")).auth.key</code>
                     </div>
                   </div>
                 </div>
                
                <div class="guide-step">
                  <div class="step-number">3</div>
                  <div class="step-content">
                    <h4>Copy the Output</h4>
                    <p>Take the output value and paste it into the authentication form below.</p>
                  </div>
                </div>
                
                <div class="guide-step">
                  <div class="step-number">4</div>
                  <div class="step-content">
                    <h4>Load Your Addons</h4>
                    <p>Your profile addons will load automatically after successful authentication.</p>
                  </div>
                </div>
                
                <div class="guide-step">
                  <div class="step-number">5</div>
                  <div class="step-content">
                    <h4>Reorder Addons</h4>
                    <p>Re-order your addons as you like using drag and drop.</p>
                  </div>
                </div>
                
                <div class="guide-step">
                  <div class="step-number">6</div>
                  <div class="step-content">
                    <h4>Sync Changes</h4>
                    <p>Click the 'Sync To Stremio' button to sync the changes back to your profile.</p>
                  </div>
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
  grid-template-columns: repeat(auto-fit, minmax(600px, 1fr));
  max-width: 1400px;
  margin: 0 auto;
}

.feature-card {
  height: fit-content;
  backdrop-filter: blur(10px);
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}

.dark .feature-card {
  background: rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.card-header-content {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  margin-bottom: 1rem;
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
  padding-top: 0;
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

/* How It Works Card Styles */
.how-it-works-card {
  grid-column: 1 / -1;
  max-width: 800px;
  margin: 0 auto;
}

.process-flow {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.process-step {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 0.75rem;
  flex: 1;
  min-width: 150px;
}

.step-icon-wrapper {
  width: 4rem;
  height: 4rem;
  background: linear-gradient(135deg, var(--primary-color), var(--primary-hover));
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: var(--shadow-lg);
}

.step-icon-wrapper i {
  font-size: 1.5rem;
  color: white;
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
  line-height: 1.4;
}

.process-arrow {
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--primary-color);
  font-size: 1.5rem;
  opacity: 0.7;
}

/* Authentication Guide Card Styles */
.auth-guide-card {
  grid-column: 1 / -1;
  max-width: 800px;
  margin: 0 auto;
}

.auth-guide {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.guide-intro {
  background: rgba(99, 102, 241, 0.05);
  border: 1px solid rgba(99, 102, 241, 0.1);
  border-radius: var(--radius-md);
  padding: 1.5rem;
  text-align: center;
}

.guide-intro p {
  font-size: 0.875rem;
  color: var(--font-color);
  margin-bottom: 0.75rem;
}

.guide-intro ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.guide-intro li {
  font-size: 0.875rem;
  color: var(--font-secondary);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.guide-intro li strong {
  color: var(--primary-color);
}

.backup-note {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  padding: 1rem;
  background: rgba(34, 197, 94, 0.05);
  border: 1px solid rgba(34, 197, 94, 0.1);
  border-radius: var(--radius-md);
  margin-top: 1rem;
}

.backup-note i {
  color: var(--success-color);
  font-size: 1.25rem;
  margin-top: 0.125rem;
  flex-shrink: 0;
}

.backup-note p {
  margin: 0;
  font-size: 0.875rem;
  color: var(--font-color);
  line-height: 1.4;
}

.backup-note strong {
  color: var(--success-color);
}

.guide-steps {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.guide-step {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: var(--radius-md);
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
  margin: 0 0 0.5rem 0;
}

.step-content p {
  font-size: 0.875rem;
  color: var(--font-secondary);
  margin: 0;
  line-height: 1.4;
}

.console-methods {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin: 0.75rem 0;
}

.method-item {
  font-size: 0.875rem;
  color: var(--font-color);
  padding: 0.5rem 0.75rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: var(--radius-sm);
}

.method-item strong {
  color: var(--primary-color);
}

kbd {
  background: rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  padding: 0.125rem 0.375rem;
  font-size: 0.75rem;
  font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, Courier, monospace;
  color: var(--font-color);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

.code-block {
  background: rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: var(--radius-sm);
  padding: 0.75rem 1rem;
  font-size: 0.75rem;
  color: var(--font-color);
  overflow-x: auto;
  white-space: pre-wrap;
  word-break: break-all;
  margin-top: 0.5rem;
}

.code-block code {
  font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, Courier, monospace;
  font-size: 0.875rem;
  color: var(--font-color);
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
    gap: 1.5rem;
  }
  
  .card-header-content {
    flex-direction: column;
    text-align: center;
    gap: 1rem;
    margin-bottom: 1.5rem;
  }
  
  .process-flow {
    flex-direction: column;
    gap: 1rem;
  }
  
  .process-arrow {
    transform: rotate(90deg);
  }
  
  .process-step {
    min-width: auto;
  }
  
  .guide-step {
    flex-direction: column;
    text-align: center;
  }
  
  .guide-intro ul {
    align-items: center;
  }
  
  .code-block {
    font-size: 0.7rem;
    padding: 0.5rem;
  }
  
  .backup-note {
    flex-direction: column;
    text-align: center;
  }
  
  .console-methods {
    gap: 0.25rem;
  }
  
  .method-item {
    text-align: center;
    padding: 0.75rem;
  }
}
</style>
