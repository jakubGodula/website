<script>
    import { onMount } from "svelte";

    let visible = false;

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
    ];

    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting) {
                        visible = true;
                    }
                });
            },
            { threshold: 0.1 },
        );

        const section = document.querySelector(".services");
        if (section) {
            observer.observe(section);
        }

        return () => observer.disconnect();
    });
</script>

<section class="services section" id="services">
    <div class="container">
        <div class="section-header" class:visible>
            <h2 class="section-title">Nasze Usługi</h2>
            <p class="section-subtitle">
                Kompleksowe rozwiązania IT wspierające rozwój Twojej firmy
            </p>
        </div>

        <div class="services-grid" class:visible>
            {#each services as service, index}
                <div
                    class="service-card"
                    style="animation-delay: {index * 0.1}s"
                >
                    <div class="service-icon">{service.icon}</div>
                    <h3 class="service-title">{service.title}</h3>
                    <p class="service-description">{service.description}</p>
                </div>
            {/each}
        </div>
    </div>
</section>

<style>
    .services {
        background: var(--color-bg-secondary);
        position: relative;
    }

    .services::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: 1px;
        background: linear-gradient(
            90deg,
            transparent,
            var(--color-border),
            transparent
        );
    }

    .section-header {
        text-align: center;
        margin-bottom: var(--spacing-4xl);
        opacity: 0;
        transform: translateY(20px);
        transition: all 0.6s ease;
    }

    .section-header.visible {
        opacity: 1;
        transform: translateY(0);
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
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
        gap: var(--spacing-xl);
    }

    .service-card {
        background: var(--color-surface);
        border: 1px solid var(--color-border);
        border-radius: var(--radius-xl);
        padding: var(--spacing-2xl);
        transition: all var(--transition-base);
        opacity: 0;
        transform: translateY(20px);
    }

    .services-grid.visible .service-card {
        animation: fadeInUp 0.6s ease forwards;
    }

    .service-card:hover {
        transform: translateY(-8px);
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
