<script>
	import Card from "./components/Card.svelte";
	import OrderBar from "./components/OrderBar.svelte";
	import SideBar from "./components/SideBar.svelte";
	import menu from "./menu.json";
	import daily_menu from "./menu_daily.json";
	import Popup from "./components/Popup.svelte";

	let catagories = [
		{ name: "Sandwiches", image_path: "./images/sandwich/sandwich.jpg" },
		{ name: "Sushi", image_path: "./images/sushi/sushi.jpg" },
		{ name: "Drinks", image_path: "./images/drinks/drinks.jpg" },
	];
	let order = [];
	let current_item = "Sandwiches";
</script>

<main>
	<Popup {daily_menu} bind:order />
	<SideBar {catagories} bind:current_item />
	<div class="card-container">
		{#each menu[current_item] as drink}
			<Card
				name={drink.name}
				price={drink.price}
				image_path={drink.image_path}
				width={"14vw"}
				bind:order
			/>
		{/each}
	</div>
	<OrderBar {order} />
</main>

<style>
	* {
		margin: 0;
		padding: 0;
	}
	main {
		display: flex;
		flex-direction: row;
		align-items: center;
		min-height: 100vh;
		background-color: hsl(0, 0%, 87%);
	}
	.card-container {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-between;
		align-items: center;
	}
</style>
