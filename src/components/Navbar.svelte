<script>
  import { onMount } from 'svelte';
  export let darkMode = false;

  let scrolled = false;
  function onScroll() {
    scrolled = window.scrollY > 10;
  }

  onMount(() => {
    onScroll();
    window.addEventListener('scroll', onScroll);
    return () => window.removeEventListener('scroll', onScroll);
  });

  // Tailwind classes that contain characters like "/" or ":" can't be used with Svelte's class:directive.
  // Compute a class string instead and bind it in the class attribute.
  $: bgClass = scrolled ? (darkMode ? 'bg-black/90' : 'bg-white/90') : '';
</script>

<nav class="fixed top-0 left-0 right-0 z-50 transition-all duration-300 {bgClass}" class:nav-blur={scrolled}>
  <!-- Navbar content -->
  <slot />
</nav>
