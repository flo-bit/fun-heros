<script lang="ts">
	import { T, useTask } from '@threlte/core';
	import { Environment, Instance, InstancedMesh, Sky, useTexture } from '@threlte/extras';
	import {
		MathUtils,
		MeshBasicMaterial,
		MeshLambertMaterial,
		MeshPhongMaterial,
		MeshStandardMaterial,
		PlaneGeometry
	} from 'three';

	let cloudTexture = useTexture('/fun-heros/materials/cloud.png');

	let geometry = new PlaneGeometry(1, 1);
	let material = new MeshStandardMaterial({
		transparent: true,
		opacity: 0.8,
		depthWrite: false,
		color: 0xc1c1c1
	});

	let positions: [number, number, number][] = [];


	const step = 1;

	for (let i = 0; i < 200; i++) {
		let x = MathUtils.randFloatSpread(1) * 60;
		let y = Math.pow(MathUtils.randFloatSpread(1), 2) * 30;
		let z = -i * step; 

		positions.push([x, y, z]);
	}

	let z = 0;
	let i = 0;

	useTask((dt) => {
		z -= dt * 10;

		if (positions[i][2] > z) {
			let last = positions[i > 0 ? i - 1 : positions.length - 1];
			positions[i][2] = last[2] - step;
			i++;
			if (i >= positions.length) {
				i = 0;
			}
		}
	});
</script>

<T.PerspectiveCamera makeDefault position={[0, 10, 0]} fov={45} far={200}>
	<Sky elevation={85} turbidity={0.65} rayleigh={0.17} mieCoefficient={0.013} />
</T.PerspectiveCamera>

{#await cloudTexture then value}
	<InstancedMesh>
		<T is={geometry} />
		<T is={material} map={value} />
		{#each positions as position}
			<Instance rotation.z={Math.random() * Math.PI * 2} position={[position[0], position[1], position[2] - z]} scale={[10, 10, 10]} />
		{/each}
	</InstancedMesh>
{/await}
