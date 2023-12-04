<script>
	import { T, useFrame } from '@threlte/core';
	import { OrbitControls, interactivity } from '@threlte/extras';
	import { spring } from 'svelte/motion';
	import { useGltf, useGltfAnimations } from '@threlte/extras';

	import PR from './Puerto Rico.svelte';
	import Water from './water.svelte';
	import { Group } from 'three';
	// export const { actions, mixer } = useGltfAnimations(gltf, ref)
	import { Sky } from '@threlte/extras';
	// import CursorLine from './CursorLine.svelte';

	interactivity();
	let cursorPosition = { x: 0, z: 0 };
	let colors = ['#fc6435', '#ff541f', '#f53c02', '#261f9a', '#1e168d'];
	const scale = spring(1);
	let rotation = 0;
	useFrame((state, delta) => {
		rotation += delta;
	});

	let group = new Group();
</script>

<!-- {#each colors as color, i}
	<CursorLine
		{color}
		{cursorPosition}
		position.y={5 - i}
		stiffness={0.02 * i + 0.02}
		damping={0.25 - 0.04 * i}
		width={15 + i * 10}
	/>
{/each} -->

<Sky elevation={0.5} />
<T.PerspectiveCamera
	makeDefault
	position={[0, 10, 5]}
	on:create={({ ref }) => {
		ref.lookAt(0, 0, 0);
	}}
	fov={20}
>
	<!-- autoRotate -->
	<OrbitControls />
</T.PerspectiveCamera>
<!-- <T ref={group}> -->
<PR />
<Water />
<T.DirectionalLight position={[0, 10, 10]} castShadow />
<!-- <T.Mesh
  rotation.y={rotation}
  position.y={1.02}
  scale={$scale}
  on:pointerenter={() => scale.set(1.5)}
  on:pointerleave={() => scale.set(1)}
  castShadow
>
  <T.BoxGeometry args={[1, 2, 1]} />
  <T.MeshStandardMaterial color="hotpink" />
</T.Mesh> -->

<T.Mesh rotation.x={-Math.PI / 2} receiveShadow>
	<T.CircleGeometry args={[2, 20]} />
	<T.MeshStandardMaterial color="blue" />
</T.Mesh>
<!-- </T> -->
