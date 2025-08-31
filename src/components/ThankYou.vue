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
                <div class="github-links">
                    <p class="github-text">Special thanks to our contributors:</p>
                    <div class="contributor-links">
                        <a href="https://github.com/TVDOfficial" target="_blank" rel="noopener" class="contributor-link">
                            <i class="uil uil-github"></i>
                            <span>TVDOfficial</span>
                        </a>
                        <a href="https://github.com/sleeyax" target="_blank" rel="noopener" class="contributor-link">
                            <i class="uil uil-github"></i>
                            <span>sleeyax</span>
                        </a>
                    </div>
                </div>
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

.github-links {
    margin-top: 2rem;
    padding-top: 2rem;
    border-top: 1px solid var(--border-color);
}

.github-text {
    font-size: 1rem;
    color: var(--font-secondary);
    margin: 0 0 1rem 0;
}

.contributor-links {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}

.contributor-link {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.75rem 1.25rem;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: var(--radius-lg);
    text-decoration: none;
    color: var(--font-color);
    font-size: 0.875rem;
    font-weight: 500;
    transition: all 0.3s ease;
}

.contributor-link:hover {
    background: rgba(255, 255, 255, 0.1);
    border-color: var(--primary-color);
    transform: translateY(-2px);
    box-shadow: var(--shadow-md);
}

.contributor-link i {
    font-size: 1.25rem;
    color: var(--primary-color);
}

.contributor-link span {
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
    
    .github-links {
        margin-top: 1.5rem;
        padding-top: 1.5rem;
    }
    
    .contributor-links {
        flex-direction: column;
        gap: 1rem;
    }
    
    .contributor-link {
        justify-content: center;
        padding: 1rem 1.5rem;
    }
}
</style>
