<script lang="ts">
	import { onMount } from 'svelte';

	onMount(() => {
		checkTheme();
		// Initial resize
		redrawOverlayCanvas();

		// Resize canvas on window resize
		window.addEventListener('resize', redrawOverlayCanvas);

		const script = import('./fluidtext.js');
		script.then((module) => {
			module.run();
		});
	});

	const overlayConfig = {
		text: 'Hello',
		fontWidth: '900',
		font: 'Arial',
		fontSize: 1 / 3 // percentage to canvas width
	};

	// overlay canvas

	function redrawOverlayCanvas() {
		let overlayCanvas = document.getElementById('maskCanvas') as HTMLCanvasElement;
		let container = document.getElementById('canvasContainer');
		if (!container || !overlayCanvas) return;

		overlayCanvas.width = container.offsetWidth;
		overlayCanvas.height = container.offsetHeight;

		let ctx = overlayCanvas.getContext('2d');
		if (!ctx) return;

		let dpr = window.devicePixelRatio || 1;
		let rect = overlayCanvas.getBoundingClientRect();

		overlayCanvas.width = rect.width * dpr;
		overlayCanvas.height = rect.height * dpr;
		ctx.scale(dpr, dpr);

		ctx.fillStyle = darkMode ? 'black' : 'white';
		ctx.fillRect(0, 0, overlayCanvas.width, overlayCanvas.height);

		let fontSize = Math.round(rect.width * overlayConfig.fontSize);
		ctx.font = overlayConfig.fontWidth + ' ' + fontSize + 'px ' + overlayConfig.font;

		ctx.strokeStyle = darkMode ? 'rgba(255, 255, 255, 0.1)' : 'rgba(0, 0, 0, 0.1)';
		ctx.lineWidth = 1;

		ctx.textBaseline = 'middle';
		ctx.textAlign = 'center';

		ctx.strokeText(overlayConfig.text, rect.width / 2, rect.height / 2);

		ctx.globalCompositeOperation = 'destination-out';
		ctx.fillText(overlayConfig.text, rect.width / 2, rect.height / 2);
	}

	let darkMode = false;
	// watch theme
	const checkTheme = () => {
		const root = document.getElementsByTagName('html')[0];
		if (root.classList.contains('dark')) {
			darkMode = true;
		} else {
			darkMode = false;
		}

		redrawOverlayCanvas();
	};
</script>

<svelte:body on:click={checkTheme} />

<div id="canvasContainer" class="w-screen h-screen relative">
	<canvas class="absolute h-full w-full"></canvas>
	<canvas id="maskCanvas" class="absolute h-full w-full"> </canvas>

	<div class="absolute bottom-4 w-full flex items-center justify-center">
		<div class="text-3xl font-thin text-white">there</div>
	</div>
</div>
