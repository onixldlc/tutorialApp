<script lang="ts">
    
	import  BalloonEditor from "@ckeditor/ckeditor5-build-balloon";
	// import CkEditor5 from "./ckeditor.svelte"
	import CkEditor5 from "./ckeditorViewOnly.svelte"

	let editor=BalloonEditor;

	let question:string = "什么";
	let answr:string[] = ["what?", "who?", "why?"];

	export let width:String = "fit-content";
	export let height:String = "fit-content";


</script>

<div class="card" style="width: {width}; height: {height}">
	<div class="container question">
		<CkEditor5
			bind:editor
			bind:value={question}
			/>
	</div>

    <!-- {#each answr as {value}, i}
    
    {/each} -->
</div>

<style>
	.card{
		content: "";
		text-align: left;
		display: flex;
		justify-content: center;
		flex-direction: column;
		position: absolute;
	}

	.card > *{
		margin-top: 10px;
	}

	.card .container{
		border-bottom: 2px solid rgba(0, 0, 0, 0.341);
	}

</style>