<script>
  import Nav from "../components/Nav.svelte";

  export let segment;
</script>

<style>
  main {
    overflow: hidden;
    padding: 64px 0;
  }
</style>

<Nav {segment} />

<main>
  <slot />
</main>
