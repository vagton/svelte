<!-- App.svelte -->
<script>
	import { fade, fly } from "svelte/transition";
	import { fly as flyIn, fade as fadeOut } from "svelte/transition";
	import CustomBox from "./CustomBox.svelte";

	let transition = "";
</script>

<main>
	<h1>Custom Box</h1>

	<label>
		Transition:
		<select bind:value={transition}>
			<option value="">None</option>
			<option value="fade">Fade</option>
			<option value="fly">Fly</option>
			<option value="flyIn">Fly In</option>
			<option value="fadeOut">Fade Out</option>
		</select>
	</label>

	<CustomBox {transition} color="blue" text="Hello, Svelte!" />
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-top: 50px;
	}

	h1 {
		font-size: 24px;
		margin-bottom: 20px;
	}

	label {
		margin-bottom: 20px;
	}

	select {
		font-size: 16px;
		padding: 5px;
	}
</style>
