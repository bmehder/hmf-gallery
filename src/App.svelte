<script>
  import Section from "./Layouts/Section.svelte";
  import Gallery from "./UI/Gallery.svelte";
</script>

<Section background="#00003e" padding="2em 0">
  <Gallery
    source="https://highlandsmotoringfestival.com/wp-json/wp/v2/media?per_page=100"
    title="Highlands Motoring Festival"
    color="white" />
</Section>

<style>
</style>
