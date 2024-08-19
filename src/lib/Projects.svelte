<script>
	import Title from '$lib/Title.svelte';
	let websites = [
		{
			src: '/project.png',
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Fuga sequi quidem consectetur earum corporis ipsa ducimus facilis quis! Molestiae, ex harum? Ullam ad illum eligendi non distinctio? A, ad nobis.',
			link: 'https://cataas.com/cat'
		},
		{
			src: '/cat.svg',
			text: 'Lorem ipsum dolor sit amet conseet consectetur adipisicing elit.ctetur adipet consectetur adipisicing elit.isicing elit. Fuga sequi quidem consectetur earum corporis ipsa ducimus facilis quis! Molestiae, ex harum? Ullam ad illum eligendi non distinctio? A, ad nobis.',
			link: 'https://www.google.com'
		}
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

<Title id="projects" text="Porjects" />

<section>
	<div class="project-container">
		<img class="project_img" src={websites[currentIndex].src} alt="projects" />

		<div class="link">
			<a style="color: white;" href={websites[currentIndex].link}>Visit website</a>
		</div>
	</div>
	<a style="margin-bottom: 16px;" href={websites[currentIndex].link}>Visit website</a>
	<div class="text-container">
		<p>{websites[currentIndex].text}</p>
	</div>
	<div class="controls">
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<svg on:click={prev} tabindex="0" role="button" aria-label="Previous Project" class="arrow left-arrow" xmlns="http://www.w3.org/2000/svg" width="24" height="48" viewBox="0 0 12 24"><path fill="currentColor" d="M1.843 12.711L7.5 18.368l1.414-1.414l-4.95-4.95l4.95-4.95L7.5 5.64 1.843 11.297a1 1 0 0 0 0 1.414" /></svg>
		<span>{currentIndex + 1} / {websites.length}</span>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<svg on:click={next} tabindex="0" role="button" aria-label="Next Project" class="arrow right-arrow" xmlns="http://www.w3.org/2000/svg" width="24" height="48" viewBox="0 0 12 24"><path fill="currentColor" d="M10.157 12.711L4.5 18.368l-1.414-1.414l4.95-4.95l-4.95-4.95L4.5 5.64l5.657 5.657a1 1 0 0 1 0 1.414" /></svg>
	</div>
</section>

<style>
	span {
		font-size: 24px;
		color: white;
	}
	.controls {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-top: 16px;
		width: 158px;
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
	.project-container {
		position: relative;
		margin-bottom: 16px;
	}
	.project_img {
		height: 192px;
		width: 384px;
		border: 1px solid var(--border);
		border-radius: 16px;
	}
	.link {
		display: flex;
		opacity: 0;
		position: absolute;
		top: 0;
		left: 0;
		background-color: rgba(0, 0, 0, 0.7); /* Semi-transparent yellow */
		height: 100%;
		width: 100%;
		border-radius: 16px;
		justify-content: center;
		align-items: center;
		transition: all 0.3s ease-in;
	}
	.project-container:hover .link {
		opacity: 100;
	}
	.link a {
		color: black;
		text-decoration: none;
		font-weight: bold;
	}
	.text-container {
		display: flex;
		align-items: center;
		height: 100px;
		overflow-y: auto;
	}
	p {
		font-size: 24px;
		text-align: center;
		color: white;
	}
	section {
		position: relative;
		display: flex;
		align-items: center;
		justify-content: space-between;
		flex-direction: column;
		padding: 32px;
		border: 1px solid var(--border);
		border-radius: 16px;
		width: 90vw;
		color: white;
		background-color: black;
		margin-bottom: 16px;
	}
	@media (max-width: 1080px) {
		p {
			font-size: 16px;
		}
		.arrow {
			height: 32px;
			width: 32px;
		}
		span {
			font-size: 18px;
		}
		.controls {
			width: 110px;
		}
	}
	@media (max-width: 689px) {
		.project_img {
			height: 128px;
			width: 256px;
		}
		p {
			font-size: 12px;
		}
	}
	@media (max-width: 380px) {
		.text-container {
			height: 120px;
		}
	}
</style>
