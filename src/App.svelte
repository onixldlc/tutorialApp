<script lang="ts">
	import InputCard from "./component/input.svelte";
	import "./app.css"
	export let name: String;
</script>

<main>
	<InputCard/>
	<!-- <h1>Hello {name}!</h1> -->
	<!-- <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p> -->
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		display: flex;
		align-items: center;
		flex-direction: column;
		background-color: rgb(151, 177, 255);
		top: 0;
		left: 0;
		margin: 0;
		height: -webkit-fill-available;
		justify-content: center;
	}	

	/* h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	} */

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>