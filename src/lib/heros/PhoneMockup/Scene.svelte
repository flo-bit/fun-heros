<script lang="ts">
	import { T, useTask } from '@threlte/core';
	import { Environment, Float, HTML, OrbitControls, RoundedBoxGeometry } from '@threlte/extras';
	import { onMount } from 'svelte';
	import { spring } from 'svelte/motion';
	import { Group, Plane } from 'three';

	let x = spring(-0.3, { stiffness: 0.01, damping: 0.04 });
	let y = spring(0.1, { stiffness: 0.01, damping: 0.04 });

	// let x = spring(-0.3);
	// let y = spring(0.1);

	let timeout: number | undefined = undefined;

	const mouseMove = (event: MouseEvent) => {
		// get percentage of mouse position in viewport
		let mouseX =  event.clientX / window.innerWidth - 0.5;
		let mouseY = event.clientY / window.innerHeight - 0.5;
		$x = Math.min(0.5, Math.max(-0.5, mouseX));
		$y = Math.min(0.5, Math.max(-0.5, mouseY));

		stop();

		if (timeout) clearTimeout(timeout);

		timeout = setTimeout(() => {
			start();
		}, 2000);
	};

	const { stop, start } = useTask((dt) => {
		if(dt > 0.1) {
			console.log(dt);
			return;
		}
		// move in circle from current position
		// get current angle
		const angle = Math.atan2($y, $x);
		// get current distance
		const distance = Math.sqrt($x * $x + $y * $y);
		let move = dt;
		// move 0.01 radians per frame
		$x = Math.cos(angle + move) * distance;
		$y = Math.sin(angle + move) * distance;
	});

	export let iframeUrl: string;
	export let iframeTitle: string;

	export let phoneColor: string;
	export let phoneButtonColor: string;
</script>

<svelte:body on:mousemove={mouseMove} />

<T.PerspectiveCamera makeDefault position={[0, 0, 25]} fov={60} />

<T.DirectionalLight intensity={0.8} position.x={5} position.y={10} position.z={10} />
<T.AmbientLight intensity={1} />

<T.Group rotation={[$y * 0.6, $x * 0.6, 0]}>
	<T.Mesh>
		<RoundedBoxGeometry args={[12, 24, 1.2]} radius={0.6} smoothness={8} />
		<T.MeshStandardMaterial color={phoneColor} metalness={0.8} roughness={0.3} />
	</T.Mesh>

	<T.Mesh position={[-5.8, 8, 0]}>
		<RoundedBoxGeometry args={[0.7, 2, 0.5]} radius={0.2} />
		<T.MeshStandardMaterial color={phoneButtonColor} metalness={0.5} roughness={0.9} />
	</T.Mesh>

	<T.Mesh position={[-5.8, 5.5, 0]}>
		<RoundedBoxGeometry args={[0.7, 2, 0.5]} radius={0.2} />
		<T.MeshStandardMaterial color={phoneButtonColor} metalness={0.5} roughness={0.9} />
	</T.Mesh>

	<!-- <T.Mesh position.z={0.62}>
		<T.PlaneGeometry args={[12, 24]} />
		<T.MeshStandardMaterial
			color="#a1a1a1"
			metalness={1.0}
			roughness={0.5}
			depthWrite={false}
			transparent
			opacity={0.5}
		/>
	</T.Mesh> -->

	<HTML position.z={0.61} transform occlude pointerEvents="auto">
		<div class="w-[430px] h-[910px] rounded-xl text-xs font-semibold overflow-hidden relative bg-black">
			<div class="absolute inset-0 w-full h-full flex justify-center items-center text-white text-xl">Loading...</div>
			<iframe
				class="absolute inset-0 w-full h-full overflow-scroll"
				src={iframeUrl}
				title={iframeTitle}
			>
			</iframe>
			<div class="absolute w-full h-8 z-10 flex justify-center">
				<div class="rounded-b-2xl bg-black h-full w-28"></div>
			</div>
			<div class="absolute bottom-1 w-full h-2 z-10 flex justify-center">
				<div class="rounded-2xl bg-white/30 h-full w-28"></div>
			</div>
		</div>
	</HTML>
</T.Group>

<Environment files="/fun-heros/env.hdr" isBackground={false} />
