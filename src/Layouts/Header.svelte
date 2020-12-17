<script>
  import { createEventDispatcher } from "svelte";
  export let sticky = false;
  export let uppercase = false;
  export let background = "darkorange";
  export let color = "white";
  export let linkColor = "white";

  const dispatch = createEventDispatcher();
</script>

<header class:sticky style="background:{background};color:{color};">
  <nav>
    <ul class:uppercase>
      <!-- <li><a style="color:{linkColor};" href="/">Home</a></li> -->
      <li>
        <a
          on:click|preventDefault={() => dispatch('pagenav', 'steam')}
          style="color:{linkColor};"
          href="/">STEAM Club</a>
      </li>
      <li>
        <a
          on:click|preventDefault={() => dispatch('pagenav', 'art')}
          style="color:{linkColor};"
          href="/">Art Class</a>
      </li>
      <!-- <li>
        <a
          on:click|preventDefault={() => dispatch('pagenav', 'webdev')}
          style="color:{linkColor};"
          href="/">Web Development</a>
      </li> -->
    </ul>
  </nav>
</header>

<style>
  header {
    /* width: 100%; */
    padding: 1em 0;
    background: darkorange;
    color: white;
    text-align: center;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.25);
  }
  .sticky {
    position: fixed;
    z-index: 100;
  }
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 960px;
    margin: 0 auto;
  }
  nav ul {
    display: flex;
    justify-content: space-between;
  }
  nav ul li {
    list-style-type: none;
    padding: 0 1em;
    font-weight: 600;
  }
  nav ul li a {
    height: auto;
    color: #f3f3f3;
    text-decoration: none;
  }
  nav ul li a:hover {
    padding-bottom: 1em;
    border-bottom: 4px solid #fdc735;
  }
  .uppercase {
    text-transform: uppercase;
  }
  @media screen and (max-width: 600px) {
    nav ul li {
      padding: 0 0.5em;
    }
  }
</style>
