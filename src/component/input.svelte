<script lang="ts">
	import  BalloonEditor from "@ckeditor/ckeditor5-build-balloon";
	import CkEditor5 from "./ckeditor.svelte"

	let editor=BalloonEditor;
	let questionData = "";
	let answrData = "";
	
	let question:String = "";
	let answr:String = "";

	let styles = {
		"max-width":"100px",
		"max-height":"100px",
	}

	export let width:String = "500px";
	export let height:String = "fit-content";

	console.log(document.getElementsByClassName("editorInstance"))

</script>

<div class="card" style="width: {width}; height: {height}">
	<div class="container question">
		<label for="question">question:</label>
		<textarea bind:value={question} name="question" id="question" rows="1" placeholder="question"></textarea>
	</div>
	<div class="container answr">
		<label for="answr">answer</label>
		<textarea bind:value={answr} name="answr" id="answr" rows="1" placeholder="answer"></textarea>
	</div>
	<button>submit</button>

	<CkEditor5
		bind:editor
		bind:value={questionData}
	/>
	<CkEditor5
		bind:editor
		bind:value={answrData}
	/>

</div>

<style>
	.card{
		text-align: left;
		display: flex;
		justify-content: center;
		flex-direction: column;
	}

	.card .container textarea:focus{
		text-align: left;
		width: 100%;
		padding-left: 15px;
		padding-right: 15px;
	}

	.card .container textarea::placeholder{
		text-align: center;
	}
	
	.card .container textarea{
		width: 100px;
		overflow: hidden;
		transition-duration: 200ms;
		border-radius: 100px;
	}
</style>