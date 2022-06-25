<script>
  import { apiData } from "../store";
  let ticker;

  const handleSubmit = async () => {
    fetch(`https://api.coincap.io/v2/assets/${ticker}`)
      .then((response) => response.json())
      .then((data) => {
        apiData.set({
		data: data.data
        });
      })
      .catch((error) => {
        console.log(error);
        // return [];
		someData = undefined;
      });
  };
</script>

<main>
  <form on:submit|preventDefault={handleSubmit}>
    <input
      class="input-field"
      bind:value={ticker}
      type="text"
      placeholder="Enter coin name"
    />
    <button style="margin-top: 10px;">Submit</button>
  </form>
  <!-- {#if $apiData.data !== undefined} -->
  {#if $apiData.data !== undefined}
    <div class="container">
      <h4>Name: {$apiData.data.name}</h4>
      <h4>Rank: {$apiData.data.rank}</h4>
      <h4>Price: {$apiData.data.priceUsd}</h4>
    </div>
  {/if}
</main>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    text-align: center;
    align-items: center;
    display: flex;
    flex-direction: column;
  }

  .input-field {
    border: 1px solid blue;
    height: 2rem;
  }

  .input-field:hover {
    box-shadow: 1px 1px blue;
  }

  .input-field:focus {
    outline: none;
  }

  .container {
    margin: 20px;
  }
</style>
