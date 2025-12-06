<script>
  import { onMount } from 'svelte';
  import Hero from './components/Hero.svelte';
  import Services from './components/Services.svelte';
  import Contact from './components/Contact.svelte';
  
  let mounted = false;
  
  onMount(() => {
    mounted = true;
  });
</script>

<main class:mounted>
  <Hero />
  <Services />
  <Contact />
</main>

<style>
  main {
    opacity: 0;
    transition: opacity 0.6s ease;
  }
  
  main.mounted {
    opacity: 1;
  }
</style>
