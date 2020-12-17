<script>
  export let background = "darkorange";
  export let color = "white";
  export let height = "";
</script>

<footer style="height:{height};background:{background};color:{color};">
  <slot />
</footer>

<style>
  footer {
    padding: 1.5rem;
    background: darkorange;
    color: white;
    text-align: center;
    font-weight: 600;
  }
</style>
