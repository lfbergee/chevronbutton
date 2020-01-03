<script>
  import ChevronButton from "../components/ChevronButton.svelte";

  function handleClick(event) {
    alert("You clicked the chevron button, it's probably quite happy now 😎");
  }
</script>

<svelte:head>
  <title>Chevron button</title>
</svelte:head>

<h1>The home of the humble chevron button</h1>
<section>
  <h2>Svelte ChevronButton</h2>
  <ChevronButton on:click={handleClick}>The chevron button</ChevronButton>
</section>
