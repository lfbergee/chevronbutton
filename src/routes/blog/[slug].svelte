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
              createdAt
              title
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

  export let post;
</script>

<svelte:head>
  <title>{post.title}</title>
</svelte:head>

<h1>{post.title}</h1>

<div class="content">
  {@html marked(post.content)}
</div>
