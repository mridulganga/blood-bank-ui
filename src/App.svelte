<script>
	import { Route, router } from "tinro";
	router.mode.hash();

	import Login from "./pages/login.svelte";
	import Signup from "./pages/signup.svelte";
	import ListUsers from "./pages/list_users.svelte";
	import ListOrders from "./pages/list_orders.svelte";
	import ListDonations from "./pages/list_donations.svelte";

	let showNav = false;

	var user = localStorage.getItem("user");
	console.log(user);
	if (user != null) {
		router.goto("/listusers");
	} else {
		console.log("no user set");
		router.goto("/login");
	}
</script>

<main>
	<Route path="/login"><Login /></Route>
	<Route path="/signup"><Signup /></Route>
	<Route path="/listusers"><ListUsers /></Route>
	<Route path="/listorders"><ListOrders /></Route>
	<Route path="/listdonations"><ListDonations /></Route>
</main>
