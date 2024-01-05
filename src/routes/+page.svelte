<script lang="ts">
	import { onMount } from 'svelte';
	import type * as Monaco from 'monaco-editor/esm/vs/editor/editor.api';

	let editor: Monaco.editor.IStandaloneCodeEditor;
	let monaco: typeof Monaco;
	let editorContainer: HTMLElement;

	const value = `function hello() {s
	alert('Hello world!');
}`;

	onMount(async () => {
		monaco = (await import('$lib/monaco')).default;
		// Hover on each property to see its docs!
		const editor = monaco.editor.create(editorContainer, {
			value,
			language: 'markdown',
			automaticLayout: true,
			theme: "vs-dark",
			lineNumbers: "off",
		}); 

		const model = monaco.editor.createModel(
            "console.log('Hello from Monaco! (the editor, not the city...)')",
            'javascript'
        );
		
        editor.setModel(model);

		// `this` is the editor instance
		//console.log(this.getModel().getValue());
	});
</script>

<div class="container" bind:this={editorContainer} />


<style>
    .container {
        width: 100%;
        height: 600px;
    }
</style>