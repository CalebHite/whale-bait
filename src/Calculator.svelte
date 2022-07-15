<script>
    export let items;
    export let bait;

    let num;
    let makeNum;

    var totalPrice = 0;

    var totalProfit = 0;

</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Oswald&family=Roboto+Mono&display=swap" rel="stylesheet">
</svelte:head>

<main>
    <h1 id="input-text">Calculate Total Cost</h1>
    <input type="text" placeholder="Amount to Make" bind:value={num} on:change={() => {
        totalPrice = 0;
        for(let i = 0; i < items.length; i++){
            totalPrice = Math.round(totalPrice * 10 + (items[i].sellPrice * items[i].amount * num) * 10) / 10;
        }

        totalProfit = Math.round((bait.buyPrice * num * 10) - totalPrice * 10) / 10
    }}>
    <input type="submit" value="Calculate" on:click={() => {makeNum = num;}}>

    {#if totalPrice > 0}
        <div id="output">
            <div id="left-items">
                <h1>Total Cost: {totalPrice} Coins</h1>
                <h1>Total Profit: {totalProfit} Coins</h1>
            </div>
            <div id="right-items">
                {#each items as {name, sellPrice, amount}}
                <h2>{amount * makeNum} {name}: {Math.round(sellPrice * amount * makeNum * 10) / 10} Coins</h2>
                {/each}
            </div>
        </div>
    {/if}
</main>

<style>    
    #input-text{
        font-family: 'Oswald', sans-serif;
        font-weight: 300px;
        color: white;
    }

    #output{
        position: absolute;
        top: 155px;
        left: 50px;
        width: 1200px;
        height: 270px;
        border-radius: 5px;
        border: 3px white solid;
        background-color: #3D56B2;
        color: white;
    }
    #left-items{
        position:absolute;
        left: 0;
        margin-left: 20px;
        font-family: 'Oswald', sans-serif;
        font-size: 1rem;
        font-weight: 300px;
    }
    #right-items{
        position:absolute;
        right: 0;
        text-align: right;
        margin-right: 20px;
        font-family: 'Roboto Mono', monospace;
    }
</style>