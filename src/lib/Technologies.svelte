<script>
	import { onMount } from 'svelte';
	import Title from '$lib/Title.svelte';
	import * as THREE from 'three';
	import { OBJLoader } from 'three/examples/jsm/loaders/OBJLoader.js';
	import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
//test
	let canvas;

	function threeJsIcon() {
		const scene = new THREE.Scene();
		const camera = new THREE.PerspectiveCamera(75, 1, 0.1, 1000);
		const renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true, alpha: true });
//pls
		// Adjusting size for different screen widths
		if (window.innerWidth <= 585) {
			renderer.setSize(64, 60); // For 360px width screens
		} else {
			renderer.setSize(64, 64);
		}

		renderer.setClearColor(new THREE.Color(0x000000), 0);
		camera.position.z = 1.2;

		// Lighting setup
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

		return () => {
			window.removeEventListener('resize', threeJsIcon);
		};
	});
</script>

<Title id="technologies" text="Technologies" />
<section>
	<!-- Frontend Technologies -->
	<div class="tech-item">
		<img src="/svelte.svg" alt="Svelte" />
		<span class="tech-name">Svelte</span>
	</div>
	<div class="tech-item">
		<img src="/sveltekit.png" alt="SvelteKit" />
		<span class="tech-name">SvelteKit</span>
	</div>
	<!-- The canvas where the 3D model of three.js will be rendered -->
	<div class="tech-item">
		<canvas bind:this={canvas} width="100" height="100"></canvas>
		<span class="tech-name">Three.js</span>
	</div>

	<!-- Backend Technologies -->
	<div class="tech-item">
		<img src="/flask.svg" alt="Flask" />
		<span class="tech-name">Flask</span>
	</div>
	<div class="tech-item">
		<img src="/python.svg" alt="Python" />
		<span class="tech-name">Python</span>
	</div>
	<div class="tech-item">
		<img src="/mongodb.svg" alt="MongoDB" />
		<span class="tech-name">MongoDB</span>
	</div>
	<div class="tech-item">
		<img src="/mysql.svg" alt="MySQL" />
		<span class="tech-name">MySQL</span>
	</div>
	<!-- Tools -->
	<div class="tech-item">
		<img src="/docker.svg" alt="Docker" />
		<span class="tech-name">Docker</span>
	</div>
	<div class="tech-item">
		<img src="/blender.svg" alt="Blender" />
		<span class="tech-name">Blender</span>
	</div>
	
</section>

<style>
	section {
		position: relative;
		display: flex;
		flex-wrap: wrap; 
		align-items: center; 
		justify-content: center;
		margin-bottom: 135px;
		border: 1px solid var(--border);
		border-radius: 16px;
		width: 70vw;
		padding: 32px;
		gap: 32px;
	}

	.tech-item {
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: center;
		transition: transform 0.3s ease;
	}

	.tech-item:hover {
		transform: translateY(-5px);
	}

	img, canvas {
		height: 64px;
		width: 64px;
		object-fit: contain;
	}

	.tech-name {
		opacity: 0;
		transition: opacity 0.3s ease;
		position: absolute;
		bottom: -20px;
		font-size: 12px;
		color: var(--text-color);
	}

	.tech-item:hover .tech-name {
		opacity: 1;
	}

	@media (max-width: 585px) {
		img, canvas {
			height: 48px;
			width: 48px;
		}
	}
</style>
