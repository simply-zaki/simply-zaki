<script>
	import { onMount } from 'svelte';
	import Title from '$lib/Title.svelte';
	import * as THREE from 'three';
	import { OBJLoader } from 'three/examples/jsm/loaders/OBJLoader.js';
	import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

	let technologie = 'Svelte';
	let des = 'Svelte is my favorite frontend framework, very fast to make powerful web applications.';
	let icon = '/svelte.svg';

	let canvas;
	let other_canvas;
	let showcase_img;

	function threeJsIcon(the_canvas) {
		const scene = new THREE.Scene();
		const camera = new THREE.PerspectiveCamera(75, 1, 0.1, 1000);
		const renderer = new THREE.WebGLRenderer({ canvas: the_canvas, antialias: true, alpha: true });

		// Check if the current canvas is "other_canvas"
		if (the_canvas === other_canvas) {
			if (window.innerWidth <= 786) {
				renderer.setSize(64, 64);
			} else {
				renderer.setSize(96, 96);
			}
		} else {
			if (window.innerWidth <= 360) {
				renderer.setSize(40, 40);
			} else if (window.innerWidth <= 480) {
				renderer.setSize(48, 48);
			} else if (window.innerWidth <= 1124) {
				renderer.setSize(48, 48);
			} else {
				renderer.setSize(70, 70);
			}
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

	// Function to handle image click and update variables
	function handleClick(event) {
		const img = event.target;

		if (img.tagName === 'CANVAS') {
			other_canvas.style.display = 'unset';
			showcase_img.style.display = 'none';
			threeJsIcon(other_canvas);
			technologie = img.dataset.name;
			des = img.dataset.description;

			// Remove outline from all images and canvases
			const images = document.querySelectorAll('.tools img');
			images.forEach((image) => (image.style.outlineColor = 'transparent'));

			const canvases = document.querySelectorAll('.tools canvas');
			canvases.forEach((canvas) => (canvas.style.outlineColor = 'transparent'));

			// Add outline color to the clicked canvas
			img.style.outlineColor = 'white';
		} else {
			showcase_img.style.display = 'unset';
			other_canvas.style.display = 'none';
			technologie = img.dataset.name;
			des = img.dataset.description;
			icon = img.src;

			// Remove outline from all images and canvases
			const images = document.querySelectorAll('.tools img');
			images.forEach((image) => (image.style.outlineColor = 'transparent'));

			const canvases = document.querySelectorAll('.tools canvas');
			canvases.forEach((canvas) => (canvas.style.outlineColor = 'transparent'));

			// Add outline color to the clicked image
			img.style.outlineColor = 'white';
		}
	}

	onMount(() => {
		threeJsIcon(canvas);

		// Corrected event listener
		window.addEventListener('resize', () => threeJsIcon(canvas));

		// Cleanup the event listener when the component is destroyed
	});
</script>

<Title id="technologies" text="Technologies" />
<section>
	<span>
		<h1>{technologie}</h1>
		<img bind:this={showcase_img} class="info_img" src={icon} alt={technologie} />
		<canvas class="info_img" style="display: none;" bind:this={other_canvas}></canvas>
		<p>{des}</p>
	</span>

	<div class="tools">
		<!-- Each image has a data-name and data-description attribute -->
		<img style="outline: 3px solid white;" src="/svelte.svg" alt="Svelte" data-name="Svelte" data-description="Svelte is my favorite frontend framework, very fast to make powerful web applications." on:click={handleClick} />
		<img src="/sveltekit.png" alt="SvelteKit" data-name="SvelteKit" data-description="SvelteKit is used for authentication, routing, and other essential web features." on:click={handleClick} />
		<canvas alt="Three.js" data-name="Three.js" data-description="Three.js is used to add 3D elements, like this icon to websites." on:click={handleClick} bind:this={canvas}></canvas>
		<img src="/jquery.svg" alt="jQuery" data-name="jQuery" data-description="jQuery was the first tool I used when starting web development; I still have skills with it." on:click={handleClick} />
		
		<img src="/github.svg" alt="GitHub" data-name="GitHub" data-description="GitHub is essential for saving projects securely and deploying websites." on:click={handleClick} />
		<img src="/notion.svg" alt="Notion" data-name="Notion" data-description="Notion helps me keep track of projects and tasks efficiently." on:click={handleClick} />
		<img src="/paintdotnet.ico" alt="Paint.NET" data-name="Paint.NET" data-description="Paint.NET is my go-to tool for editing images." on:click={handleClick} />
		<img src="/vscode.svg" alt="VS Code" data-name="VS Code" data-description="VS Code is the only code editor I use because it makes my work faster." on:click={handleClick} />
		<img src="/vercel.svg" alt="Vercel" data-name="Vercel" data-description="Vercel makes deploying websites easy, fast, and feature-rich." on:click={handleClick} />
		<img src="/figma.svg" alt="Figma" data-name="Figma" data-description="Figma is essential for creating and editing SVGs and other UI/UX designs." on:click={handleClick} />
		<img src="/blender.svg" alt="Blender" data-name="Blender" data-description="Blender is used for creating or editing 3D objects; I have experience from my game development days." on:click={handleClick} />
		<img src="/docker.svg" alt="Docker" data-name="Docker" data-description="Docker helps me run local servers efficiently." on:click={handleClick} />
		<img src="/ai.svg" alt="AI" data-name="AI" data-description="AI is my go-to tool for speeding up work significantly." on:click={handleClick} />
		
		<img src="/mongodb.svg" alt="MongoDB" data-name="MongoDB" data-description="MongoDB is my database of choice because it's easy to use and flexible." on:click={handleClick} />
		<img src="/python.svg" alt="Python" data-name="Python" data-description="Python is my preferred language for backend APIs, thanks to its simplicity and extensive libraries." on:click={handleClick} />
		<img src="/flask.svg" alt="Flask" data-name="Flask" data-description="Flask is the framework I use for Python backend development due to its flexibility and minimalism." on:click={handleClick} />
		<img src="/mysql.svg" alt="MySQL" data-name="MySQL" data-description="MySQL was my first database system; I still have skills with it." on:click={handleClick} />
		<img src="/php.svg" alt="PHP" data-name="PHP" data-description="PHP was one of the first scripting languages I used for web development, and I still maintain my skills with it." on:click={handleClick} />
		
	</div>
</section>

<style>
	/* Default styles */
	section {
		position: relative;
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		color: white;
		margin-bottom: 64px;
		width: 90vw;
		height: 440px;
	}
	div {
		display: grid;
		grid-template-columns: repeat(5, 70px);
		grid-template-rows: repeat(4, 70px);
		border: 1px solid var(--border);
		border-radius: 16px;
		width: 45%;
		padding: 32px;
		align-items: center;
		justify-items: center;
		justify-content: center;
		align-content: center;
		height: 100%;
		gap: 16px;
	}
	span {
		display: flex;
		align-items: center;
		flex-direction: column;
		justify-content: center;
		padding: 24px;
		border: 1px solid var(--border);
		border-radius: 16px;
		width: 45%;
		font-size: 20px;
		text-align: center;
		height: 100%;
	}
	span h1 {
		margin-bottom: 16px;
	}
	.info_img {
		height: 96px;
		width: 96px;
		margin-bottom: 16px;
	}
	img {
		height: 70px;
		width: 70px;
		padding: 4px;
		border-radius: 16px;
		cursor: pointer;
		outline: 3px solid transparent;
		transition: outline-color 0.2s ease-in;
	}
	canvas {
		cursor: grab;
		border-radius: 16px;
		outline: 3px solid transparent;
		transition: outline-color 0.2s ease-in;
	}
	span p {
		display: flex;
		align-items: center;
		height: 80px;
	}
	/* Styles for screens up to 1124px wide */
	@media (max-width: 1124px) {
		div {
			grid-template-columns: repeat(5, 48px);
			grid-template-rows: repeat(4, 48px);
			height: 80%;
		}
		img {
			height: 48px;
			width: 48px;
		}
		span {
			height: 80%;
		}
		section {
			margin-bottom: 32px;
		}
	}

	/* Styles for screens up to 768px wide */
	@media (max-width: 768px) {
		section {
			flex-direction: column;
			align-items: center;
			width: 90vw;
			margin-bottom: 256px;
		}
		span {
			width: 90vw;
			margin-bottom: 16px;
			font-size: 16px;
		}
		div {
			width: fit-content;
		}
		.info_img {
			height: 64px;
			width: 64px;
			margin-bottom: 8px;
		}
		span h1 {
			margin-bottom: 8px;
		}
	}

	/* Styles for screens up to 480px wide */
	@media (max-width: 480px) {
		div {
			grid-template-columns: repeat(4, 48px);
			grid-template-rows: repeat(4, 48px);
		}
		span {
			font-size: 16px;
			padding: 16px;
		}
		img {
			height: 40px;
			width: 40px;
		}
	}

	/* Styles for screens up to 360px wide */
	@media (max-width: 360px) {
		div {
			grid-template-columns: repeat(4, 40px);
			grid-template-rows: repeat(4, 40px);
		}
		span {
			font-size: 12px;
			padding: 12px;
		}
		img {
			height: 32px;
			width: 32px;
		}
	}
</style>
