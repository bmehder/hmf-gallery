<script>
  import { scale } from "svelte/transition";
  import Grid from "../Layouts/Grid.svelte";

  // The endpoint we want to send a GET request to
  export let source;

  // The Heading and color for the Gallery
  export let title;
  export let color;

  // Create an empty array for the posts
  let posts = [];

  // Dynamically console the current post object
  $: posts.length !== 0 ? console.log(posts[postIndex]) : undefined;

  // Is the modal open?
  let isModalOpen = false;

  // Create a variable to hold the Promise
  let promise = (url) => getData(url);

  // Function to get the data using the Fetch API
  async function getData(url) {
    const res = await fetch(url);
    // Turn the response into a JS object
    const data = await res.json();
    // If all is well with the data, put it in the array, and return it.
    if (res.ok) {
      // Put the fetched data in the local posts array variable
      posts = [...data];
      return posts; // An array of objects representing posts
    } else {
      throw new Error(posts);
    }
  }

  // Keep track of the index of the post that was clicked on.
  let postIndex = 0;

  // Update the track index with the index from the each loop.
  const updatePostIndex = (index) => {
    postIndex = index;
    isModalOpen = true;
    window.scrollTo(0, 0);
    // console.log(postIndex);
  };

  // Close the modal
  const closeModal = () => {
    isModalOpen = false;
  };
</script>

<!-- Asynchronously get the posts by invoking the "promise" variable -->
{#await promise(source) then posts}
  <!-- <p>...waiting</p> -->

  <!-- Once the Promise is resolved (successfully)... -->
  <!-- {:then} -->
  {#if !isModalOpen}
    {#if title}
      <h3 style="color:{color};">{title}</h3>
    {/if}
    <Grid columns="1fr 1fr 1fr" gap="2em">
      <!-- 	Loop through each post... -->
      {#each posts as post, i}
        <!-- 	Use the featured image property of the current object as the src attribute -->
        <!-- <h3>{post.title.rendered}</h3> -->
        <a on:click|preventDefault={(e) => updatePostIndex(i)} href="/"><img
            in:scale
            src={post.source_url}
            alt="gallery-item" /></a>
      {/each}
    </Grid>
  {:else}
    <!-- Show the modal when isModalOpen is true -->
    <div transition:scale class="modal" on:click={closeModal}>
      <div>
        <!-- Use the featured image property of the
           current post object for the src attr. -->
        <img src={posts[postIndex].source_url} alt="single item" />
        {#if posts[postIndex].excerpt}
          <p>
            {@html posts[postIndex].excerpt}
          </p>
        {/if}
      </div>
    </div>
  {/if}
  <!-- ...Or, if the Promise is rejected, handle the error -->
{:catch error}
  <p>Something has gone horribly wrong. :-(</p>
  <p style="color: red">{error.message}</p>

  <!-- End Async request -->
{/await}

<style>
  * {
    box-sizing: border-box;
  }
  h3 {
    font-size: 2em;
  }
  img {
    display: block;
    margin: 1em 0;
    width: 250px;
    height: 250px;
    object-fit: cover;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.24);
  }

  .modal {
    position: absolute;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.9);
    cursor: pointer;
  }
  .modal div {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80%;
  }
  .modal img {
    width: auto;
    height: 100%;
  }
  .modal p {
    height: 100%;
    width: 250px;
    padding: 0 2em;
    background: white;
    border: 1px solid #eaeaea;
    line-height: 1.5em;
  }

  @media screen and (max-width: 600px) {
    img {
      width: 90% !important;
      margin: 2em auto;
    }
    .modal div {
      flex-direction: column;
      justify-content: start;
    }
    .modal p {
      width: 100%;
    }
  }
</style>
