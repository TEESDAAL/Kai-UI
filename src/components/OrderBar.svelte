<script>
    export let order = [];
    $: total = order
        .reduce((acc, cur) => {
            return acc + cur.price * cur.quantity;
        }, 0)
        .toFixed(2);

    function submit_order() {
        order.length = 0;
    }

    function remove_item(product) {
        console.log("test");
        // let item = {
        //     name: product.name,
        //     price: product.price,
        //     quantity: 1,
        //     image_path: product.image_path,
        // };
        // try {
        //     order.find((obj) => {
        //         return obj.name == item.name;
        //     }).quantity--;
        // } catch (UncaughtTypeError) {
        //     order.push(item);
        // }
        // order = order;
    }
</script>

<div class="order-bar">
    {#if total}
        <h3 id="total">Total:&nbsp{total}</h3>
    {:else}
        <h3 id="total">Total:&nbsp$0.00</h3>
    {/if}
    <div>
        {#each order as drink}
            <div class="order-item">
                <img src={drink.image_path} alt={drink.name} />
                <p>
                    x{drink.quantity} (${(drink.price * drink.quantity).toFixed(
                        2
                    )})
                    <span
                        id="remove-item"
                        on:click={() => {
                            console.log("test");
                        }}>➖</span
                    >
                </p>
            </div>
        {/each}
    </div>

    <button id="order-button" on:click={submit_order}> Order </button>
</div>

<style>
    #remove-item {
        visibility: hidden;
    }
    .order-item:hover #remove-item {
        visibility: visible;
    }
    .order-item:hover #remove-item:hover {
        cursor: pointer;
    }
    .order-bar {
        display: flex;
        flex-direction: column;
        justify-content: end;
        align-items: center;
        background-color: hsl(0, 0%, 94%);
        height: 100%;
        width: max(10vw, 200px);
        font-size: calc(max(10vw, 100px) / 7.5);
        padding: 5px;
        padding-top: 20px;
        filter: drop-shadow(5px 5px 10px hsla(0, 0%, 0%, 0.5));
        box-sizing: border-box;
        min-height: 100vh;
    }
    img {
        width: 20px;
        border-radius: 3px;
        margin-right: 5px;
    }
    .order-item {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: left;
        width: 100%;
        margin-top: 10px;
    }

    #order-button {
        margin-top: auto;
        text-align: center;
        border-radius: 5px;
    }
</style>
