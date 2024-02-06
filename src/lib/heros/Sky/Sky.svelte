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
	
	<div class="mx-auto max-w-4xl px-8 sm:px-16 py-32 sm:py-48 lg:py-72">
		<div class="text-left">
			<p class="mt-6 text-lg leading-8 text-neutral-700 dark:text-neutral-300 mb-8 font-semibold">
				{company}
			</p>
			<h1 class="text-4xl font-bold tracking-tight text-neutral-900 dark:text-white sm:text-6xl">
				{#if title}
					{@html title}
				{/if}
			</h1>
			{#if buttonHref}
				<div class="mt-10 flex items-center justify-start">
					<a
						href={buttonHref}
						class="rounded-lg ring-1 ring-cyan-400 bg-cyan-500 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-cyan-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-amber-400"
						>{buttonLabel}</a
					>
				</div>
			{/if}
		</div>
	</div>
</div>
