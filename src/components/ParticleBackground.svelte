<script>
    import { onMount } from "svelte";

    let canvas;
    let ctx;
    let particles = [];
    let mouse = { x: null, y: null, radius: 150 };
    let animationId;

    const particleCount = 100;

    class Particle {
        constructor(x, y) {
            this.x = x;
            this.y = y;
            this.baseX = x;
            this.baseY = y;
            this.size = Math.random() * 3 + 1;
            this.density = Math.random() * 30 + 1;
            this.speedX = Math.random() * 0.5 - 0.25;
            this.speedY = Math.random() * 0.5 - 0.25;
        }

        update() {
            // Calculate distance from mouse
            const dx = mouse.x - this.x;
            const dy = mouse.y - this.y;
            const distance = Math.sqrt(dx * dx + dy * dy);
            const forceDirectionX = dx / distance;
            const forceDirectionY = dy / distance;
            const maxDistance = mouse.radius;
            const force = (maxDistance - distance) / maxDistance;
            const directionX = forceDirectionX * force * this.density;
            const directionY = forceDirectionY * force * this.density;

            if (distance < mouse.radius) {
                this.x -= directionX;
                this.y -= directionY;
            } else {
                // Return to base position
                if (this.x !== this.baseX) {
                    const dx = this.x - this.baseX;
                    this.x -= dx / 10;
                }
                if (this.y !== this.baseY) {
                    const dy = this.y - this.baseY;
                    this.y -= dy / 10;
                }
            }

            // Gentle floating animation
            this.baseX += this.speedX;
            this.baseY += this.speedY;

            // Wrap around edges
            if (this.baseX < 0) this.baseX = canvas.width;
            if (this.baseX > canvas.width) this.baseX = 0;
            if (this.baseY < 0) this.baseY = canvas.height;
            if (this.baseY > canvas.height) this.baseY = 0;
        }

        draw() {
            ctx.fillStyle = "rgba(255, 255, 255, 0.5)";
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
            ctx.closePath();
            ctx.fill();
        }
    }

    function init() {
        particles = [];
        for (let i = 0; i < particleCount; i++) {
            const x = Math.random() * canvas.width;
            const y = Math.random() * canvas.height;
            particles.push(new Particle(x, y));
        }
    }

    function connect() {
        for (let a = 0; a < particles.length; a++) {
            for (let b = a; b < particles.length; b++) {
                const dx = particles[a].x - particles[b].x;
                const dy = particles[a].y - particles[b].y;
                const distance = Math.sqrt(dx * dx + dy * dy);

                if (distance < 100) {
                    const opacity = 1 - distance / 100;
                    ctx.strokeStyle = `rgba(255, 255, 255, ${opacity * 0.2})`;
                    ctx.lineWidth = 1;
                    ctx.beginPath();
                    ctx.moveTo(particles[a].x, particles[a].y);
                    ctx.lineTo(particles[b].x, particles[b].y);
                    ctx.stroke();
                }
            }
        }
    }

    function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        particles.forEach((particle) => {
            particle.update();
            particle.draw();
        });

        connect();

        animationId = requestAnimationFrame(animate);
    }

    function handleResize() {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        init();
    }

    function handleMouseMove(event) {
        mouse.x = event.clientX;
        mouse.y = event.clientY;
    }

    function handleMouseLeave() {
        mouse.x = null;
        mouse.y = null;
    }

    onMount(() => {
        canvas = document.getElementById("particle-canvas");
        ctx = canvas.getContext("2d");

        handleResize(); // Initial size setup

        window.addEventListener("resize", handleResize);
        window.addEventListener("mousemove", handleMouseMove);
        window.addEventListener("mouseleave", handleMouseLeave);

        init();
        animate();

        return () => {
            window.removeEventListener("resize", handleResize);
            window.removeEventListener("mousemove", handleMouseMove);
            window.removeEventListener("mouseleave", handleMouseLeave);
            cancelAnimationFrame(animationId);
        };
    });
</script>

<canvas id="particle-canvas"></canvas>

<style>
    canvas {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 0;
        background: linear-gradient(135deg, #0a0a0a 0%, #1a1a2e 100%);
    }
</style>
