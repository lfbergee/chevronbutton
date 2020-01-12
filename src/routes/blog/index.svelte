<script context="module">
  export async function preload(page, session) {
    const res = await this.fetch(
      "https://api-euwest.graphcms.com/v1/ck4y6untahrrr01bqdwyr6z6h/master",
      {
        method: "post",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          query: `{
          posts: blogs(where: {
            status: PUBLISHED
          }) {
            slug
            title
            description
          }
        }`
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
  export let posts;
</script>

<style>
  ul {
    margin: 0 0 1em 0;
    line-height: 1.5;
  }
</style>

<svelte:head>
  <title>Blog</title>
</svelte:head>

<h1>Blog posts</h1>

<ul>
  {#each posts as post}
    <li>
      <a rel="prefetch" href="blog/{post.slug}">{post.title}</a>
    </li>
  {/each}
</ul>
