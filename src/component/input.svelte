
<script lang="ts">
	// ck editor script
	import  BalloonEditor from "@ckeditor/ckeditor5-build-balloon";
	import CkEditor5 from "./ckeditor.svelte"

	let editor=BalloonEditor;
	let questionData = "Question ?";
	let answrData = "Answer";
	
	let question:String = "";
	let answr:String = "";

	// ----------------------------------
	// other Default properties

	let styles = {
		"max-width":"100px",
		"max-height":"100px",
	}

	export let width:String = "500px";
	export let height:String = "fit-content";

	var getParrent = (e) => e.detail.instance.sourceElement.parentElement

	const changeAttribute = {
		classnames: null,
		returns: [],
		change: function(e){
			var parent = e.detail.instance.sourceElement.parentElement
			var retArr: string[];

			this.classNames = parent.getAttribute("class")

			if(!this.classNames.includes("inputFocused ")){
				retArr = [this.classNames, "inputFocused " + this.classNames];
			}else{
				retArr = ["inputFocused ", ""]
			}

			parent.setAttribute("class", this.classNames.replace(...retArr))
		}
	}

	function ckeditorFocus(e){
		changeAttribute.change(e)
	}

	function ckeditorBlur(e){
		changeAttribute.change(e)
	}

</script>

<div class="card" style="width: {width}; height: {height}">
	<div class="container question">
		<CkEditor5
			bind:editor
			bind:value={questionData}
			on:focus={ckeditorFocus}
			on:blur={ckeditorBlur}
			/>
		<div class="inputFocused dummy" style="display: none;"></div>
	</div>

	<div class="container answr">
		<CkEditor5
			bind:editor
			bind:value={answrData}
			on:focus={ckeditorFocus}
			on:blur={ckeditorBlur}
			/>
	</div>

	<button>submit</button>
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

	.inputFocused::after{
		width: 100% !important;
		height: 2px;
	}

	.card .container::after{
		display: block;
		position: absolute;
		content: " ";
		background-color: rgb(71, 138, 255);
		width: 0%;
		height: 4px;
		transition-duration: 500ms;
		pointer-events: none;
	}



</style>