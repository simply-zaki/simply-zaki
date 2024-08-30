<script>
	import Title from '$lib/Title.svelte';
	let websites = [
		{
			src: '/simply calisthenics.png',
			text: '1A minimalist fitness web app dedicated to calisthenics. It offers a comprehensive exercise library with detailed information and allows you to create, customize, and track your workouts. Designed to support your calisthenics journey, this app provides all the essential tools you need to progress and achieve your fitness goals',
			link: 'https://simply-calisthenics.vercel.app/',
			name: "Simply calisthenics"
		},
		{
			src: '/simply calisthenics.png',
			text: '2A minimalist fitness web app dedicated to calisthenics. It offers a comprehensive exercise library with detailed information and allows you to create, customize, and track your workouts. Designed to support your calisthenics journey, this app provides all the essential tools you need to progress and achieve your fitness goals',
			link: 'https://simply-calisthenics.vercel.app/',
			name: "Simply calisthenics"
		},
		{
			src: '/simply calisthenics.png',
			text: '3A minimalist fitness web app dedicated to calisthenics. It offers a comprehensive exercise library with detailed information and allows you to create, customize, and track your workouts. Designed to support your calisthenics journey, this app provides all the essential tools you need to progress and achieve your fitness goals',
			link: 'https://simply-calisthenics.vercel.app/',
			name: "Simply calisthenics"
		},
	];

	let currentIndex = 0;

	function next() {
		if (currentIndex < websites.length - 1) {
			currentIndex += 1;
		}
	}

	function prev() {
		if (currentIndex > 0) {
			currentIndex -= 1;
		}
	}
</script>

<Title id="projects" text="Projects" />

<section>
	<img src={websites[currentIndex].src} alt={websites[currentIndex].src} />

	<h1><a href={websites[currentIndex].link}>{websites[currentIndex].name}</a></h1>
	<p>{websites[currentIndex].text}</p>
	<div class="controls">
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<svg on:click={prev} tabindex="0" role="button" aria-label="Previous Project" class="arrow left-arrow" xmlns="http://www.w3.org/2000/svg" width="24" height="48" viewBox="0 0 12 24"><path fill="currentColor" d="M1.843 12.711L7.5 18.368l1.414-1.414l-4.95-4.95l4.95-4.95L7.5 5.64 1.843 11.297a1 1 0 0 0 0 1.414" /></svg>
	<span class="controls_number">{currentIndex + 1} / {websites.length}</span>
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<svg on:click={next} tabindex="0" role="button" aria-label="Next Project" class="arrow right-arrow" xmlns="http://www.w3.org/2000/svg" width="24" height="48" viewBox="0 0 12 24"><path fill="currentColor" d="M10.157 12.711L4.5 18.368l-1.414-1.414l4.95-4.95l-4.95-4.95L4.5 5.64l5.657 5.657a1 1 0 0 1 0 1.414" /></svg>
</div>
</section>


<style>
	section {
		display: flex;
		align-items: center;
		justify-content: space-between;
		flex-direction: column;
		padding: 32px;
		border: 1px solid var(--border);
		border-radius: 16px;
		color: white;
		background-color: black;
		text-align: center;
		margin-bottom: 100px;
	}
	section img {
		border: 1px solid var(--border);
		border-radius: 16px;
		height: 192px;
	}
	section h1 {
		margin-bottom: 16px;
		margin-top: 16px;
	}
	section p {
		font-size: 18px;
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
</style>
