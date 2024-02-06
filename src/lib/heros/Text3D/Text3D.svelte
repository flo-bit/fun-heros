<script lang="ts">
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';

	export let title = 'General Kenobi!';
	
	export let buttonLabel = 'Sign the petition!';
	export let buttonHref = '';

	export let company = 'hello there';
</script>


<div class="relative isolate overflow-hidden pt-14 h-screen">
	<div class="absolute inset-0 -z-10 h-screen w-full">
		<Canvas>
			<Scene />
		</Canvas>
	</div>
	
</div>
