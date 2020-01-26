<script>
  import { fade } from "svelte/transition";
</script>

<style>
  div {
    position: absolute;
    top: 50px;
    width: 100vw;
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  @keyframes loading {
    0% {
      opacity: 0;
      transform: scale(0.2);
    }
    50% {
      opacity: 1;
      transform: scale(1);
    }
    100% {
      opacity: 0;
      transform: scale(0.2);
    }
  }

  span {
    height: 40px;
    width: 40px;
    background-color: var(--primary-light);
    border-radius: 50%;
    animation: loading 2s infinite;
  }
</style>

<div transition:fade>
  <span />
</div>
