<script>
  import Nav from "../components/Nav.svelte";

  export let segment;
</script>

<style>
  main {
    overflow: hidden;
  }
</style>

<Nav {segment} />

<main>
  <slot />
</main>
