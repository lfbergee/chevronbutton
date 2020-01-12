<script>
  import marked from "marked";

  export let title = "";
  export let content = "";
</script>

<style>
  .dark-green {
    position: relative;
    background-color: var(--green);
    margin: 64px 0;
    padding: 24px;
  }

  .dark-green::before {
    content: " ";
    position: absolute;
    top: -48px;
    left: -24px;
    height: 200px;
    width: 110%;
    background-color: var(--green);
    transform: rotate(-3deg);
    z-index: -1;
  }

  .dark-green::after {
    content: " ";
    position: absolute;
    bottom: -48px;
    left: -24px;
    height: 200px;
    width: 110%;
    background-color: var(--green);
    transform: rotate(-3deg);
    z-index: -1;
  }

  .dark-green-content {
    min-height: 400px;
    max-width: 768px;
    margin: 0 48px;
    color: var(--primary-light);
  }

  @media (min-width: 768px) {
    .dark-green-content {
      margin: 0 150px;
    }
  }
</style>

<section class="dark-green">
  <article class="dark-green-content">
    <h2>{title}</h2>
    <div class="content">
      {@html marked(content)}
    </div>

  </article>
</section>
