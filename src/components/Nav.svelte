<script>
  export let segment;
</script>

<style>
  nav {
    font-weight: 300;
    padding: 0 1em;
    background-color: var(--green);
    box-shadow: 0 0 4px 2px rgba(0, 0, 0, 0.7);
    color: var(--primary-light);
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 100;
  }

  ul {
    margin: 0;
    padding: 0;
  }

  /* clearfix */
  ul::after {
    content: "";
    display: block;
    clear: both;
  }

  li {
    display: block;
    float: left;
  }

  .selected {
    position: relative;
    display: inline-block;
  }

  .selected::after {
    position: absolute;
    content: "";
    width: calc(100% - 1em);
    height: 4px;
    background-color: var(--primary-light);
    display: block;
    top: 0;
    border-bottom-left-radius: 1px;
    border-bottom-right-radius: 1px;
  }

  a {
    text-decoration: none;
    padding: 1em 0.5em;
    display: block;
    position: relative;
    min-width: 75px;
    text-align: center;
  }
  a::after {
    position: absolute;
    content: " ";
    width: calc(100% - 1em);
    height: 0px;
    background-color: var(--primary-light);
    display: block;
    top: 0;
    transition: 500ms ease;
    transition-property: height, border;
  }

  a:hover::after {
    height: 16px;
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
  }
</style>

<nav>
  <ul>
    <li>
      <a class:selected={segment === undefined} href=".">home</a>
    </li>
    <li>
      <a rel="prefetch" class:selected={segment === 'blog'} href="blog">blog</a>
    </li>
  </ul>
</nav>
