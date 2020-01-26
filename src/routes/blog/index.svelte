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
            ingress
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
  import { fade } from "svelte/transition";
  import marked from "marked";

  let searchTerm = "";
  const getPosts = term => posts.filter(post => post.title.includes(term));
</script>

<style>
  section {
    margin: 0 32px;
  }
  article {
    background-color: white;
    position: relative;
    padding: 32px;
    box-shadow: 0 0 4px -2px rgba(0, 0, 0, 0.7);
    transition: 125ms ease box-shadow;
  }
  article:focus-within,
  article:hover {
    box-shadow: 0 0 8px -2px rgba(0, 0, 0, 0.7);
  }
  article::before {
    content: " ";
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    width: 4px;
    background-color: var(--green);
  }

  a:focus {
    outline: none;
  }

  a::before {
    content: "";
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }

  input {
    background-color: transparent;
    border: none;
    font-size: 1rem;
    width: 120px;
  }
  input:focus {
    outline: none;
  }

  .search {
    margin: 24px 0;
    padding: 8px 16px;
    border-radius: 4px;
    transition: 125ms ease;
    transition-property: box-shaddow, width;
    display: inline-flex;
    overflow: hidden;
  }
  .search:hover,
  .search:focus-within {
    box-shadow: 0px 1px 2px 0px rgba(0, 0, 0, 0.7);
  }
  i {
    color: darkgray;
  }
  .top {
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
    align-items: center;
    margin: 0;
  }
  h1 {
    margin: 0;
    margin-right: 2rem;
  }
  .blog {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  @media (min-width: 768px) {
    .top,
    article {
      width: 100%;
      max-width: 700px;
    }
  }
</style>

<svelte:head>
  <title>ChevronButton - Blog</title>
</svelte:head>

<section class="blog" transition:fade>
  <section class="top">
    <h1>Blog</h1>
    <aside class="search">
      <i class="material-icons">search</i>
      <input
        type="text"
        placeholder="Search posts..."
        bind:value={searchTerm} />
    </aside>
  </section>

  {#each getPosts(searchTerm) as post}
    <article transition:fade>
      <h3>{post.title}</h3>
      {@html marked(post.ingress)}
      <a rel="prefetch" href="blog/{post.slug}">... continue reading</a>
    </article>
  {/each}
</section>
