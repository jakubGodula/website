<script>
    import { onMount } from "svelte";

    let visible = false;

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

        const section = document.querySelector(".contact");
        if (section) {
            observer.observe(section);
        }

        return () => observer.disconnect();
    });
</script>

<section class="contact section" id="contact">
    <div class="container">
        <div class="contact-content" class:visible>
            <div class="contact-info">
                <h2 class="contact-title">Rozpocznijmy współpracę</h2>
                <p class="contact-description">
                    Jesteśmy gotowi pomóc w realizacji Twojego projektu.
                    Skontaktuj się z nami, aby omówić szczegóły.
                </p>

                <div class="info-items">
                    <div class="info-item">
                        <div class="info-icon">📧</div>
                        <div class="info-content">
                            <div class="info-label">Email</div>
                            <a
                                href="mailto:kontakt@quanturity.pl"
                                class="info-value">quanturity@proton.me</a
                            >
                        </div>
                    </div>

                    <div class="info-item">
                        <div class="info-icon">🏢</div>
                        <div class="info-content">
                            <div class="info-label">Firma</div>
                            <div class="info-value">Quanturity sp. z o.o.</div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="contact-cta">
                <div class="cta-card">
                    <h3 class="cta-title">Masz projekt w głowie?</h3>
                    <p class="cta-text">
                        Opowiedz nam o swoich potrzebach, a my zaproponujemy
                        najlepsze rozwiązanie dopasowane do Twojego biznesu.
                    </p>
                    <a href="mailto:kontakt@quanturity.pl" class="cta-button">
                        Wyślij wiadomość
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
        </div>
    </div>

    <footer class="footer">
        <div class="container">
            <div class="footer-content">
                <p class="footer-text">
                    © 2025 Quanturity sp. z o.o. Wszelkie prawa zastrzeżone.
                </p>
            </div>
        </div>
    </footer>
</section>

<style>
    .contact {
        background: var(--color-bg);
        position: relative;
        padding-bottom: 0;
    }

    .contact::before {
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

    .contact-content {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: var(--spacing-4xl);
        align-items: center;
        opacity: 0;
        transform: translateY(20px);
        transition: all 0.6s ease;
    }

    .contact-content.visible {
        opacity: 1;
        transform: translateY(0);
    }

    .contact-title {
        font-size: var(--font-size-4xl);
        font-weight: 700;
        margin-bottom: var(--spacing-lg);
        background: linear-gradient(135deg, #ffffff 0%, #a0a0a0 100%);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
    }

    .contact-description {
        font-size: var(--font-size-lg);
        color: var(--color-text-secondary);
        line-height: 1.7;
        margin-bottom: var(--spacing-3xl);
    }

    .info-items {
        display: flex;
        flex-direction: column;
        gap: var(--spacing-xl);
    }

    .info-item {
        display: flex;
        align-items: flex-start;
        gap: var(--spacing-lg);
    }

    .info-icon {
        font-size: 2rem;
        flex-shrink: 0;
    }

    .info-content {
        flex: 1;
    }

    .info-label {
        font-size: var(--font-size-sm);
        color: var(--color-text-secondary);
        margin-bottom: var(--spacing-xs);
        text-transform: uppercase;
        letter-spacing: 0.05em;
    }

    .info-value {
        font-size: var(--font-size-lg);
        color: var(--color-text);
        text-decoration: none;
        transition: color var(--transition-base);
    }

    a.info-value:hover {
        color: var(--color-accent);
    }

    .cta-card {
        background: var(--color-surface);
        border: 1px solid var(--color-border);
        border-radius: var(--radius-xl);
        padding: var(--spacing-3xl);
        transition: all var(--transition-base);
    }

    .cta-card:hover {
        border-color: var(--color-accent);
        box-shadow: 0 20px 60px rgba(59, 130, 246, 0.15);
    }

    .cta-title {
        font-size: var(--font-size-2xl);
        font-weight: 600;
        margin-bottom: var(--spacing-md);
        color: var(--color-text);
    }

    .cta-text {
        font-size: var(--font-size-base);
        color: var(--color-text-secondary);
        line-height: 1.7;
        margin-bottom: var(--spacing-2xl);
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

    .footer {
        margin-top: var(--spacing-4xl);
        padding: var(--spacing-2xl) 0;
        border-top: 1px solid var(--color-border);
    }

    .footer-content {
        text-align: center;
    }

    .footer-text {
        font-size: var(--font-size-sm);
        color: var(--color-text-secondary);
    }

    @media (max-width: 768px) {
        .contact-content {
            grid-template-columns: 1fr;
            gap: var(--spacing-2xl);
        }

        .contact-title {
            font-size: var(--font-size-3xl);
        }

        .cta-card {
            padding: var(--spacing-2xl);
        }
    }
</style>
