<script>
  import { Accordion, AccordionItem } from "./lib/accordion";

  let open = $state(false);
</script>

<Accordion bind:open>
  <AccordionItem
    >{#snippet accordionItem({ open, toggle })}
      <button onclick={toggle} class="accordion-heading">
        <div>MY TITLE</div>
        <div class="accordion-trigger" class:open>x</div>
      </button>

      {#if open}
        <div class="accordion-content">test</div>
      {/if}
    {/snippet}</AccordionItem
  >
</Accordion>
