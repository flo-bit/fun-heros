<script lang="ts">
	import { T } from '@threlte/core';
	import { Environment, Float, OrbitControls } from '@threlte/extras';
	import { onMount } from 'svelte';
	import Diamond from './Diamond.svelte';
</script>

<T.PerspectiveCamera makeDefault position={[0, 10, 25]} fov={60}>
	<OrbitControls enableDamping enablePan={false} autoRotate enableZoom={false} />
</T.PerspectiveCamera>

<T.DirectionalLight intensity={0.8} position.x={5} position.y={10} position.z={10} />
<T.AmbientLight intensity={2} />

<Float floatIntensity={5} rotationIntensity={0.3} rotationSpeed={[0, 0, 0]}>
	<Diamond scale={8} />
</Float>
