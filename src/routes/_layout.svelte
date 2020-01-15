<script>
  import Nav from "../components/Nav.svelte";

  // export let segment;
</script>

<style>
  main {
    height: 100vh;
	/* padding: 25px; */
	background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
  }
</style>

<!-- <Nav {segment}/> -->

<main>
  <slot />
</main>
