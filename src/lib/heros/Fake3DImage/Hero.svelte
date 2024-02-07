<script lang="ts">
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';

	// @ts-ignore
	import dark from './images/dark.jpg?w=2048&format=webp';
	// @ts-ignore
	import light from './images/light.jpg?w=2048&format=webp';
	// @ts-ignore
	import dark_depth from './images/light-depth.png?w=1024&format=webp';
	// @ts-ignore
	import light_depth from './images/light-depth.png?w=1024&format=webp';
	import { onMount } from 'svelte';

	let image = light;
	let depth = light_depth;

	// optional
	export let buttonHref: string | undefined = undefined;
	export let buttonLabel = 'Button';

	export let backgroundBlend = 'opacity-30';

	export let title: string = 'This 3D effect is fake';
	export let subtitle: string = 'still cool though';

	let darkMode = false;
	const checkTheme = () => {
		const root = document.getElementsByTagName('html')[0];
		if (root.classList.contains('dark')) {
			console.log('dark mode');
			darkMode = true;
		} else {
			console.log('light mode');
			darkMode = false;
		}

		if (darkMode) {
			image = dark;
			depth = dark_depth;
		} else {
			image = light;
			depth = light_depth;
		}
	};

	onMount(() => {
		checkTheme();
	});
</script>

<svelte:body on:click={checkTheme} />

<div class="relative isolate overflow-hidden h-screen w-screen pt-14">
	<img class="absolute -z-20 w-screen h-screen inset-0 blur-sm" src={image} alt="" />
	<div class="absolute -z-10 w-screen h-screen inset-0">
		{#key image}
			<Canvas>
				<Scene
					image={{
						image,
						depth
					}}
				/>
			</Canvas>
		{/key}
	</div>

	<div
		class="absolute inset-0 w-screen h-screen bg-white dark:bg-black {backgroundBlend} -z-10"
	></div>
	<div
		class="absolute inset-x-0 -top-40 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80"
		aria-hidden="true"
	>
		<div
			class="relative left-[calc(50%-11rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 rotate-[30deg] bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-20 sm:left-[calc(50%-30rem)] sm:w-[72.1875rem]"
			style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
		></div>
	</div>
	<div class="mx-auto max-w-2xl h-screen flex items-center justify-center">
		<div class="text-center">
			<h1 class="text-4xl font-bold tracking-tight text-neutral-900 dark:text-white sm:text-6xl">
				{title}
			</h1>
			<p class="mt-6 text-lg leading-8 text-neutral-700 dark:text-neutral-300">
				{subtitle}
			</p>
			<div class="mt-10 flex items-center justify-center gap-x-6">
				{#if buttonHref}
					<a href={buttonHref}>{buttonLabel}</a>
				{/if}
			</div>
		</div>
	</div>
	<div
		class="absolute inset-x-0 top-[calc(100%-13rem)] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[calc(100%-30rem)]"
		aria-hidden="true"
	>
		<div
			class="relative left-[calc(50%+3rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-20 sm:left-[calc(50%+36rem)] sm:w-[72.1875rem]"
			style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
		></div>
	</div>
</div>
