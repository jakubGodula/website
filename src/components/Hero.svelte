<script>
    import { onMount } from "svelte";

    let visible = false;

    onMount(() => {
        setTimeout(() => {
            visible = true;
        }, 100);
    });
</script>

<section class="hero">
    <div class="hero-background">
        <div class="gradient-orb orb-1"></div>
        <div class="gradient-orb orb-2"></div>
        <div class="gradient-orb orb-3"></div>
    </div>

    <div class="container">
        <div class="hero-content" class:visible>
            <h1 class="hero-title">
                <span class="company-name">Quanturity</span>
                <span class="company-type">sp. z o.o.</span>
            </h1>

            <p class="hero-subtitle">
                Nowoczesne rozwiązania IT dla wymagających firm
            </p>

            <p class="hero-description">
                Tworzymy dedykowane systemy webowe, automatyzujemy procesy
                biznesowe i wdrażamy rozwiązania oparte o sztuczną inteligencję
            </p>

            <a href="#contact" class="cta-button">
                Porozmawiajmy o Twoim projekcie
                <svg
                    class="arrow-icon"
                    width="20"
                    height="20"
                    viewBox="0 0 20 20"
                    fill="none"
                >
                    <path
                        d="M4 10h12m0 0l-4-4m4 4l-4 4"
                        stroke="currentColor"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                    />
                </svg>
            </a>
        </div>
    </div>
</section>

<style>
    .hero {
        position: relative;
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow: hidden;
    }

    .hero-background {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 0;
        overflow: hidden;
    }

    .gradient-orb {
        position: absolute;
        border-radius: 50%;
        filter: blur(80px);
        opacity: 0.3;
        animation: float 8s ease-in-out infinite;
    }

    .orb-1 {
        width: 500px;
        height: 500px;
        background: radial-gradient(circle, #3b82f6 0%, transparent 70%);
        top: -10%;
        left: -10%;
        animation-delay: 0s;
    }

    .orb-2 {
        width: 400px;
        height: 400px;
        background: radial-gradient(circle, #8b5cf6 0%, transparent 70%);
        bottom: -10%;
        right: -5%;
        animation-delay: 2s;
    }

    .orb-3 {
        width: 350px;
        height: 350px;
        background: radial-gradient(circle, #06b6d4 0%, transparent 70%);
        top: 50%;
        right: 20%;
        animation-delay: 4s;
    }

    .hero-content {
        position: relative;
        z-index: 1;
        text-align: center;
        max-width: 900px;
        opacity: 0;
        transform: translateY(30px);
        transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .hero-content.visible {
        opacity: 1;
        transform: translateY(0);
    }

    .hero-title {
        margin-bottom: var(--spacing-lg);
    }

    .company-name {
        display: block;
        font-size: var(--font-size-6xl);
        font-weight: 700;
        letter-spacing: -0.02em;
        background: linear-gradient(135deg, #ffffff 0%, #a0a0a0 100%);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
        margin-bottom: var(--spacing-xs);
    }

    .company-type {
        display: block;
        font-size: var(--font-size-xl);
        font-weight: 300;
        color: var(--color-text-secondary);
        letter-spacing: 0.1em;
    }

    .hero-subtitle {
        font-size: var(--font-size-2xl);
        font-weight: 500;
        color: var(--color-text);
        margin-bottom: var(--spacing-lg);
        line-height: 1.4;
    }

    .hero-description {
        font-size: var(--font-size-lg);
        color: var(--color-text-secondary);
        margin-bottom: var(--spacing-3xl);
        line-height: 1.8;
        max-width: 700px;
        margin-left: auto;
        margin-right: auto;
    }

    .cta-button {
        display: inline-flex;
        align-items: center;
        gap: var(--spacing-sm);
        padding: var(--spacing-md) var(--spacing-xl);
        background: var(--color-accent);
        color: white;
        text-decoration: none;
        border-radius: var(--radius-lg);
        font-weight: 500;
        font-size: var(--font-size-base);
        transition: all var(--transition-base);
        border: 1px solid transparent;
    }

    .cta-button:hover {
        background: var(--color-accent-hover);
        transform: translateY(-2px);
        box-shadow: 0 10px 40px rgba(59, 130, 246, 0.3);
    }

    .arrow-icon {
        transition: transform var(--transition-base);
    }

    .cta-button:hover .arrow-icon {
        transform: translateX(4px);
    }

    @media (max-width: 768px) {
        .hero {
            min-height: 90vh;
        }

        .company-name {
            font-size: var(--font-size-5xl);
        }

        .hero-subtitle {
            font-size: var(--font-size-xl);
        }

        .hero-description {
            font-size: var(--font-size-base);
        }

        .gradient-orb {
            filter: blur(60px);
        }
    }
</style>
