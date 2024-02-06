<script lang="ts">
	import confetti from 'canvas-confetti';
	import { onMount } from 'svelte';

	onMount(() => {
		setTimeout(() => {
			if (window.scrollY <= 20) {
				launchConfetti();
			}
		}, 100);
	});

	const launchConfetti = () => {
		let count = 200;
		let defaults = {
			origin: { y: 0.7 }
		};

		function fire(particleRatio: number, opts: confetti.Options | undefined) {
			confetti({
				...defaults,
				...opts,
				particleCount: Math.floor(count * particleRatio)
			});
		}

		fire(0.25, {
			spread: 26,
			startVelocity: 55
		});
		fire(0.2, {
			spread: 60
		});
		fire(0.35, {
			spread: 100,
			decay: 0.91,
			scalar: 0.8
		});
		fire(0.1, {
			spread: 120,
			startVelocity: 25,
			decay: 0.92,
			scalar: 1.2
		});
		fire(0.1, {
			spread: 120,
			startVelocity: 45
		});
	};

	export let title = 'Fun, interactive hero sections 🎉';
	export let description = 'Wow your visitors with a fun, interactive hero section. Created with svelte, tailwind, threlte and others.';

</script>

<div class="bg-white dark:bg-black">
	<div class="relative isolate px-6">
		<div
			class="absolute inset-x-0 -top-40 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80"
			aria-hidden="true"
		>
			<div
				class="relative left-[calc(50%-11rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 rotate-[30deg] bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%-30rem)] sm:w-[72.1875rem]"
				style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
			></div>
		</div>
		<div class="flex items-center h-screen">
			<div class="mx-auto max-w-2xl py-32 sm:py-48 lg:py-56">
				<div class="text-center">
					<h1 class="text-4xl font-bold tracking-tight text-gray-900 dark:text-gray-50 sm:text-6xl">
						{title}
					</h1>
					<p class="mt-6 text-lg leading-8 text-gray-600 dark:text-gray-400">
						{description}
					</p>
					<div class="mt-10 flex items-center justify-center gap-x-6">
						<button
							on:click={launchConfetti}
							class="rounded-md bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 px-5 py-3 text-lg font-semibold text-white shadow-sm hover:opacity-90 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
							>Confetti</button
						>
					</div>
				</div>
			</div>
		</div>
		<div
			class="absolute inset-x-0 top-[calc(100%-13rem)] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[calc(100%-30rem)]"
			aria-hidden="true"
		>
			<div
				class="relative left-[calc(50%+3rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 bg-gradient-to-tr from-blue-400 to-rose-500 opacity-30 sm:left-[calc(50%+36rem)] sm:w-[72.1875rem]"
				style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
			></div>
		</div>
	</div>
</div>
