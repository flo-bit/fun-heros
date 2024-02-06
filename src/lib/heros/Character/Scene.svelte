<script lang="ts">
	import { T } from '@threlte/core';
	import { Environment } from '@threlte/extras';
	import { onMount } from 'svelte';
	import Michelle from './Michelle.svelte';
</script>


<T.PerspectiveCamera makeDefault position={[0, 0, 25]} fov={60} />

<T.DirectionalLight intensity={0.8} position.x={5} position.y={10} position.z={10} />
<T.AmbientLight intensity={2} />

<Michelle rotation.y={-0.2}/>

<Environment files="/fun-heros/env.hdr" isBackground={false} />
