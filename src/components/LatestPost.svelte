<script>
  import { onMount } from "svelte";
  import marked from "marked";
  import { fade } from "svelte/transition";
  import Loader from "./Loader.svelte";

  let post;
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
            ingress
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
  .dark-green {
    position: relative;
    background-color: var(--green);
    margin: 64px 0;
    padding: 24px;
    min-height: 200px;
  }

  .dark-green::before {
    content: " ";
    position: absolute;
    top: -48px;
    left: -24px;
    height: 150px;
    width: 110%;
    background-color: var(--green);
    transform: rotate(-3deg);
    z-index: -1;
  }

  .dark-green::after {
    content: " ";
    position: absolute;
    bottom: -40px;
    left: -24px;
    height: 150px;
    width: 110%;
    background-color: var(--green);
    transform: rotate(-3deg);
    z-index: -1;
  }

  .dark-green-content {
    min-height: 400px;
    max-width: 768px;
    margin: 0 24px;
    color: var(--primary-light);
  }

  .content {
    max-height: 500px;
    overflow: hidden;
  }

  h2 {
    color: var(--primary-light);
    margin-bottom: 24px;
  }

  @media (min-width: 768px) {
    .dark-green-content {
      margin: 0 150px;
    }
  }
</style>

<section class="dark-green">
  <h2>Latest blog post</h2>
  {#if !post}
    <Loader />
  {:else}
    <article class="dark-green-content" transition:fade>
      <h3>{post.title}</h3>
      <div class="content">
        {@html marked(post.ingress)}
      </div>
      <a href={`/blog/${post.slug}`}>... continue reading</a>
    </article>
  {/if}
</section>
