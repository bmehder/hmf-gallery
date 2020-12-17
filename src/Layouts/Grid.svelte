<!-- Do grid template rows -->
<script>
  export let columns = "1fr";
  export let rows = "1fr";
  export let gap = "";
  export let place = "";
</script>

<div
  class="grid-wrap"
  style="grid-template-columns:{columns};grid-template-rows:{rows};grid-gap:{gap};place-items:{place};">
  <slot />
</div>

<style>
  .grid-wrap {
    display: grid;
    max-width: 960px;
  }
  @media screen and (max-width: 600px) {
    .grid-wrap {
      display: block;
    }
  }
</style>
