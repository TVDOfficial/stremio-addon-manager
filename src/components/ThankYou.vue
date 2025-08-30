<template>
    <section id="thanks" class="thanks-section">
        <div class="container">
            <div class="thanks-card card text-center">
                <div class="thanks-icon">
                    <i class="uil uil-heart"></i>
                </div>
                <h3 class="thanks-title">Thank You</h3>
                <p class="thanks-text">
                    Big thank you to <code class="code-highlight">Sleeyax</code> and <code class="code-highlight">&#60;Code/&#62;</code> 
                    for the conversations and code snippets that made this really easy to implement.
                </p>
            </div>
        </div>
    </section>
</template>

<style scoped>
.thanks-section {
    padding: 4rem 0;
    background: var(--bg-secondary-color);
}

.thanks-card {
    max-width: 600px;
    margin: 0 auto;
    text-align: center;
    background: linear-gradient(135deg, var(--bg-secondary-color) 0%, var(--bg-tertiary-color) 100%);
    border: none;
    box-shadow: var(--shadow-xl);
}

.thanks-icon {
    width: 80px;
    height: 80px;
    margin: 0 auto 2rem auto;
    background: linear-gradient(135deg, var(--primary-color), var(--primary-hover));
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: var(--shadow-lg);
}

.thanks-icon i {
    font-size: 2rem;
    color: white;
}

.thanks-title {
    font-size: 2rem;
    font-weight: 700;
    color: var(--font-color);
    margin: 0 0 1rem 0;
}

.thanks-text {
    font-size: 1.125rem;
    color: var(--font-secondary);
    line-height: 1.6;
    margin: 0;
}

.code-highlight {
    background: var(--bg-tertiary-color);
    color: var(--primary-color);
    padding: 0.25rem 0.5rem;
    border-radius: var(--radius-sm);
    font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', monospace;
    font-size: 0.875rem;
    font-weight: 600;
}

@media (max-width: 768px) {
    .thanks-section {
        padding: 2rem 0;
    }
    
    .thanks-icon {
        width: 60px;
        height: 60px;
        margin-bottom: 1.5rem;
    }
    
    .thanks-icon i {
        font-size: 1.5rem;
    }
    
    .thanks-title {
        font-size: 1.75rem;
    }
    
    .thanks-text {
        font-size: 1rem;
    }
}
</style>
