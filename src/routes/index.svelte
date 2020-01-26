<script>
  import ChevronButton from "../components/ChevronButton.svelte";
  import RaisedSection from "../components/RaisedSection.svelte";
  import LatestPost from "../components/LatestPost.svelte";
  import Loader from "../components/Loader.svelte";
  import { fade } from "svelte/transition";

  function handleClick(event) {
    alert("You clicked the chevron button, it's probably quite happy now 😎");
  }
</script>

<style>
  .hero {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin: 0 2rem;
  }

  h1 {
    margin-top: 92px;
    font-family: "Mukta", sans-serif;
    font-size: 3.5rem;
    text-align: center;
  }

  h2 {
    font-family: "Mukta", sans-serif;
    font-size: 2rem;
    text-align: center;
  }
</style>

<svelte:head>
  <title>Chevron button</title>
</svelte:head>

<section class="hero" transition:fade>
  <h1>
    <span>Chevron</span>
    <span>Button</span>
  </h1>
  <h2>The home of the all things ChevronButton</h2>

  <RaisedSection>
    <ChevronButton on:click={handleClick}>The chevron button</ChevronButton>
  </RaisedSection>
</section>

<LatestPost />
