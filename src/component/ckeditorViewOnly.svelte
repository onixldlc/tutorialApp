<script lang="ts">
	import { onMount, onDestroy, createEventDispatcher } from "svelte";
	import debounce from "just-debounce-it";
	import {randomId} from "./helper"
	
	// Properties
	export let editor = null;
	export let value = "";
	export let config = () => ({});

	// Instance variables
	let divName = randomId()
	let instance = null;
	let lastEditorData = "";
	let editorElement;

	const dispatch = createEventDispatcher();

	onMount(() => {
		if (value) {
			Object.assign(config, {
			initialData: value
			});
		}
		editorElement = document.getElementById(divName);
		editor
			.create(editorElement, config)
			.then(editor => {
				// Save the reference to the instance for future use.
				instance = editor;
				// console.log(instance)
				console.log(Array.from( instance.ui.componentFactory.names() ))
				// Set initial disabled state.
                editor.enableReadOnlyMode(editor.id)
                console.log(editor.isReadOnly)
				// editor.isReadOnly = true;

				// Let the world know the editor is ready.
				dispatch("ready", editor);
				setUpEditorEvents();
			})
			.catch(error => {
				console.error(error);
		});
	});
	onDestroy(() => {
		if (instance) {
			instance.destroy();
			instance = null;
		}
		// Note: By the time the editor is destroyed (promise resolved, editor#destroy fired)
		// the Vue component will not be able to emit any longer.
		// So emitting #destroy a bit earlier.
		dispatch("destroy", instance);
	});
	function setUpEditorEvents() {
		const emitInputEvent = evt => {
			// Cache the last editor data. This kind of data is a result of typing,
			// editor command execution, collaborative changes to the document, etc.
			// This data is compared when the component value changes in a 2-way binding.
			const data = (value = lastEditorData = instance.getData());
			dispatch("input", { data, evt, instance });
		};
		// Debounce emitting the #input event. When data is huge, instance#getData()
		// takes a lot of time to execute on every single key press and ruins the UX.
		instance.editing.view.document.on("focus", evt => {
			dispatch("focus", { evt, instance });
		});
		instance.editing.view.document.on("blur", evt => {
			dispatch("blur", { evt, instance });
		});
	}
	</script>
	
	<div id="{divName}" class="editor" />