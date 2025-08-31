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
}
</style>
