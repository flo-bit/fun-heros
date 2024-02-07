<script lang="ts">
	let basicExamples = [{
		name: 'Confetti',
		href: '/confetti',
		image: '/previews/confetti.png',
		image_dark: '/previews/confetti-dark.png',
		alt: 'Cool confetti effect'
	}, {
		name: 'Video',
		href: '/video',
		image: '/previews/video.png',
		image_dark: '/previews/video-dark.png',
		alt: 'Background video with text overlay'
	}]

	let threeDExamples = [ {
		name: 'Phone Mockup',
		href: '/phone-mockup',
		image: '/previews/phone.png',
		image_dark: '/previews/phone-dark.png',
		alt: 'Interactive 3D phone mockup'
	}, {
		name: 'Character',
		href: '/character',
		image: '/previews/character.png',
		image_dark: '/previews/character-dark.png',
		alt: 'Animated character'
	}, {
		name: 'Fake 3D Image',
		href: '/fake-3d-image',
		image: '/previews/fake3d.png',
		image_dark: '/previews/fake3d-dark.png',
		alt: 'Fake 3D effect'
	}, {
		name: 'Text 3D',
		href: '/text-3d',
		image: '/previews/text3d.png',
		image_dark: '/previews/text3d-dark.png',
		alt: '3D text effect'
	}, {
		name: 'Product Showcase',
		href: '/product',
		image: '/previews/product.png',
		image_dark: '/previews/product-dark.png',
		alt: '3D product showcase'
	}];

	const textExamples = [
		{
			name: 'Fluid Text',
			href: '/fluid-text',
			image: '/previews/fluidtext.png',
			image_dark: '/previews/fluidtext-dark.png',
			alt: 'Text that flows like water'
		}
	] 
</script>

<div class="bg-white dark:bg-black py-24 sm:py-32">
	<div class="mx-auto max-w-7xl px-6 lg:px-8">
		<div class="mx-auto max-w-2xl text-center">
			<h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl dark:text-gray-50">
				3D heros
			</h2>
			<p class="mt-2 text-lg leading-8 text-gray-600 dark:text-gray-400">
				All the 3D hero sections, with new ones being added whenever I feel like it
			</p>
		</div>
		<div
			class="mx-auto mt-16 grid max-w-2xl auto-rows-fr grid-cols-1 sm:grid-cols-2 gap-8 sm:mt-20 lg:mx-0 lg:max-w-none lg:grid-cols-3"
		>
			{#each threeDExamples as example}
				<article
					class="relative isolate flex flex-col justify-end overflow-hidden rounded-2xl bg-gray-900 px-8 pb-8 pt-80 sm:pt-48 lg:pt-80"
				>
					<img
						src="/fun-heros{example.image}"
						alt={example.alt}
						class="absolute block dark:hidden inset-0 -z-10 h-full w-full object-cover"
					/>

					<img
						src="/fun-heros{example.image_dark}"
						alt={example.alt}
						class="absolute hidden dark:block inset-0 -z-10 h-full w-full object-cover"
					/>
					<div
						class="absolute inset-0 -z-10 bg-gradient-to-t from-gray-900/70 via-gray-900/30"
					></div>
					<div
						class="absolute inset-0 -z-10 rounded-2xl ring-1 ring-inset ring-gray-900/10 dark:ring-white/5"
					></div>

					<h3 class="mt-3 text-lg font-semibold leading-6 text-white">
						<a href="/fun-heros{example.href}">
							<span class="absolute inset-0"></span>
							{example.name}
						</a>
					</h3>
				</article>
			{/each}
		</div>

		<div class="mx-auto max-w-2xl text-center pt-24 sm:pt-32">
			<h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl dark:text-gray-50">
				Text effects
			</h2>
			<p class="mt-2 text-lg leading-8 text-gray-600 dark:text-gray-400">
				Do something cool with your title text
			</p>
		</div>
		<div
			class="mx-auto mt-16 grid max-w-2xl auto-rows-fr grid-cols-1 sm:grid-cols-2 gap-8 sm:mt-20 lg:mx-0 lg:max-w-none lg:grid-cols-3"
		>
			{#each textExamples as example}
				<article
					class="relative isolate flex flex-col justify-end overflow-hidden rounded-2xl bg-gray-900 px-8 pb-8 pt-80 sm:pt-48 lg:pt-80"
				>
					<img
						src="/fun-heros{example.image}"
						alt={example.alt}
						class="absolute block dark:hidden inset-0 -z-10 h-full w-full object-cover"
					/>

					<img
						src="/fun-heros{example.image_dark}"
						alt={example.alt}
						class="absolute hidden dark:block inset-0 -z-10 h-full w-full object-cover"
					/>
					<div
						class="absolute inset-0 -z-10 bg-gradient-to-t from-gray-900/70 via-gray-900/30"
					></div>
					<div
						class="absolute inset-0 -z-10 rounded-2xl ring-1 ring-inset ring-gray-900/10 dark:ring-white/5"
					></div>

					<h3 class="mt-3 text-lg font-semibold leading-6 text-white">
						<a href="/fun-heros{example.href}">
							<span class="absolute inset-0"></span>
							{example.name}
						</a>
					</h3>
				</article>
			{/each}
		</div>

		<div class="mx-auto max-w-2xl text-center pt-24 sm:pt-32">
			<h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl dark:text-gray-50">
				Basic
			</h2>
			<p class="mt-2 text-lg leading-8 text-gray-600 dark:text-gray-400">
				Basic hero examples. They're not 3D, but they're still cool
			</p>
		</div>
		<div
			class="mx-auto mt-16 grid max-w-2xl auto-rows-fr grid-cols-1 sm:grid-cols-2 gap-8 sm:mt-20 lg:mx-0 lg:max-w-none lg:grid-cols-3"
		>
			{#each basicExamples as example}
				<article
					class="relative isolate flex flex-col justify-end overflow-hidden rounded-2xl bg-gray-900 px-8 pb-8 pt-80 sm:pt-48 lg:pt-80"
				>
					<img
						src="/fun-heros{example.image}"
						alt={example.alt}
						class="absolute block dark:hidden inset-0 -z-10 h-full w-full object-cover"
					/>

					<img
						src="/fun-heros{example.image_dark}"
						alt={example.alt}
						class="absolute hidden dark:block inset-0 -z-10 h-full w-full object-cover"
					/>
					<div
						class="absolute inset-0 -z-10 bg-gradient-to-t from-gray-900/70 via-gray-900/30"
					></div>
					<div
						class="absolute inset-0 -z-10 rounded-2xl ring-1 ring-inset ring-gray-900/10 dark:ring-white/5"
					></div>

					<h3 class="mt-3 text-lg font-semibold leading-6 text-white">
						<a href="/fun-heros{example.href}">
							<span class="absolute inset-0"></span>
							{example.name}
						</a>
					</h3>
				</article>
			{/each}
		</div>

	</div>
</div>
