<template>
    <section id="faq" class="faq-section">
        <div class="container">
            <div class="section-header text-center mb-5">
                <h2 class="section-title">Frequently Asked Questions</h2>
                <p class="section-subtitle">Everything you need to know about using this tool safely</p>
            </div>

            <div class="faq-grid">
                <div class="faq-card card">
                    <details class="faq-item">
                        <summary class="faq-question">
                            <i class="uil uil-exclamation-triangle"></i>
                            What risks are involved?
                        </summary>
                        <div class="faq-answer">
                            <p>
                                This was whipped together in a couple of hours. It is not well tested and may break your Stremio
                                profile. Stremio functionality relies on the existence of certain addons (ie, Cinemeta). It is
                                possible that the order of addons is also important to some functionality.
                            </p>
                            <p>
                                There is currently no way to 'reset' your addons to previous configurations or default
                                configurations.
                            </p>
                        </div>
                    </details>
                </div>

                <div class="faq-card card">
                    <details class="faq-item">
                        <summary class="faq-question">
                            <i class="uil uil-shield-check"></i>
                            Are my credentials safe?
                        </summary>
                        <div class="faq-answer">
                            <p>
                                Yes. We only use your credentials to authenticate with the Stremio API. We do not store them in any way; as soon as you refresh the page they are gone.
                            </p>
                            <p>
                                If you're still in doubt, we highly encourage you to go read the source code. You'll see there's no hidden funny business going on.
                            </p>
                        </div>
                    </details>
                </div>

                <div class="faq-card card">
                    <details class="faq-item">
                        <summary class="faq-question">
                            <i class="uil uil-browser"></i>
                            What is the developer console and how do I open it?
                        </summary>
                        <div class="faq-answer">
                            <p>
                                The browser developer console is a tool which logs the information associated with a web application, such
                                as network requests and errors. It also allows you to interact with the loaded web page using JavaScript.
                                Most modern browsers have a developer console built in.
                            </p>
                            <p>
                                Use <a href="https://balsamiq.com/support/faqs/browserconsole/" target="_blank" class="link">this guide</a> to open your
                                browsers developer console, ensuring have the Stremio web app open.
                            </p>
                        </div>
                    </details>
                </div>

                <div class="faq-card card">
                    <details class="faq-item">
                        <summary class="faq-question">
                            <i class="uil uil-arrows-h"></i>
                            Can I use this to move Cinemeta catalogs from the top?
                        </summary>
                        <div class="faq-answer">
                            <p>
                                Yes! This will allow you to move the Cinemeta provided catalogs (ie, Popular - Series/Movie and Featured -
                                Series/Movie) from the top of your catalog list.
                            </p>
                            <p>
                                Do note that the in-built 'Continue watching' catalog cannot be moved from the top.
                            </p>
                        </div>
                    </details>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
.faq-section {
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

.faq-grid {
    display: grid;
    gap: 1.5rem;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
}

.faq-card {
    border: 1px solid var(--border-color);
    transition: all 0.3s ease;
}

.faq-card:hover {
    box-shadow: var(--shadow-lg);
    transform: translateY(-2px);
}

.faq-item {
    border: none;
    background: none;
}

.faq-question {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1.5rem;
    cursor: pointer;
    font-size: 1.125rem;
    font-weight: 600;
    color: var(--font-color);
    border: none;
    background: none;
    width: 100%;
    text-align: left;
    transition: all 0.2s ease;
    border-radius: var(--radius-lg);
}

.faq-question:hover {
    background: var(--bg-tertiary-color);
}

.faq-question i {
    color: var(--primary-color);
    font-size: 1.25rem;
    flex-shrink: 0;
}

.faq-question::marker {
    display: none;
}

.faq-question::after {
    content: '\f107';
    font-family: 'Unicons';
    font-size: 1.25rem;
    color: var(--font-secondary);
    margin-left: auto;
    transition: transform 0.2s ease;
}

.faq-item[open] .faq-question::after {
    transform: rotate(180deg);
}

.faq-answer {
    padding: 0 1.5rem 1.5rem 1.5rem;
    color: var(--font-secondary);
    line-height: 1.6;
}

.faq-answer p {
    margin-bottom: 1rem;
}

.faq-answer p:last-child {
    margin-bottom: 0;
}

.link {
    color: var(--primary-color);
    text-decoration: none;
    font-weight: 500;
    transition: color 0.2s ease;
}

.link:hover {
    color: var(--primary-hover);
    text-decoration: underline;
}

@media (max-width: 768px) {
    .faq-section {
        padding: 2rem 0;
    }
    
    .section-title {
        font-size: 2rem;
    }
    
    .faq-grid {
        grid-template-columns: 1fr;
    }
    
    .faq-question {
        font-size: 1rem;
        padding: 1rem;
    }
    
    .faq-answer {
        padding: 0 1rem 1rem 1rem;
    }
}
</style>
