<script setup>
import { ref } from 'vue'
import draggable from 'vuedraggable'
import AddonItem from './AddonItem.vue'
import Authentication from './Authentication.vue'
import StremioPreview from './StremioPreview.vue'

const stremioAPIBase = "https://api.strem.io/api/"
const dragging = false
let stremioAuthKey = ref('');
let addons = ref([])
let loadAddonsButtonText = ref('Load Addons')
let showPreview = ref(false)

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
            showPreview.value = true // Auto-show preview when addons are loaded
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
}

function togglePreview() {
    showPreview.value = !showPreview.value
}
</script>

<template>
    <section id="configure" class="configure-section">
        <div class="container">
            <div class="section-header text-center mb-5">
                <h2 class="section-title">Configure Your Addons</h2>
                <p class="section-subtitle">Manage and organize your Stremio addons with ease</p>
            </div>

            <div class="configure-grid">
                <!-- Authentication Card -->
                <div class="configure-card card">
                    <div class="card-header">
                        <div class="card-header-content">
                            <i class="uil uil-shield-check card-icon"></i>
                            <div>
                                <h3 class="card-title">Authentication</h3>
                                <p class="card-subtitle">Connect your Stremio account</p>
                            </div>
                        </div>
                    </div>
                    <div class="card-body">
                        <Authentication :stremioAPIBase="stremioAPIBase" @auth-key="setAuthKey" />
                    </div>
                </div>

                <!-- Load Addons Card -->
                <div class="configure-card card">
                    <div class="card-header">
                        <div class="card-header-content">
                            <i class="uil uil-download-alt card-icon"></i>
                            <div>
                                <h3 class="card-title">Step 1: Load Addons</h3>
                                <p class="card-subtitle">Fetch your current addon collection</p>
                            </div>
                        </div>
                    </div>
                    <div class="card-body">
                        <button class="button primary w-full" @click="loadUserAddons" :disabled="!stremioAuthKey">
                            <i class="uil uil-cloud-download"></i>
                            {{ loadAddonsButtonText }}
                        </button>
                        <p class="help-text mt-2">
                            <i class="uil uil-info-circle"></i>
                            Make sure you've authenticated first
                        </p>
                    </div>
                </div>

                <!-- Reorder Addons Card -->
                <div class="configure-card card" v-if="addons.length > 0">
                    <div class="card-header">
                        <div class="card-header-content">
                            <i class="uil uil-sort-amount-down card-icon"></i>
                            <div>
                                <h3 class="card-title">Step 2: Reorder Addons</h3>
                                <p class="card-subtitle">Drag and drop to change priority</p>
                            </div>
                        </div>
                    </div>
                    <div class="card-body">
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

                <!-- Sync Addons Card -->
                <div class="configure-card card" v-if="addons.length > 0">
                    <div class="card-header">
                        <div class="card-header-content">
                            <i class="uil uil-sync card-icon"></i>
                            <div>
                                <h3 class="card-title">Step 3: Sync Changes</h3>
                                <p class="card-subtitle">Apply your changes to Stremio</p>
                            </div>
                        </div>
                    </div>
                    <div class="card-body">
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

            <!-- Preview Toggle -->
            <div class="preview-toggle-section" v-if="addons.length > 0">
                <div class="preview-toggle-card card">
                    <div class="preview-toggle-content">
                        <div class="preview-toggle-info">
                            <i class="uil uil-eye"></i>
                            <div>
                                <h4>Preview Your Changes</h4>
                                <p>See how your Stremio home page will look after reordering</p>
                            </div>
                        </div>
                        <button 
                            class="button primary" 
                            @click="togglePreview"
                            :class="{ 'active': showPreview }"
                        >
                            <i :class="showPreview ? 'uil uil-eye-slash' : 'uil uil-eye'"></i>
                            {{ showPreview ? 'Hide Preview' : 'Show Preview' }}
                        </button>
                    </div>
                </div>
            </div>

            <!-- Stremio Preview -->
            <StremioPreview 
                :addons="addons" 
                :isVisible="showPreview && addons.length > 0"
            />
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

.configure-grid {
    display: grid;
    gap: 2rem;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    margin-bottom: 3rem;
}

.configure-card {
    height: fit-content;
}

.card-header-content {
    display: flex;
    align-items: center;
    gap: 1rem;
}

.card-icon {
    font-size: 1.5rem;
    color: var(--primary-color);
    background: var(--bg-tertiary-color);
    padding: 0.75rem;
    border-radius: var(--radius-lg);
}

.card-body {
    padding-top: 1rem;
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

.preview-toggle-section {
    margin-bottom: 2rem;
}

.preview-toggle-card {
    max-width: 600px;
    margin: 0 auto;
}

.preview-toggle-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
}

.preview-toggle-info {
    display: flex;
    align-items: center;
    gap: 1rem;
    flex: 1;
}

.preview-toggle-info i {
    font-size: 1.5rem;
    color: var(--primary-color);
}

.preview-toggle-info h4 {
    font-size: 1.125rem;
    font-weight: 600;
    color: var(--font-color);
    margin: 0 0 0.25rem 0;
}

.preview-toggle-info p {
    font-size: 0.875rem;
    color: var(--font-secondary);
    margin: 0;
}

.button.active {
    background: var(--success-color);
    border-color: var(--success-color);
}

@media (max-width: 768px) {
    .configure-section {
        padding: 2rem 0;
    }
    
    .section-title {
        font-size: 2rem;
    }
    
    .configure-grid {
        grid-template-columns: 1fr;
        margin-bottom: 2rem;
    }
    
    .card-header-content {
        flex-direction: column;
        text-align: center;
        gap: 0.75rem;
    }
    
    .preview-toggle-content {
        flex-direction: column;
        text-align: center;
    }
    
    .preview-toggle-info {
        flex-direction: column;
        text-align: center;
    }
}
</style>
