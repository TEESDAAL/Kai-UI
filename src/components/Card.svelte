<script>
    export let item;
    export let width;
    export let order;
    function test() {
        let food = {
            name: item.name,
            price: item.price,
            quantity: 1,
            image_path: item.image_path,
        };
        try {
            order.find((obj) => {
                return obj.name == food.name;
            }).quantity++;
        } catch (UncaughtTypeError) {
            order.push(food);
        }

        order = order;
    }
    console.log(item);
</script>

<div class="card" style="--width: {width}" on:click={test}>
    <img src={item.image_path} alt="{item.name} image" />
    <div id="text-box">
        <h3>{item.name}</h3>
        <p>${item.price.toFixed(2)}</p>
        {#if item.contains_sugar}
            <p class="warning">Contains sugar</p>
        {/if}
        <div id="info">
            {#if item.is_vegetarian}
                <img
                    class="info-img"
                    src="./images/vegetarian.webp"
                    alt="is vegetarian"
                />
            {/if}
            {#if item.is_vegan}
                <img
                    class="info-img"
                    src="./images/vegan.webp"
                    alt="is vegan"
                />
            {/if}
        </div>
    </div>
</div>

<style>
    * {
        margin: 0;
        padding: 0;
    }
    :root {
        --border-radius: 10px;
    }
    .card {
        display: flex;
        flex-direction: column;
        align-items: center;
        border: 1px solid;
        border-radius: var(--border-radius);
        width: var(--width);
        margin: 20px;
        background-color: white;
    }
    #text-box {
        display: flex;
        flex-direction: column;
        text-align: center;
        align-items: center;
        justify-content: space-around;
        height: 15vh;
    }
    .card:hover {
        filter: drop-shadow(5px 5px 10px rgba(0, 0, 0, 0.5));
        cursor: pointer;
    }
    img {
        width: 100%;
        border-radius: 10px 10px 0 0;
    }
    #info {
        display: flex;
        justify-content: space-around;
        width: 100%;
    }
    .warning {
        color: red;
    }
    .info-img {
        width: 30px;
    }
</style>
