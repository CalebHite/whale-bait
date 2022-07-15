<script>
    import axios from "axios";
    const baseURL = "https://api.slothpixel.me/api/skyblock/bazaar/";
  
    export let id;
    export let amount;

    let itemID = id;
  
    let sellPrice;
    let buyPrice;
    let name;

    export let items;

    function getItem(itemID){   
            axios.get(baseURL + itemID).then((response) => {
                name = response.data.name;
                sellPrice = Math.round(response.data.quick_status.sellPrice * 10) / 10;
                buyPrice = Math.round(response.data.quick_status.buyPrice * 10) / 10;

                items.push({
                  name: name,
                  sellPrice: sellPrice,
                  amount: amount
                })
            });
    }
    
    getItem(itemID);
</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Oswald&family=Roboto+Mono&display=swap" rel="stylesheet">
</svelte:head>

<main>
  {#if sellPrice !== undefined && buyPrice !== undefined}
      <div class="item">
        <h1 class="name">{name}</h1>
        <h2>Sell Price: {sellPrice} Coins</h2>
        <h2>Buy Price: {buyPrice} Coins</h2>
      </div>
  {/if}
</main>
<style>  
  .item{
    width: 300px;
    height: 200px;
    border-radius: 5px;
    border: 3px white solid;
    background-color: #3D56B2;
    color: white;
    text-align: center;
    margin: 10px;
    float: left;
  }

  .name{
    font-family: 'Oswald', sans-serif;
    font-weight: 300px;
    font-size: 2.4rem;
  }

  h2{
    font-family: 'Roboto Mono', monospace;
    font-size: 1.2rem;
  }
</style>