<script>
	import Title from '$lib/Title.svelte';
	let websites = [
		{
			src: '/simply calisthenics.png',
			text: 'A minimalist fitness web app dedicated to calisthenics. It offers a comprehensive exercise library with detailed information and allows you to create, customize, and track your workouts. Designed to support your calisthenics journey, this app provides all the essential tools you need to progress and achieve your fitness goals.',
			link: 'https://simply-calisthenics.vercel.app/',
			name: 'Simply calisthenics'
		},
		{
			src: '/cat.jpg',
			text: 'Did you know that cats have an extra organ that allows them to taste scents on the air? It\'s called the Jacobson\'s organ and it\'s located on the roof of their mouths. This unique sensory tool helps cats analyze smells with the flehmen response, often seen as a "grimacing" expression. This ability enhances their hunting and social skills.',
			link: '#',
			name: 'Cat Fact 1'
		},
		{
			src: '/cat2.jpg',
			text: 'Cats have night vision about 6 times better than humans, thanks to a reflective layer called tapetum lucidum behind their retina. This, combined with their ability to dilate their pupils widely, gives cats their superior night vision and "glowing eyes" in the dark.',
			link: '#',
			name: 'Cat Fact 2'
		}
	];

	let currentIndex = 0;
	let animating = false;

	function animate() {
		animating = true;
		setTimeout(() => {
			animating = false;
		}, 1200); // Increased total animation duration to 1.2 seconds
	}

	function next() {
		if (currentIndex < websites.length - 1 && !animating) {
			animate();
			setTimeout(() => {
				currentIndex += 1;
			}, 600); // Increased delay to 600ms (half of the total animation time)
		}
	}

	function prev() {
		if (currentIndex > 0 && !animating) {
			animate();
			setTimeout(() => {
				currentIndex -= 1;
			}, 600); // Increased delay to 600ms (half of the total animation time)
		}
	}
</script>

<Title id="projects" text="Projects" />

<section class:animating>
	<img src={websites[currentIndex].src} alt={websites[currentIndex].src} />
	<span class="project-info">
		<h1><a href={websites[currentIndex].link}>{websites[currentIndex].name}</a></h1>
		<p>{websites[currentIndex].text}</p>
	</span>
</section>

<div class="controls">
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<svg on:click={prev} tabindex="0" role="button" aria-label="Previous Project" class="arrow left-arrow" xmlns="http://www.w3.org/2000/svg" width="24" height="48" viewBox="0 0 12 24"><path fill="currentColor" d="M1.843 12.711L7.5 18.368l1.414-1.414l-4.95-4.95l4.95-4.95L7.5 5.64 1.843 11.297a1 1 0 0 0 0 1.414" /></svg>
	<span class="controls_number">{currentIndex + 1} / {websites.length}</span>
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<svg on:click={next} tabindex="0" role="button" aria-label="Next Project" class="arrow right-arrow" xmlns="http://www.w3.org/2000/svg" width="24" height="48" viewBox="0 0 12 24"><path fill="currentColor" d="M10.157 12.711L4.5 18.368l-1.414-1.414l4.95-4.95l-4.95-4.95L4.5 5.64l5.657 5.657a1 1 0 0 1 0 1.414" /></svg>
</div>

<style>
	section {
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		flex-direction: row;
		padding: 32px;
		border: 1px solid var(--border);
		border-radius: 16px;
		color: white;
		width: 70vw;
	}
	section img {
		border: 1px solid var(--border);
		border-radius: 16px;
		height: 128px;
	}
	.controls_number {
		font-size: 24px;
		color: white;
	}
	.controls {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 158px;
		margin-top: 16px;
		margin-bottom: 100px;
	}
	.arrow {
		height: 48px;
		width: 48px;
		cursor: pointer;
		color: white;
		transition:
			color 0.3s,
			transform 0.2s;
		outline: none;
	}
	.arrow:hover path {
		fill: #d3d3d3; /* Light gray on hover */
	}
	.arrow:active {
		transform: scale(0.9);
		fill: #a9a9a9; /* Darker gray on active */
	}
	.project-info {
		display: flex;
		text-align: start;
		flex-direction: column;
		padding: 0 16px 0 16px;
	}
	@keyframes fadeOut {
		from {
			opacity: 1;
		}
		to {
			opacity: 0;
		}
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	.animating {
		animation:
			fadeOut 0.6s ease-out,
			fadeIn 0.6s ease-in 0.6s;
	}
	@media (max-width: 970px) {
		section{
			flex-direction: column;
		}
		section h1 {
			margin: 16px 0 16px 0;
		}
		.project-info{
			align-items: center;
			text-align: center;
		}
	}
</style>
