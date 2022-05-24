<script>
    export let name;
    export let price;
    export let image_path;
    export let width;
    export let order;

    function test() {
        let item = {
            name: name,
            price: price,
            quantity: 1,
            image_path: image_path,
        };
        try {
            order.find((obj) => {
                return obj.name == item.name;
            }).quantity++;
        } catch (UncaughtTypeError) {
            order.push(item);
        }

        order = order;
    }
</script>

<div class="card" style="--width: {width}" on:click={test}>
    <img src={image_path} alt="{name} image" />
    <div id="text-box">
        <h3>{name}</h3>
        <p>${price.toFixed(2)}</p>
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
</style>
