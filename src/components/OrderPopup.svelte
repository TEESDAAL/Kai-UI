<script>
    export let order;
</script>

<div
    id="order-popup"
    on:click={() => {
        document.getElementById("order-popup").style.display = "none";
    }}
>
    <div
        id="receipt"
        on:click={(event) => {
            event.stopImmediatePropagation();
        }}
    >
        <h1>Kai UI</h1>
        <hr />
        <h2>Virtual Receipt</h2>
        <hr />
        <div class="item">
            <p><b>Description</b></p>
            <p><b>Price</b></p>
        </div>
        {#each order as item}
            <div class="item">
                <p>{item.name}</p>
                <p>${item.price.toFixed(2)} x{item.quantity}</p>
            </div>
        {/each}
        <hr />
        <div class="total">
            <p>
                Total: ${order
                    .reduce((acc, item) => {
                        return acc + item.price * item.quantity;
                    }, 0)
                    .toFixed(2)}
            </p>
        </div>
    </div>
</div>

<style>
    #receipt {
        background-color: white;
        width: 30vw;
        min-height: 30vh;
        margin: auto;
        padding: 20px;
        border-radius: 5px;
        justify-content: center;
    }
    #order-popup {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        display: none;
    }
    .item {
        display: flex;
        justify-content: space-between;
    }
</style>
