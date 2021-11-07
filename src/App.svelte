<script>
	//export let name;

	// router
	import { Router, Link, Route } from "svelte-routing";

	// pages
	import Todo from "./pages/Todo.svelte";
</script>

<Router>
	<Route path="/" component={Todo} />
</Router>

<style lang="postcss" global>
	@import url("https://fonts.googleapis.com/css2?family=Lora&display=swap");
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
</style>
