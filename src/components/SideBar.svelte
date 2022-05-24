<script>
    export let catagories;
    export let current_item;
</script>

<div id="catagory-selector">
    {#each catagories as catagory}
        <img
            src={catagory.image_path}
            alt={catagory.name}
            class="option-selector"
            on:click={() => (current_item = catagory.name)}
        />
    {/each}
</div>

<style>
    #catagory-selector {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        min-height: 100vh;
        background-color: hsl(0, 0%, 80%);
        flex-grow: 1;
    }
    .option-selector {
        width: 100px;
        height: 100px;
        border-radius: 5px;
        margin: 10px;
        cursor: pointer;
    }
</style>
