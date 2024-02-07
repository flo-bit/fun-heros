<script lang="ts">
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';

	export let title = 'This could be your product!';
	export let description =
		"So shiny and beautiful, it's almost like you can touch it!";

	export let button = 'Sign the petition!';
	export let buttonHref = '';
</script>

<div
	class="relative isolate bg-gray-50 dark:bg-gray-950 min-h-screen w-screen overflow-x-hidden flex items-center justify-center"
>
	<div
		class="absolute left-[calc(50%-4rem)] top-10 -z-10 transform-gpu blur-3xl sm:left-[calc(50%-18rem)] lg:left-48 lg:top-[calc(50%-30rem)] xl:left-[calc(50%-24rem)]"
		aria-hidden="true"
	>
		<div
			class="aspect-[1108/632] w-[69.25rem] bg-gradient-to-r from-cyan-300 to-emerald-700 opacity-20"
			style="clip-path: polygon(73.6% 51.7%, 91.7% 11.8%, 100% 46.4%, 97.4% 82.2%, 92.5% 84.9%, 75.7% 64%, 55.3% 47.5%, 46.5% 49.4%, 45% 62.9%, 50.3% 87.2%, 21.3% 64.1%, 0.1% 100%, 5.4% 51.1%, 21.4% 63.9%, 58.9% 0.2%, 73.6% 51.7%)"
		></div>
	</div>
	<div class="w-full mx-auto max-w-7xl pb-24 pt-10 sm:pb-32 lg:flex lg:px-8">
		<div
			class="px-6 mx-auto max-w-2xl flex-shrink-0 lg:mx-0 lg:max-w-xl lg:pt-8 lg:py-40 flex items-center mt-5 lg:mt-0"
		>
			<div>
				<h1 class="mt-10 text-4xl font-bold tracking-tight text-black dark:text-white sm:text-6xl">
					{title}
				</h1>
				<p class="mt-6 text-lg leading-8 text-gray-700 dark:text-gray-300">
					{description}
				</p>
				{#if buttonHref && button}
					<div class="mt-10 flex items-center gap-x-6">
						<a
							href={buttonHref}
							class="rounded-lg ring-1 ring-cyan-400 bg-cyan-500 px-8 py-4 text-lg font-semibold text-white shadow-sm hover:bg-cyan-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-amber-400"
							>{button}</a
						>
					</div>
				{/if}
			</div>
		</div>
		<div class="w-full mx-auto flex overflow-hidden mt-10 lg:mt-0">
			<div class="w-full rounded-md h-[90vh] relative">
				<Canvas>
					<Scene />
				</Canvas>
			</div>
		</div>
	</div>
</div>
