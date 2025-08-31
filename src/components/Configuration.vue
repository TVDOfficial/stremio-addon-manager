<script setup>
import { ref } from 'vue'
import draggable from 'vuedraggable'
import AddonItem from './AddonItem.vue'
import Authentication from './Authentication.vue'

const stremioAPIBase = "https://api.strem.io/api/"
const dragging = false
let stremioAuthKey = ref('');
let addons = ref([])
let loadAddonsButtonText = ref('Load Addons')

function loadUserAddons() {
    const key = stremioAuthKey.value
    if (!key) {
        console.error('No auth key provided')
        return
    }

    loadAddonsButtonText.value = 'Loading...'
    console.log('Loading addons...')

    const url = `${stremioAPIBase}addonCollectionGet`
    fetch(url, {
        method: 'POST',
        body: JSON.stringify({
            type: 'AddonCollectionGet',
            authKey: key,
            update: true,
        })
    }).then((resp) => {
        resp.json().then((data) => {
            console.log(data)
            if (!("result" in data) || data.result == null) {
                console.error("Failed to fetch user addons: ", data)
                alert('Failed to fetch user addons - are you sure you pasted the correct Stremio AuthKey?')
                return
            }
            addons.value = data.result.addons
        })
    }).catch((error) => {
        console.error('Error fetching user addons', error)
    }).finally(() => {
        loadAddonsButtonText.value = 'Load Addons'
    })
}

function syncUserAddons() {
    const key = stremioAuthKey.value
    if (!key) {
        console.error('No auth key provided')
        return
    }
    console.log('Syncing addons...')

    const url = `${stremioAPIBase}addonCollectionSet`
    fetch(url, {
        method: 'POST',
        body: JSON.stringify({
            type: 'AddonCollectionSet',
            authKey: key,
            addons: addons.value,
        })
    }).then((resp) => {
        resp.json().then((data) => {
            if (!("result" in data) || data.result == null) {
                console.error("Sync failed: ", data)
                alert('Sync failed if unknown error')
                return
            } else if (!data.result.success) {
                alert("Failed to sync addons: " + data.result.error)
            } else {
                console.log("Sync complete: + ", data)
                alert('Sync complete!')
            }
        })
    }).catch((error) => {
        alert("Error syncing addons: " + error)
        console.error('Error fetching user addons', error)
    })
}

function removeAddon(idx) {
    addons.value.splice(idx, 1)
}

function getNestedObjectProperty(obj, path, defaultValue = null) {
    try {
        return path.split('.').reduce((acc, part) => acc && acc[part], obj)
    } catch (e) {
        return defaultValue
    }
}

function setAuthKey(authKey) {
    stremioAuthKey.value = authKey
    console.log('AuthKey set to: ', stremioAuthKey.value)
    // Automatically load addons after successful authentication
    if (authKey) {
        loadUserAddons()
    }
}

// Backup and Restore Functions
function exportAddonOrder() {
    if (!addons.value.length) {
        alert('No addons to export. Please load your addons first.')
        return
    }
    
    const backupData = {
        version: '1.0',
        timestamp: new Date().toISOString(),
        addons: addons.value.map(addon => ({
            name: addon.manifest.name,
            transportUrl: addon.transportUrl,
            logo: addon.manifest.logo,
            description: addon.manifest.description || '',
            version: addon.manifest.version || '',
            id: addon.manifest.id || ''
        }))
    }
    
    const dataStr = JSON.stringify(backupData, null, 2)
    const dataBlob = new Blob([dataStr], { type: 'application/json' })
    
    const link = document.createElement('a')
    link.href = URL.createObjectURL(dataBlob)
    link.download = `stremio-addons-backup-${new Date().toISOString().split('T')[0]}.json`
    link.click()
    
    URL.revokeObjectURL(link.href)
}

function importAddonOrder(event) {
    const file = event.target.files[0]
    if (!file) return
    
    const reader = new FileReader()
    reader.onload = function(e) {
        try {
            const backupData = JSON.parse(e.target.result)
            
            if (!backupData.addons || !Array.isArray(backupData.addons)) {
                alert('Invalid backup file format.')
                return
            }
            
            // Convert backup format to current addon format
            const importedAddons = backupData.addons.map(addon => ({
                manifest: {
                    name: addon.name,
                    logo: addon.logo,
                    description: addon.description,
                    version: addon.version,
                    id: addon.id
                },
                transportUrl: addon.transportUrl
            }))
            
            addons.value = importedAddons
            alert(`Successfully imported ${importedAddons.length} addons from backup.`)
            
        } catch (error) {
            console.error('Error parsing backup file:', error)
            alert('Error reading backup file. Please make sure it\'s a valid JSON file.')
        }
    }
    
    reader.readAsText(file)
    // Reset the input so the same file can be selected again
    event.target.value = ''
}
</script>

<template>
    <section id="configure" class="configure-section">
        <div class="container">
            <div class="section-header text-center mb-5">
                <h2 class="section-title">Configure Your Addons</h2>
                <p class="section-subtitle">Manage and organize your Stremio addons with ease</p>
            </div>

            <div class="configure-layout">
                <!-- Centered Process Steps -->
                <div class="process-container">
                    <div class="process-list">
                        <!-- Authentication Step -->
                        <div class="process-step card">
                            <div class="step-header">
                                <div class="step-number">1</div>
                                <div class="step-info">
                                    <h3 class="step-title">Authentication</h3>
                                    <p class="step-subtitle">Connect your Stremio account</p>
                                </div>
                                <i class="uil uil-shield-check step-icon"></i>
                            </div>
                            <div class="step-content">
                                <Authentication :stremioAPIBase="stremioAPIBase" @auth-key="setAuthKey" />
                            </div>
                        </div>

                        <!-- Load Addons Step (Hidden when addons are loaded) -->
                        <div class="process-step card" v-if="!addons.length">
                            <div class="step-header">
                                <div class="step-number">2</div>
                                <div class="step-info">
                                    <h3 class="step-title">Loading Addons</h3>
                                    <p class="step-subtitle">Fetching your current addon collection...</p>
                                </div>
                                <i class="uil uil-download-alt step-icon"></i>
                            </div>
                            <div class="step-content">
                                <div class="loading-state">
                                    <div class="loading-spinner"></div>
                                    <p class="loading-text">Loading your addons...</p>
                                </div>
                            </div>
                        </div>

                        <!-- Reorder Addons Step -->
                        <div class="process-step card" v-if="addons.length > 0">
                            <div class="step-header">
                                <div class="step-number">2</div>
                                <div class="step-info">
                                    <h3 class="step-title">Reorder Addons</h3>
                                    <p class="step-subtitle">Drag and drop to change priority</p>
                                </div>
                                <i class="uil uil-sort-amount-down step-icon"></i>
                            </div>
                            <div class="step-content">
                                <div class="addons-list">
                                    <draggable 
                                        :list="addons" 
                                        item-key="transportUrl" 
                                        class="sortable-list" 
                                        ghost-class="ghost"
                                        @start="dragging = true" 
                                        @end="dragging = false"
                                    >
                                        <template #item="{ element, index }">
                                            <AddonItem 
                                                :name="element.manifest.name" 
                                                :idx="index" 
                                                :manifestURL="element.transportUrl"
                                                :logoURL="element.manifest.logo"
                                                :isDeletable="!getNestedObjectProperty(element, 'flags.protected', false)"
                                                :isConfigurable="getNestedObjectProperty(element, 'manifest.behaviorHints.configurable', false)"
                                                @delete-addon="removeAddon" 
                                            />
                                        </template>
                                    </draggable>
                                </div>
                            </div>
                        </div>

                        <!-- Sync Addons Step -->
                        <div class="process-step card" v-if="addons.length > 0">
                            <div class="step-header">
                                <div class="step-number">3</div>
                                <div class="step-info">
                                    <h3 class="step-title">Sync Changes</h3>
                                    <p class="step-subtitle">Apply your changes to Stremio</p>
                                </div>
                                <i class="uil uil-sync step-icon"></i>
                            </div>
                            <div class="step-content">
                                <button type="button" class="button success w-full" @click="syncUserAddons">
                                    <i class="uil uil-cloud-upload"></i>
                                    Sync to Stremio
                                </button>
                                <p class="help-text mt-2">
                                    <i class="uil uil-clock"></i>
                                    This will update your addon order in Stremio
                                </p>
                            </div>
                        </div>

                        <!-- Backup & Restore Step -->
                        <div class="process-step card" v-if="addons.length > 0">
                            <div class="step-header">
                                <div class="step-number">4</div>
                                <div class="step-info">
                                    <h3 class="step-title">Backup & Restore</h3>
                                    <p class="step-subtitle">Save or load your addon configuration</p>
                                </div>
                                <i class="uil uil-save step-icon"></i>
                            </div>
                            <div class="step-content">
                                <div class="backup-actions">
                                    <button type="button" class="button primary" @click="exportAddonOrder">
                                        <i class="uil uil-download-alt"></i>
                                        Export Backup
                                    </button>
                                    <div class="import-wrapper">
                                        <input 
                                            type="file" 
                                            id="import-file" 
                                            accept=".json" 
                                            @change="importAddonOrder" 
                                            style="display: none;"
                                        />
                                        <button type="button" class="button secondary" onclick="document.getElementById('import-file').click()">
                                            <i class="uil uil-upload-alt"></i>
                                            Import Backup
                                        </button>
                                    </div>
                                </div>
                                <div class="backup-info">
                                    <p><i class="uil uil-info-circle"></i> Export your current addon order as a JSON file. You can import this backup on other devices or after reinstalling Stremio.</p>
                                </div>
                            </div>
                        </div>

                        <!-- Popular Addons Section -->
                        <div class="popular-addons-section">
                            <div class="section-header text-center mb-5">
                                <h3 class="section-title">Popular Addons</h3>
                                <p class="section-subtitle">Add these recommended addons to your profile</p>
                            </div>
                            
                            <div class="addons-grid">
                                <div class="addon-item">
                                    <div class="addon-info">
                                        <h4>Torrentio</h4>
                                        <p class="addon-description">Provides torrent streams from scraped torrent providers. Supports YTS, EZTV, RARBG, 1337x, ThePirateBay, and many more with RealDebrid/Premiumize support.</p>
                                        <div class="addon-features">
                                            <span class="feature-tag">Movies</span>
                                            <span class="feature-tag">Series</span>
                                            <span class="feature-tag">Anime</span>
                                            <span class="feature-tag">Debrid Support</span>
                                        </div>
                                    </div>
                                    <div class="addon-actions">
                                        <a href="https://torrentio.strem.fun/configure" target="_blank" rel="noopener" class="btn btn-primary">
                                            <i class="uil uil-external-link-alt"></i>
                                            Configure & Install
                                        </a>
                                    </div>
                                </div>
                                
                                <div class="addon-item">
                                    <div class="addon-info">
                                        <h4>AIO Streams</h4>
                                        <p class="addon-description">All-in-one streaming addon with multiple sources including direct links, torrents, and various streaming platforms for movies and TV shows.</p>
                                        <div class="addon-features">
                                            <span class="feature-tag">Movies</span>
                                            <span class="feature-tag">Series</span>
                                            <span class="feature-tag">Multiple Sources</span>
                                            <span class="feature-tag">Direct Links</span>
                                        </div>
                                    </div>
                                    <div class="addon-actions">
                                        <a href="https://aiostreams.elfhosted.com/stremio/configure" target="_blank" rel="noopener" class="btn btn-primary">
                                            <i class="uil uil-external-link-alt"></i>
                                            Configure & Install
                                        </a>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="addons-note">
                                <i class="uil uil-info-circle"></i>
                                <div>
                                    <h4>How to Install Addons:</h4>
                                    <ol>
                                        <li>Click "Configure & Install" on any addon above</li>
                                        <li>Configure the addon settings on the configuration page</li>
                                        <li>Click "Install" to add it to your Stremio profile</li>
                                        <li>The addon will appear in your Stremio addons list</li>
                                    </ol>
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
.configure-section {
    padding: 4rem 0;
    background: var(--bg-color);
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

.configure-layout {
    display: flex;
    justify-content: center;
}

.process-container {
    max-width: 800px;
    width: 100%;
}

.process-list {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
}

.process-step {
    position: relative;
}

.step-header {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 1rem;
}

.step-number {
    width: 2.5rem;
    height: 2.5rem;
    background: var(--primary-color);
    color: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 600;
    font-size: 1.125rem;
    flex-shrink: 0;
}

.step-info {
    flex: 1;
}

.step-title {
    font-size: 1.25rem;
    font-weight: 600;
    color: var(--font-color);
    margin: 0 0 0.25rem 0;
}

.step-subtitle {
    font-size: 0.875rem;
    color: var(--font-secondary);
    margin: 0;
}

.step-icon {
    font-size: 1.5rem;
    color: var(--primary-color);
    background: var(--bg-tertiary-color);
    padding: 0.75rem;
    border-radius: var(--radius-lg);
    flex-shrink: 0;
}

.step-content {
    padding-left: 3.5rem;
}

.w-full {
    width: 100%;
}

.help-text {
    font-size: 0.875rem;
    color: var(--font-secondary);
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.help-text i {
    color: var(--primary-color);
}

.loading-state {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1rem;
    background: var(--bg-tertiary-color);
    border-radius: var(--radius-lg);
}

.loading-spinner {
    width: 1.5rem;
    height: 1.5rem;
    border: 2px solid var(--border-color);
    border-top: 2px solid var(--primary-color);
    border-radius: 50%;
    animation: spin 1s linear infinite;
}

.loading-text {
    color: var(--font-secondary);
    margin: 0;
    font-size: 0.875rem;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

.addons-list {
    max-height: 400px;
    overflow-y: auto;
}

.sortable-list {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
}

.sortable-list .item {
    background: var(--bg-color);
    border: 1px solid var(--border-color);
    border-radius: var(--radius-md);
    padding: 1rem;
    transition: all 0.2s ease;
}

.sortable-list .item:hover {
    box-shadow: var(--shadow-md);
    transform: translateY(-1px);
}

.sortable-list .item.dragging {
    opacity: 0.6;
    transform: rotate(2deg);
}

.ghost {
    opacity: 0.3;
    background: var(--primary-color);
}

/* Backup & Restore Styles */
.backup-actions {
    display: flex;
    gap: 1rem;
    margin-bottom: 1rem;
}

.backup-actions .button {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    padding: 0.75rem 1rem;
    border-radius: var(--radius-md);
    font-size: 0.875rem;
    font-weight: 500;
    text-decoration: none;
    transition: all 0.2s ease;
    border: none;
    cursor: pointer;
}

.button.primary {
    background: var(--primary-color);
    color: white;
}

.button.primary:hover {
    background: var(--primary-hover);
    transform: translateY(-1px);
}

.button.secondary {
    background: var(--bg-tertiary-color);
    color: var(--font-color);
    border: 1px solid var(--border-color);
}

.button.secondary:hover {
    background: var(--bg-color);
    border-color: var(--primary-color);
    transform: translateY(-1px);
}

.backup-info {
    background: rgba(99, 102, 241, 0.05);
    border: 1px solid rgba(99, 102, 241, 0.1);
    border-radius: var(--radius-md);
    padding: 1rem;
}

.backup-info p {
    font-size: 0.875rem;
    color: var(--font-secondary);
    margin: 0;
    display: flex;
    align-items: flex-start;
    gap: 0.5rem;
    line-height: 1.4;
}

.backup-info i {
    color: var(--primary-color);
    margin-top: 0.125rem;
    flex-shrink: 0;
}

/* Popular Addons Section Styles */
.popular-addons-section {
    margin-top: 4rem;
    padding-top: 3rem;
    border-top: 1px solid var(--border-color);
}

.popular-addons-section .section-header {
    margin-bottom: 2rem;
}

.popular-addons-section .section-title {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
    background: linear-gradient(135deg, var(--primary-color), var(--primary-hover));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.popular-addons-section .section-subtitle {
    font-size: 1rem;
    color: var(--font-secondary);
    max-width: 500px;
    margin: 0 auto;
}

.addons-grid {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    max-width: 900px;
    margin: 0 auto;
}

.addon-item {
    display: flex;
    align-items: flex-start;
    gap: 1.5rem;
    padding: 1.5rem;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: var(--radius-lg);
    transition: all 0.3s ease;
}

.addon-item:hover {
    background: rgba(255, 255, 255, 0.08);
    border-color: rgba(255, 255, 255, 0.2);
    transform: translateY(-2px);
}

.addon-info {
    flex: 1;
}

.addon-info h4 {
    font-size: 1.25rem;
    font-weight: 600;
    color: var(--font-color);
    margin: 0 0 0.75rem 0;
}

.addon-description {
    font-size: 0.875rem;
    color: var(--font-secondary);
    line-height: 1.5;
    margin: 0 0 1rem 0;
}

.addon-features {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
}

.feature-tag {
    background: rgba(99, 102, 241, 0.1);
    color: var(--primary-color);
    padding: 0.25rem 0.75rem;
    border-radius: var(--radius-sm);
    font-size: 0.75rem;
    font-weight: 500;
    border: 1px solid rgba(99, 102, 241, 0.2);
}

.addon-actions {
    flex-shrink: 0;
    display: flex;
    align-items: center;
}

.btn {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.75rem 1.5rem;
    border-radius: var(--radius-md);
    font-size: 0.875rem;
    font-weight: 500;
    text-decoration: none;
    transition: all 0.2s ease;
    border: none;
    cursor: pointer;
}

.btn-primary {
    background: var(--primary-color);
    color: white;
}

.btn-primary:hover {
    background: var(--primary-hover);
    transform: translateY(-1px);
}

.btn i {
    font-size: 0.875rem;
}

.addons-note {
    display: flex;
    align-items: flex-start;
    gap: 1rem;
    padding: 1.5rem;
    background: rgba(34, 197, 94, 0.05);
    border: 1px solid rgba(34, 197, 94, 0.1);
    border-radius: var(--radius-lg);
    margin-top: 2rem;
    max-width: 900px;
    margin-left: auto;
    margin-right: auto;
}

.addons-note i {
    color: var(--success-color);
    font-size: 1.5rem;
    margin-top: 0.125rem;
    flex-shrink: 0;
}

.addons-note h4 {
    font-size: 1rem;
    font-weight: 600;
    color: var(--font-color);
    margin: 0 0 0.75rem 0;
}

.addons-note ol {
    margin: 0;
    padding-left: 1.25rem;
}

.addons-note li {
    font-size: 0.875rem;
    color: var(--font-secondary);
    margin-bottom: 0.5rem;
    line-height: 1.4;
}

.addons-note li:last-child {
    margin-bottom: 0;
}

@media (max-width: 768px) {
    .configure-section {
        padding: 2rem 0;
    }
    
    .section-title {
        font-size: 2rem;
    }
    
    .process-container {
        max-width: 100%;
        padding: 0 1rem;
    }
    
    .step-header {
        flex-direction: column;
        text-align: center;
        gap: 0.75rem;
    }
    
    .step-content {
        padding-left: 0;
    }
    
    .loading-state {
        flex-direction: column;
        text-align: center;
        gap: 0.5rem;
    }
    
    .backup-actions {
        flex-direction: column;
    }
    
    .popular-addons-section {
        margin-top: 2rem;
        padding-top: 2rem;
    }
    
    .popular-addons-section .section-title {
        font-size: 1.5rem;
    }
    
    .addon-item {
        flex-direction: column;
        text-align: center;
    }
    
    .addon-actions {
        width: 100%;
        justify-content: center;
    }
    
    .addons-note {
        flex-direction: column;
        text-align: center;
    }
}
</style>
