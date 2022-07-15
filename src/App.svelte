<script>
  import Item from "./Item.svelte";
  import Search from "./Search.svelte";
  import Calculator from "./Calculator.svelte"
  import axios from "axios";

  var bait;

  function getBait(){   
      axios.get("https://api.slothpixel.me/api/skyblock/bazaar/WHALE_BAIT").then((response) => {
          let sellPrice = Math.round(response.data.quick_status.sellPrice * 10) / 10;
          let buyPrice = Math.round(response.data.quick_status.buyPrice * 10) / 10;
          bait = {
            sellPrice: sellPrice,
            buyPrice: buyPrice
          }
      });
  }

  var items = [];

  getBait();
</script>

<main>
  <div id="items">
    <Item id="RAW_FISH" items={items} amount={5}/>
    <Item id="RAW_FISH:1" items={items} amount={1}/>
    <Item id="PRISMARINE_CRYSTALS" items={items} amount={3}/>
    <Item id="INK_SACK" items={items} amount={1}/>
    <Item id="GOLD_INGOT" items={items} amount={9}/>
  </div>
  <div id="search">
    <Search />
  </div>
  <div id="calculator">
    <Calculator items={items} bait={bait}/>
  </div>
</main>

<style>
  :root{
    background-color: black;
    background-image: url("https://www.transparenttextures.com/patterns/cartographer.png");
    overflow: hidden;
  }

  #items{
    position: relative;
    width: 1630px;
    left: 120px;
    top: 300px;
  }

  #search{
    position: absolute;
    left: 382px;
    top: 535px;
  }

  #calculator{
    position: absolute;
    top: 535px;
    right: 405px;
  }
</style>