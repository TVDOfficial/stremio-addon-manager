<script setup>
import { ref } from 'vue'

const props = defineProps({
    stremioAPIBase: {
        type: String,
        required: true
    },
})

const authKey = ref('')
const email = ref('')
const password = ref('')
const loginButtonText = ref('Login')
const isLoading = ref(false)
const emits = defineEmits(['auth-key'])

async function loginUserPassword() {
    if (!email.value || !password.value) {
        alert('Please enter both email and password')
        return
    }
    
    isLoading.value = true
    loginButtonText.value = 'Logging in...'
    
    try {
        const response = await fetch(`${props.stremioAPIBase}login`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                authKey: null,
                email: email.value,
                password: password.value,
            })
        })
        
        const data = await response.json()
        console.log("Auth data:", data)
        
        if (data.result && data.result.authKey) {
            authKey.value = data.result.authKey
            loginButtonText.value = 'Success!'
            emitAuthKey()
        } else {
            throw new Error('Login failed - invalid response')
        }
    } catch (err) {
        console.error(err);
        alert('Login failed: ' + err.message);
        loginButtonText.value = 'Login'
    } finally {
        isLoading.value = false
    }
}

function emitAuthKey() {
    emits('auth-key', authKey.value.replaceAll('"', '').trim())
}
</script>

<template>
    <div class="auth-container">
        <!-- Login Form -->
        <div class="auth-section">
            <h4 class="auth-title">
                <i class="uil uil-user-circle"></i>
                Login with Email
            </h4>
            <div class="auth-form">
                <div class="form-group">
                    <label for="email">Email Address</label>
                    <input 
                        id="email"
                        type="email" 
                        v-model="email" 
                        placeholder="Enter your Stremio email"
                        :disabled="isLoading"
                    >
                </div>
                
                <div class="form-group">
                    <label for="password">Password</label>
                    <input 
                        id="password"
                        type="password" 
                        v-model="password" 
                        placeholder="Enter your Stremio password"
                        :disabled="isLoading"
                    >
                </div>
                
                <button 
                    class="button primary w-full" 
                    @click="loginUserPassword"
                    :disabled="isLoading || !email || !password"
                >
                    <i class="uil uil-signin" v-if="!isLoading"></i>
                    <i class="uil uil-spinner" v-else></i>
                    {{ loginButtonText }}
                </button>
            </div>
        </div>

        <!-- Divider -->
        <div class="auth-divider">
            <span class="divider-text">OR</span>
        </div>

        <!-- Auth Key Input -->
        <div class="auth-section">
            <h4 class="auth-title">
                <i class="uil uil-key-skeleton"></i>
                Use Auth Key
            </h4>
            <div class="auth-form">
                <div class="form-group">
                    <label for="authKey">Stremio Auth Key</label>
                    <input 
                        id="authKey"
                        type="password" 
                        v-model="authKey" 
                        @input="emitAuthKey"
                        placeholder="Paste your Stremio AuthKey here..."
                        :disabled="isLoading"
                    >
                </div>
                
                <p class="help-text">
                    <i class="uil uil-info-circle"></i>
                    You can find your AuthKey in Stremio settings
                </p>
            </div>
        </div>
    </div>
</template>

<style scoped>
.auth-container {
    display: flex;
    flex-direction: column;
    gap: 2rem;
}

.auth-section {
    background: var(--bg-color);
    border: 1px solid var(--border-color);
    border-radius: var(--radius-lg);
    padding: 1.5rem;
}

.auth-title {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    font-size: 1.125rem;
    font-weight: 600;
    color: var(--font-color);
    margin: 0 0 1.5rem 0;
}

.auth-title i {
    color: var(--primary-color);
    font-size: 1.25rem;
}

.auth-form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.form-group label {
    font-size: 0.875rem;
    font-weight: 500;
    color: var(--font-color);
}

.form-group input {
    padding: 0.75rem 1rem;
    border: 1px solid var(--border-color);
    border-radius: var(--radius-md);
    background: var(--bg-color);
    color: var(--font-color);
    font-size: 0.875rem;
    transition: all 0.2s ease;
}

.form-group input:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgb(99 102 241 / 0.1);
}

.form-group input:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

.auth-divider {
    position: relative;
    text-align: center;
    margin: 1rem 0;
}

.auth-divider::before {
    content: '';
    position: absolute;
    top: 50%;
    left: 0;
    right: 0;
    height: 1px;
    background: var(--border-color);
}

.divider-text {
    background: var(--bg-color);
    padding: 0 1rem;
    color: var(--font-secondary);
    font-size: 0.875rem;
    font-weight: 500;
    position: relative;
    z-index: 1;
}

.help-text {
    font-size: 0.875rem;
    color: var(--font-secondary);
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin: 0;
}

.help-text i {
    color: var(--primary-color);
}

.w-full {
    width: 100%;
}

/* Loading animation */
@keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

.uil-spinner {
    animation: spin 1s linear infinite;
}

/* Responsive design */
@media (max-width: 768px) {
    .auth-section {
        padding: 1rem;
    }
    
    .auth-title {
        font-size: 1rem;
    }
}
</style>
