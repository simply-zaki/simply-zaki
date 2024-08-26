<script>
	import { onMount } from 'svelte';
	import Title from '$lib/Title.svelte';
	import * as THREE from 'three';
	import { OBJLoader } from 'three/examples/jsm/loaders/OBJLoader.js';
	import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
//yes
	let canvas;
	function threeJsIcon() {
		const scene = new THREE.Scene();
		const camera = new THREE.PerspectiveCamera(75, 1, 0.1, 1000);
		const renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true, alpha: true });

		if (window.innerWidth <= 450) {
			renderer.setSize(50, 50);
		} else if (window.innerWidth <= 620) {
			renderer.setSize(70, 70);
		} else {
			renderer.setSize(100, 100);
		}

		renderer.setClearColor(new THREE.Color(0x000000), 0);

		camera.position.z = 1.2;

		// Lighting
		const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
		scene.add(ambientLight);

		const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
		directionalLight.position.set(1, 1, 1).normalize();
		scene.add(directionalLight);

		// Load the OBJ model
		const loader = new OBJLoader();
		let object;
		loader.load('/threejs.obj', (obj) => {
			object = obj;

			// Apply white material to the model
			object.traverse((node) => {
				if (node.isMesh) {
					node.material = new THREE.MeshBasicMaterial({ color: 0xffffff });
				}
			});

			// Scale the model to fit the canvas
			const box = new THREE.Box3().setFromObject(object);
			const size = new THREE.Vector3();
			box.getSize(size);

			const maxDim = Math.max(size.x, size.y, size.z);
			const scaleFactor = 1 / maxDim;

			object.scale.set(scaleFactor, scaleFactor, scaleFactor);

			scene.add(object);

			// Default animation setup
			let up = true;
			const animate = () => {
				requestAnimationFrame(animate);

				// Floating animation like Minecraft item
				const time = Date.now() * 0.002;
				const yOffset = Math.sin(time) * 0.002;
				object.position.y += up ? yOffset : -yOffset;
				if (object.position.y > 0.01) up = false;
				if (object.position.y < -0.01) up = true;
				object.rotation.y += 0.01;

				renderer.render(scene, camera);
			};

			animate();
		});

		// Orbit controls for user interaction (rotate, zoom)
		const controls = new OrbitControls(camera, renderer.domElement);
		controls.enableDamping = true;
		controls.dampingFactor = 0.05;
		controls.screenSpacePanning = false;
		controls.minDistance = 1;
		controls.maxDistance = 10;
		controls.maxPolarAngle = Math.PI / 2;

		const render = () => {
			requestAnimationFrame(render);
			controls.update();
			renderer.render(scene, camera);
		};

		render();
	}
	onMount(() => {
		threeJsIcon();
		window.addEventListener('resize', threeJsIcon, false);
	});
</script>

<Title id="technologies" text="Technologies" />
<section>
	<div class="tools">
		<img src="/github.svg" alt="icon" />
		<img src="/notion.svg" alt="icon" />
		<img src="/paintdotnet.ico" alt="icon" />
		<img src="/vscode.svg" alt="icon" />
		<img src="/vercel.svg" title="triangle company" alt="icon" />
		<img src="/figma.svg" alt="icon" />
		<img src="/blender.svg" alt="icon" />
		<img src="/docker.svg" alt="icon" />
		<img src="/ai.svg" alt="icon" />
	</div>

	<div class="languages">
		<img src="/svelte.svg" alt="" />
		<img src="/sveltekit.png" alt="" />
		<img src="/mongodb.svg" alt="" />
		<img src="/python.svg" alt="" />
		<img src="/flask.svg" alt="" />
		<img src="/mysql.svg" alt="" />
		<img src="/php.svg" alt="" />
		<img src="/jquery.svg" alt="" />
		<!-- The canvas where the 3D model will be rendered -->
		<canvas bind:this={canvas} width="100" height="100"></canvas>
	</div>
</section>

<style>
	section {
		position: relative;
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		color: white;
		margin-bottom: 16px;
		width: 90vw;
	}
	div {
		display: grid;
		grid-template-columns: 100px 100px 100px 100px 100px;
		grid-template-rows: 100px 100px;
		border: 1px solid var(--border);
		border-radius: 16px;
		width: 45%;
		padding: 32px;
		align-items: center;
		justify-items: center;
		justify-content: center;
	}
	img {
		height: 64px;
	}
	canvas {
		cursor: grab;
	}
	@media (max-width: 1250px) {
		div {
			grid-template-columns: 100px 100px 100px 100px;
			grid-template-rows: 100px 100px 100px;
		}
	}
	@media (max-width: 1000px) {
		div {
			grid-template-columns: 100px 100px 100px;
			grid-template-rows: 100px 100px 100px 100px;
		}
	}
	@media (max-width: 768px) {
		div {
			grid-template-columns: 100px 100px;
			grid-template-rows: 100px 100px 100px 100px 100px;
		}
	}
	@media (max-width: 620px) {
		img {
			height: 48px;
		}
	}
	@media (max-width: 450px) {
		img {
			height: 32px;
		}
		div {
			grid-template-columns: 32px 32px 32px;
			grid-template-rows: 32px 32px 32px 32px;
			padding: 16px;
			gap: 12px;
		}
	}
</style>
