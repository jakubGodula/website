<script>
    import { onMount } from "svelte";

    const services = [
        {
            title: "Systemy Webowe",
            description:
                "Dedykowane systemy i aplikacje webowe dostosowane do specyfiki Twojego biznesu",
            icon: "🌐",
        },
        {
            title: "Integracja i Automatyzacja",
            description:
                "Integracja systemów i automatyzacja procesów biznesowych dla zwiększenia efektywności",
            icon: "⚡",
        },
        {
            title: "Architektura Chmurowa",
            description:
                "Nowoczesne architektury IT oparte o rozwiązania chmurowe zapewniające skalowalność",
            icon: "☁️",
        },
        {
            title: "Systemy CRM/ERP",
            description:
                "Systemy CRM i ERP tworzone na miarę potrzeb Twojej organizacji",
            icon: "📊",
        },
        {
            title: "AI i Analiza Danych",
            description:
                "Rozwiązania wykorzystujące sztuczną inteligencję i zaawansowaną analizę danych",
            icon: "🤖",
        },
        {
            title: "Cyberbezpieczeństwo",
            description:
                "Doradztwo w zakresie cyberbezpieczeństwa i ochrony danych",
            icon: "🔒",
        },
        {
            title: "Web3",
            description:
                "Tworzenie zdecentralizowanych aplikacji, smart kontraktów i rozwiązań blockchain",
            icon: "🔗",
        },
        {
            title: "Sieci",
            description:
                "Projektowanie, wdrażanie i zabezpieczanie infrastruktury sieciowej dla firm",
            icon: "📡",
        },
        {
            title: "Szkolenia",
            description:
                "Warsztaty i szkolenia z zakresu cyberbezpieczeństwa, programowania i nowych technologii",
            icon: "🎓",
        },
    ];

    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    const ratio = entry.intersectionRatio;
                    const y = entry.boundingClientRect.y;
                    const isVisible =
                        entry.target.classList.contains("visible");

                    if (isVisible) {
                        // Leaving bottom (scrolling up) -> Early exit requested
                        if (y > 0 && ratio < 0.9) {
                            entry.target.classList.remove("visible");
                        }
                        // Leaving top (scrolling down) -> Standard exit
                        else if (y < 0 && ratio < 0.1) {
                            entry.target.classList.remove("visible");
                        }
                    } else {
                        // Entering -> Standard entry
                        if (ratio > 0.1) {
                            entry.target.classList.add("visible");
                        }
                    }
                });
            },
            { threshold: [0.1, 0.9] },
        );

        const elements = document.querySelectorAll(
            ".section-header, .grids-wrapper",
        );
        elements.forEach((el) => observer.observe(el));

        return () => observer.disconnect();
    });
</script>

<section class="services section" id="services">
    <div class="container">
        <div class="section-header">
            <h2 class="section-title">Nasze Usługi</h2>
            <p class="section-subtitle">
                Kompleksowe rozwiązania IT wspierające rozwój Twojej firmy
            </p>
        </div>
    </div>

    <div class="grids-wrapper">
        <div class="services-grid">
            {#each services.slice(0, 3) as service, index}
                <div class="service-wrapper slide-left">
                    <div class="service-card">
                        <div class="service-icon">{service.icon}</div>
                        <h3 class="service-title">{service.title}</h3>
                        <p class="service-description">{service.description}</p>
                    </div>
                </div>
            {/each}
        </div>

        <div class="services-grid" style="margin-top: var(--spacing-xl);">
            {#each services.slice(3, 6) as service, index}
                <div class="service-wrapper slide-right">
                    <div class="service-card">
                        <div class="service-icon">{service.icon}</div>
                        <h3 class="service-title">{service.title}</h3>
                        <p class="service-description">{service.description}</p>
                    </div>
                </div>
            {/each}
        </div>

        <div class="services-grid" style="margin-top: var(--spacing-xl);">
            {#each services.slice(6, 9) as service, index}
                <div class="service-wrapper slide-left">
                    <div class="service-card">
                        <div class="service-icon">{service.icon}</div>
                        <h3 class="service-title">{service.title}</h3>
                        <p class="service-description">{service.description}</p>
                    </div>
                </div>
            {/each}
        </div>
    </div>
</section>

<style>
    .services {
        background: transparent;
        position: relative;
        overflow: hidden;
    }

    .section-header {
        text-align: center;
        margin-bottom: var(--spacing-4xl);
        opacity: 0;
        transform: translateY(20px);
        transition: all 0.6s ease;
    }

    :global(.section-header.visible) {
        opacity: 1;
        transform: translateY(0);
    }

    :global(.grids-wrapper.visible) .service-wrapper {
        opacity: 1;
        transform: translateX(0);
    }

    .section-title {
        font-size: var(--font-size-4xl);
        font-weight: 700;
        margin-bottom: var(--spacing-md);
        background: linear-gradient(135deg, #ffffff 0%, #a0a0a0 100%);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
    }

    .section-subtitle {
        font-size: var(--font-size-lg);
        color: var(--color-text-secondary);
        max-width: 600px;
        margin: 0 auto;
    }

    .services-grid {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: var(--spacing-xl);
        padding: 0 var(--spacing-xl);
    }

    .service-wrapper {
        width: 100%;
        max-width: 400px;
        aspect-ratio: 1;
        opacity: 0;
        transition:
            transform 2.5s cubic-bezier(0.4, 0, 0.2, 1),
            opacity 2.5s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .service-wrapper.slide-left {
        transform: translateX(-200%);
    }

    .service-wrapper.slide-right {
        transform: translateX(200%);
    }

    .service-card {
        width: 100%;
        height: 100%;
        background: var(--color-surface);
        border: 1px solid var(--color-border);
        border-radius: var(--radius-xl);
        padding: var(--spacing-2xl);
        transition: all 0.3s ease;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
    }

    .service-card:hover {
        transform: translateX(0) translateY(-8px);
        border-color: var(--color-accent);
        background: var(--color-surface-hover);
        box-shadow: 0 20px 60px rgba(59, 130, 246, 0.15);
    }

    .service-icon {
        font-size: 3rem;
        margin-bottom: var(--spacing-lg);
        display: inline-block;
        transition: transform var(--transition-base);
    }

    .service-card:hover .service-icon {
        transform: scale(1.1) rotate(5deg);
    }

    .service-title {
        font-size: var(--font-size-xl);
        font-weight: 600;
        margin-bottom: var(--spacing-md);
        color: var(--color-text);
    }

    .service-description {
        font-size: var(--font-size-base);
        color: var(--color-text-secondary);
        line-height: 1.7;
    }

    @media (max-width: 768px) {
        .services-grid {
            grid-template-columns: 1fr;
            gap: var(--spacing-lg);
        }

        .section-title {
            font-size: var(--font-size-3xl);
        }
    }
</style>
