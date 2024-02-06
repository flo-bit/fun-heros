<script lang="ts">
	import { T } from '@threlte/core';
	import { Environment, OrbitControls } from '@threlte/extras';

	import Text3D from '$lib/components/Text3D/Text3D.svelte';

	let cameraDistance = 20;
	const resize = () => {
		cameraDistance = window.innerWidth < 768 ? 60 : 30;
		console.log(cameraDistance);
	};

	resize();
</script>

<svelte:body on:resize={resize} />

<Text3D
	font={'/fun-heros/fonts/Inter-semibold.blob'}
	text={`hello there`}
	size={5}
	height={1}
	bevelEnabled={true}
	bevelThickness={0.1}
	bevelSize={0.1}
	bevelSegments={5}
	position.x={-17}
>
	<T.MeshStandardMaterial color="313131" metalness={0.7} roughness={0.2} />
</Text3D>

<T.PerspectiveCamera
	makeDefault
	position.y={0}
	position.z={cameraDistance}
	fov={75}
	on:create={({ ref }) => {
		ref.lookAt(0, 0, 0);
	}}
>
	<OrbitControls enableDamping enablePan={false} enableZoom={false} />
</T.PerspectiveCamera>

<Environment files="/fun-heros/envs/env.hdr" />
