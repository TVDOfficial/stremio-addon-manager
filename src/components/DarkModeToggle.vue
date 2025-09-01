<script setup>
import { ref, onMounted } from 'vue'

let darkEnabled = ref(getDarkModePreference())

function getDarkModePreference() {
    const userSet = localStorage.getItem('darkMode')
    // User explicit setting takes precedence
    if (userSet !== null) {
        return userSet === 'true'
    } else {
        // If user has no preference, default to dark mode
        return true
    }
}

function toggleMode() {
    darkEnabled.value = !darkEnabled.value
    localStorage.setItem('darkMode', darkEnabled.value)
    document.body.classList.toggle('dark')
}

onMounted(() => {
    if (darkEnabled.value) {
        document.body.classList.add('dark')
    }
})
</script>

<template>
    <div class="theme-toggle">
        <button @click="toggleMode" class="theme-toggle-btn" :title="darkEnabled ? 'Switch to light mode' : 'Switch to dark mode'">
            <i v-if="darkEnabled" class="uil uil-sun"></i>
            <i v-else class="uil uil-moon"></i>
        </button>
    </div>
</template>

<style scoped>
.theme-toggle {
    position: fixed;
    top: 2rem;
    right: 2rem;
    z-index: 1000;
}

.theme-toggle-btn {
    width: 3rem;
    height: 3rem;
    border: none;
    border-radius: 50%;
    background: var(--bg-secondary-color);
    color: var(--font-color);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: var(--shadow-lg);
    transition: all 0.3s ease;
    border: 1px solid var(--border-color);
}

.theme-toggle-btn:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow-xl);
    background: var(--primary-color);
    color: white;
    border-color: var(--primary-color);
}

.theme-toggle-btn i {
    font-size: 1.25rem;
}

@media (max-width: 768px) {
    .theme-toggle {
        top: 1rem;
        right: 1rem;
    }
    
    .theme-toggle-btn {
        width: 2.5rem;
        height: 2.5rem;
    }
    
    .theme-toggle-btn i {
        font-size: 1rem;
    }
}
</style>
