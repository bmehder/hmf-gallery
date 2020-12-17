<script>
  export let direction = "row";
  export let justify = "left";
  export let align = "baseline";
</script>

<div
  class:column={direction === 'column'}
  class:justify-center={justify === 'center'}
  class:space-between={justify === 'space-between'}
  class:space-around={justify === 'space-around'}
  class:space-evenly={justify === 'space-evenly'}
  class:start={align === 'start'}
  class:center={align === 'center'}
  class:end={align === 'end'}>
  <slot />
</div>

<style>
  div {
    display: flex;
    flex-wrap: wrap;
    align-items: baseline;
    justify-content: left;
    /* height: 100%; */
  }
  .column {
    flex-direction: column;
  }
  .justify-center {
    justify-content: center;
  }
  .space-between {
    justify-content: space-between;
  }
  .space-around {
    justify-content: space-around;
  }
  .space-evenly {
    justify-content: space-evenly;
  }
  .start {
    align-items: flex-start;
  }
  .center {
    align-items: center;
  }
  .end {
    align-items: flex-end;
  }
</style>
