<script>
    export let daily_menu;
    export let order;

    let day = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"];
    let current_day = day[new Date().getDay() - 1];
    if (current_day === undefined) {
        current_day = "Monday";
    }
    let daily_offering = daily_menu[current_day];

    function hide() {
        if (
            document.activeElement.id == "popup" ||
            document.activeElement.id == "order-daily"
        ) {
            return;
        }
        let popup = document.getElementById("popup-container");
        popup.style.display = "none";
    }
    function test() {
        let item = {
            name: daily_offering.name,
            price: daily_offering.price,
            quantity: 1,
            image_path: daily_offering.image_path,
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

<div id="popup-container" on:click={hide}>
    <div id="popup" tabindex="0">
        <h1 id="title">{daily_offering.name}</h1>
        <div id="image-text">
            <img
                src={daily_offering.image_path}
                alt="{daily_offering.name} image"
                id="daily-image"
            />
            <div class="text-order">
                <p>{daily_offering.description}</p>
                <button id="order-daily" on:click={test}>Add to order</button>
            </div>
        </div>
    </div>
</div>

<style>
    #popup-container {
        position: absolute;
        top: 0;
        z-index: 1;
        background-color: hsla(0, 0%, 30%, 80%);
        width: 100vw;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 10px;
    }

    #popup {
        background-color: white;
        width: 50vw;
        height: 50vh;
        padding: 20px;
        border-radius: 20px;
    }

    img {
        margin-top: 15px;
        height: 40vh;
        border-radius: 20px;
    }
    #image-text {
        display: flex;
        flex-direction: row;
        font-size: 25px;
    }

    #image-text img {
        margin-right: 20px;
    }
</style>
