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
			text: "Did you know that cats have an extra organ that allows them to taste scents on the air? It's called the Jacobson's organ and it's located on the roof of their mouths. This unique sensory tool helps cats analyze smells with the flehmen response, often seen as a \"grimacing\" expression. This ability enhances their hunting and social skills.",
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
	let hoveredIndex = -1;

	function animate() {
		animating = true;
		setTimeout(() => {
			animating = false;
		}, 1200); // Increasedtotal animation duration to 1.2 seconds
	}

	function changeProject(index) {
		if (currentIndex !== index) {
			animate();
			setTimeout(() => {
				currentIndex = index;
			}, 600); // Increased delay to 600ms (half of the total animation time)
		}
	}
</script>

<Title id="projects" text="Projects" />

<section class:animating>
	<img src={websites[currentIndex].src} alt={websites[currentIndex].name} />
	<span class="project-info">
		<h1>
			<a href={websites[currentIndex].link} >
				{websites[currentIndex].name}
			</a>
			<svg class="link-icon" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
				<path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path>
				<path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path>
			</svg>
		</h1>
		<p>{websites[currentIndex].text}</p>
	</span>
</section>

<div class="controls">
	{#each websites as _, index}
		<div class="dot" class:active={index === currentIndex} on:click={() => changeProject(index)}>
			{#if hoveredIndex === index}
				<span class="dot-preview">{websites[index].name}</span>
			{/if}
		</div>
		{/each}
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
	.controls {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 158px;
		margin-top: 16px;
		margin-bottom: 100px;
	}
	.project-info {
		display: flex;
		text-align: start;
		flex-direction: column;
		padding: 0 16px 0 16px;
	}
	.animating {
		animation:
			fadeOut 0.6s ease-out,
			fadeIn 0.6s ease-in 0.6s;
	}
	.link-icon {
		vertical-align: middle;
		margin-left: 4px;
	}
	.controls {
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 20px;
	}
	.dot {
		width: 12px;
		height: 12px;
		border-radius: 50%;
		background-color: #555;
		margin: 0 8px;
		cursor: pointer;
		transition: all 0.3s ease;
		position: relative;
	}
	.dot.active {
		background-color: white;
		transform: scale(1.2);
	}
	.dot:hover {
		transform: scale(1.3);
	}
	.dot-preview {
		position: absolute;
		bottom: 20px;
		left: 50%;
		transform: translateX(-50%);
		background-color: rgba(0, 0, 0, 0.7);
		color: white;
		padding: 4px 8px;
		border-radius: 4px;
		font-size: 12px;
		white-space: nowrap;
	}
	.link-icon {
		vertical-align: middle;
		margin-left: 4px;
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
	@keyframes fadeInOut {
		0%,
		100% {
			opacity: 1;
		}
		50% {
			opacity: 0;
		}
	}
	@media (max-width: 970px) {
		section {
			flex-direction: column;
		}
		section h1 {
			margin: 16px 0 16px 0;
		}
		.project-info {
			align-items: center;
			text-align: center;
		}
	}
</style>
