<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
</script>

<style>
  button {
    border: 1px solid #3d3d3d;
    border-radius: 4px;
    background-color: #fafafa;
    color: #3d3d3d;
    position: relative;
    padding: 12px 38px 12px 12px;
    font-size: 1rem;
    transition: 150ms cubic-bezier(0.075, 0.82, 0.165, 1);
    transition-property: background-color, color;
  }

  button::after {
    content: "›";
    font-size: 2rem;
    line-height: 0.9rem;
    position: absolute;
    right: 18px;
    transition: 250ms cubic-bezier(0.075, 0.82, 0.165, 1) right;
  }

  button:hover::after {
    right: 16px;
  }

  button:active {
    background-color: #3d3d3d;
    color: #fafafa;
  }

  button:active::after {
    right: 8px;
  }
</style>

<button on:click={() => dispatch('click')}>
  <slot />
</button>
