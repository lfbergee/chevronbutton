<script>
  import { onMount } from "svelte";
  import ChevronButton from "../components/ChevronButton.svelte";
  import RaisedSection from "../components/RaisedSection.svelte";
  import LatestPost from "../components/LatestPost.svelte";

  function handleClick(event) {
    alert("You clicked the chevron button, it's probably quite happy now 😎");
  }

  let post = {};
  onMount(async () => {
    const res = await fetch(
      "https://api-euwest.graphcms.com/v1/ck4y6untahrrr01bqdwyr6z6h/master",
      {
        method: "post",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          query: `{
          post: blogs(where: {
            status: PUBLISHED
          }, last:1
          ) {
            slug
            title
            content
          }
        }`
        })
      }
    );
    const json = await res.json();
    if (res.status === 200) {
      post = json.data.post[0];
    } else {
      post = null;
    }
  });
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
    font-family: "Seymour One", sans-serif;
    font-size: 3.5rem;
  }

  h2 {
    font-family: "Seymour One", sans-serif;
    font-size: 2rem;
    text-align: center;
  }
</style>

<svelte:head>
  <title>Chevron button</title>
</svelte:head>

<section class="hero">
  <h1>ChevronButton</h1>
  <h2>The home of the all things ChevronButton</h2>

  <RaisedSection>
    <ChevronButton on:click={handleClick}>The chevron button</ChevronButton>
  </RaisedSection>
</section>

{#if post && post.title}
  <LatestPost {...post} />
{/if}
