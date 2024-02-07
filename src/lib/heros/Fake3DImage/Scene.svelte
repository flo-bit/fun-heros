<script lang="ts">
	import { T, useTask } from '@threlte/core';
	import { useTexture, Align } from '@threlte/extras';

	import { Vector2, ShaderMaterial, PlaneGeometry, LinearEncoding } from 'three';

	type DepthImage = {
		image: string;
		depth: string;
	};

	export let image: DepthImage;

	const map = useTexture(image.image, {
		transform: (texture) => {
			texture.encoding = LinearEncoding;
			return texture;
		}
	});
	const depthMap = useTexture(image.depth, {
		transform: (texture) => {
			//texture.encoding = LinearEncoding;
			return texture;
		}
	});

	const rotation = new Vector2(0.5, 0.5);

	const uniforms = {
		uTexture: { type: 't', value: map },
		depthMap: { type: 't', value: depthMap }
	};
	const material = new ShaderMaterial({
		uniforms: uniforms,
		vertexShader: `
varying vec2 vUv;
uniform sampler2D depthMap;

void main() {
    vUv = uv;
    // move z position based on the depth map
    float depth = texture2D(depthMap, vUv).r;
    vec3 newPosition = position + vec3(0.0, 0.0, depth * 4.5);
    gl_Position = projectionMatrix * modelViewMatrix * vec4(newPosition, 1.0);
}`,
		fragmentShader: `
uniform sampler2D uTexture;
// uniform sampler2D depthMap;
// uniform vec2 mouse;
varying vec2 vUv;

void main() {
	// float shift = texture2D(depthMap, vUv).r;
	// vec2 uv = vUv + mouse * shift * 0.03;

    gl_FragColor = texture2D(uTexture, vUv);
}`
	});

	const geometry = new PlaneGeometry(7, 7, 500, 500);

	export let time = 0;
	useTask((dt) => {
		time += dt * 0.4;
		rotation.x = Math.sin(time) * 0.5;
		rotation.y = Math.cos(time) * 0.5;
	});
</script>

<T.PerspectiveCamera
	makeDefault
	position={[0, 0, 7]}
	on:create={({ ref }) => {
		ref.lookAt(0, 0, 0);
	}}
	fov={40}
></T.PerspectiveCamera>

{#await map then mapValue}
	{#await depthMap then depthValue}
		<Align>
			<T.Mesh
				rotation.x={rotation.y * 0.25}
				rotation.y={rotation.x * 0.25}
				scale.x={mapValue.image.width / mapValue.image.height}
			>
				<T is={geometry} />
				<T
					is={material}
					uniforms={{
						depthMap: { value: depthValue },
						uTexture: { value: mapValue },
						mouse: { value: rotation }
					}}
				/>
			</T.Mesh>
		</Align>
	{/await}
{/await}
