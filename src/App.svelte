<script>
  import { onMount } from "svelte";
  import ParticleBackground from "./components/ParticleBackground.svelte";
  import Hero from "./components/Hero.svelte";
  import Services from "./components/Services.svelte";
  import Contact from "./components/Contact.svelte";

  let mounted = false;

  onMount(() => {
    mounted = true;
  });
</script>

<div class="particle-container">
  <ParticleBackground />
</div>

<main class:mounted>
  <Hero />
  <Services />
  <Contact />
</main>

<style>
  .particle-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    z-index: -1;
    pointer-events: none;
  }

  main {
    position: relative;
    opacity: 0;
    transition: opacity 0.6s ease;
  }

  main.mounted {
    opacity: 1;
  }
</style>
