<script>
  import { setContext } from "svelte";

  let { open = $bindable(), children } = $props();

  setContext("accordion", {
    get open() {
      return open;
    },
  });
</script>

<div class="accordion">
  <!-- {#if children}
    {@render children()}
  {:else}
    Fallback
  {/if} -->

  <!-- OR THIS STYLE -->
  {@render children?.()}
</div>
