<script>
	import Card from "./components/Card.svelte";
	import OrderBar from "./components/OrderBar.svelte";
	import SideBar from "./components/SideBar.svelte";
	import menu from "./menu.json";
	import daily_menu from "./menu_daily.json";
	import Popup from "./components/Popup.svelte";
	import OrderPopup from "./components/OrderPopup.svelte";

	let day = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"];
	let current_day = day[new Date().getDay() - 1];

	if (current_day === undefined) {
		current_day = "Monday";
	}

	let catagories = [
		{ name: "Sandwiches", image_path: "./images/sandwich/sandwich.jpg" },
		{ name: "Sushi", image_path: "./images/sushi/sushi.jpg" },
		{ name: "Drinks", image_path: "./images/drinks/drinks.jpg" },
	];
	let order = [];

	let current_item = "Sandwiches";
	let show_receipt = false;
</script>

<main>
	<Popup {daily_menu} bind:order />
	<SideBar {catagories} bind:current_item />
	<div class="card-container">
		{#each menu[current_item] as drink}
			<Card item={drink} width={"14vw"} bind:order />
		{/each}
		<Card item={daily_menu[current_day]} width={"14vw"} bind:order />
	</div>
	<OrderBar {order} bind:show_receipt />
	<OrderPopup bind:order bind:show_receipt />
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
