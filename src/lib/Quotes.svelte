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
      <li>{quote.author} said {quote.text}</li>
    {/each}
  </ul>
</div>
