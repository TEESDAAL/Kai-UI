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

	let catagories = [
		{ name: "Sandwiches", image_path: "./images/sandwich/sandwich.jpg" },
		{ name: "Sushi", image_path: "./images/sushi/sushi.jpg" },
		{ name: "Drinks", image_path: "./images/drinks/drinks.jpg" },
	];
	let order = [];

	let current_item = "Sandwiches";
	function add_daily() {
		console.log("test");
		// let item = {
		// 	name: menu_daily[current_day].name,
		// 	price: menu_daily[current_day].price,
		// 	quantity: 1,
		// 	image_path: menu_daily[current_day].image_path,
		// };
		// try {
		// 	order.find((obj) => {
		// 		return obj.name == item.name;
		// 	}).quantity++;
		// } catch (UncaughtTypeError) {
		// 	order.push(item);
		// }

		// order = order;
	}
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
		<Card
			name={daily_menu[current_day].name}
			price={daily_menu[current_day].price}
			image_path={daily_menu[current_day].image_path}
			width={"14vw"}
			bind:order
			on:click={add_daily}
		/>
	</div>
	<OrderBar {order} />
	<OrderPopup bind:order />
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
