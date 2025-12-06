<script>
    import { onMount } from "svelte";

    let visible = false;

    onMount(() => {
        setTimeout(() => {
            visible = true;
        }, 100);
    });
</script>

<script>
    import logo from "../imgs/logo_long.png";
</script>

<section class="hero">
    <div class="container">
        <div class="hero-content" class:visible>
            <h1 class="hero-title">
                <img src={logo} alt="Quanturity" />
            </h1>

            <p class="hero-subtitle">
                Nowoczesne rozwiązania IT dla wymagających firm
            </p>

            <p class="hero-description">
                Tworzymy dedykowane systemy informatyczne, automatyzujemy
                procesy biznesowe i wdrażamy rozwiązania oparte o sztuczną
                inteligencję
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

    .company-logo {
        max-width: 100%;
        width: 600px;
        height: auto;
        margin-bottom: var(--spacing-sm);
        filter: brightness(0) invert(1);
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

        .company-logo {
            width: 300px;
        }

        .hero-subtitle {
            font-size: var(--font-size-xl);
        }

        .hero-description {
            font-size: var(--font-size-base);
        }
    }
</style>
