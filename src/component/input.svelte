<script lang="ts">
	import  BalloonEditor from "@ckeditor/ckeditor5-build-balloon";
	import CkEditor5 from "./ckeditor.svelte"

	let editor=BalloonEditor;
	let questionData = "question";
	let answrData = "data";
	


	// setTimeout(async()=>{
	//     await BalloonEditor.create( editor )
	//     .then( editor => {
	//         console.log( 'Editor was initialized', editor );
	//         document.body.appendChild( editor.ui.element );
	//     } )
	//     .catch( err => {
	//         console.error( err.stack );
	//     } );
	// }, 1000)

	// onMount(async ()=>{
	//     var editor = document.querySelector("editorInstance");
	//     var ckEditor = await BalloonEditor.create("test");
	//     editor = ckEditor.ui.element
	// })



	// async function createCkEditor(){
		// console.log(document)
		// await BalloonEditor.create( "test" )
		// .then( editor => {
		//     console.log( 'Editor was initialized', editor );
		//     document.body.appendChild( editor.ui.element );
		// } )
		// .catch( err => {
		//     console.error( err.stack );
		// } );
	// }


	let question:String = "";
	let answr:String = "";

	let styles = {
		"max-width":"100px",
		"max-height":"100px",
	}

	export let width:String = "500px";
	export let height:String = "fit-content";

	console.log(document.getElementsByClassName("editorInstance"))

	function onReady({ detail: editor }) {
		// editor.ui
		// .getEditableElement()
		// .parentElement.insertBefore(
		// 	editor.ui.view.toolbar.element,
		// 	editor.ui.getEditableElement()
		// );
	}

	// afterUpdate(async ()=>{
		// console.log(document)
		// var list = await Array.from(document.querySelectorAll( ".editorInstance" ))
		// console.log(list)
	// })


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
		on:ready={onReady}
		bind:value={questionData}
	/>
	<CkEditor5
		bind:editor
		on:ready={onReady}
		bind:value={answrData}
	/>

</div>

<style>
	.card{
		text-align: left;
		/* outline: 1px solid black; */
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

	/* .card .container textarea:focus::placeholder{
		color: transparent;
	} */

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