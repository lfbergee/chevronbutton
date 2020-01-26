<script context="module">
  export async function preload({ params, query }) {
    // the `slug` parameter is available because
    // this file is called [slug].svelte
    const res = await this.fetch(
      "https://api-euwest.graphcms.com/v1/ck4y6untahrrr01bqdwyr6z6h/master",
      {
        method: "post",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          query: `query Post($slug: String) {
            post: blog(where: {
              slug: $slug
            }) {
              slug
              title
              ingress
              content
            }
          }`,
          variables: {
            slug: params.slug
          }
        })
      }
    );
    const json = await res.json();

    if (res.status === 200) {
      return json.data;
    } else {
      this.error(res.status, json && json.errors);
    }
  }
</script>

<script>
  import marked from "marked";
  import { fade } from "svelte/transition";

  export let post;
</script>

<style>
  section {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  article {
    background-color: white;
    padding: 4rem 4rem 2rem 3rem;
  }
  @media (min-width: 768px) {
    article {
      width: 100%;
      max-width: 700px;
    }
  }
</style>

<svelte:head>
  <title>{post.title}</title>
</svelte:head>
<section transition:fade>
  <article transition:fade>
    <h1>{post.title}</h1>
    {@html marked(post.ingress)}

    {@html marked(post.content)}
  </article>
</section>
