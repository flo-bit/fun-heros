<script lang="ts">
	import { onMount } from 'svelte';

	export let buttonHref: string | undefined = undefined;
	export let buttonLabel = 'Button';

	export let backgroundBlend = 'opacity-30 backdrop-blur-sm';

	export let title: string = '';

	export let titles = [
		'Innovative Technology.',
		'Green Solutions.',
		'Community Engagement.',
		'Sustainable Development.'
	];

	export let titleDuration = 3900;

	export let video = '/fun-heros/background.mov';

	export let company = 'EcoInnovate';

	let i = 0;

	onMount(() => {
		setInterval(() => {
			i = (i + 1) % titles.length;
		}, titleDuration);
	});
</script>

<div class="relative isolate overflow-hidden pt-14 h-screen">
	<video autoplay muted loop class="absolute inset-0 -z-10 h-screen w-full object-cover">
		<source src={video} type="video/mp4" />
	</video>

	<div class="absolute inset-0 w-full h-full bg-white dark:bg-black {backgroundBlend} -z-10"></div>

	<div class="mx-auto max-w-4xl px-8 sm:px-16 py-32 sm:py-48 lg:py-72">
		<div class="text-left">
			<p class="mt-6 text-lg leading-8 text-neutral-700 dark:text-neutral-300 mb-8 font-semibold">
				{company}
			</p>
			<h1 class="text-4xl font-bold tracking-tight text-neutral-900 dark:text-white sm:text-6xl">
				{#if title}
					{@html title}
				{/if}
				{#key titles[i]}
					<span class="text-black dark:text-white">{titles[i]}</span>
				{/key}
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
