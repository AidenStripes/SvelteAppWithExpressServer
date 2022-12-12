<script>
  import { onMount } from "svelte";
  import axios from "axios";

  let quotes = [];
  let error = null;

  onMount(async () => {
    try {
      const res = await axios.get("http://localhost:3001/api/quotes", {
        params: { author: "author", title: "title" },
      });
      quotes = res.data;
    } catch (e) {
      error = e;
    }
  });

  async function update() {
    const res = await axios.get("http://localhost:3001/api/quotes", {
      params: { author: "author", title: "title" },
    });
    quotes = res.data;
  }
</script>

<div>
  <button on:click={update}>UPDATE QUOTES</button>

  <ul>
    {#each quotes as quote}
      <li class="q">{quote.text} <br />
          {quote.author}
      </li>
    {/each}
  </ul>
</div>

<style>
  .q {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    margin-bottom: 50px;
    list-style-type: none;
  }

  .q:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
  }
</style>
