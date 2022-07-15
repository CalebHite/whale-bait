<script>
import { create_component } from "svelte/internal";
    import Item from "./Item.svelte";
    let itemID;
</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Oswald&family=Roboto+Mono&display=swap" rel="stylesheet">
</svelte:head>

<main>
    <h1 id="input-text">Search for Items</h1>
    <input type="text" placeholder="Item ID" bind:value={itemID}>
    {#key itemID}
        <div class="item">
            <Item id={itemID}/>
        </div>
    {/key}
</main>

<style>
    #input-text{
        font-family: 'Oswald', sans-serif;
        font-weight: 300px;
        color: white;
    }

    .item{
        position: absolute;
        top: 140px;
        left: -65px;
    }
</style>
