<script>
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';
	let loaded = false;
	onMount(() => {
		loaded = true;
	});
</script>

{#if loaded === true}
	<header transition:fade={{duration:800, delay:500}} >
		<span>simply zaki</span>
		<img src="/cat.svg" alt="icon" />
		<a href="#about">About</a>
		<a href="#projects">Projects</a>
		<a href="#technologies">Technologies</a>
		<a href="#skills">Skills</a>
	</header>
{/if}

<style>
	header {
		position: fixed;
		top: 0;
		display: flex;
		align-items: center;
		padding: 16px;
		border-bottom: 1px solid var(--border);
		width: 100vw;
		background-color: black;
		z-index: 999;
	}
	img {
		margin-right: auto;
		height: 48px;
		margin-left: 8px;
	}
	a {
		margin-right: 16px;
		text-decoration: none;
		transition: color background-color 0.2s ease-in;
	}
	a:hover {
		color: #d3d3d3;
	}
	a:active {
		transform: scale(0.97);
		fill: #a9a9a9; /* Darker gray on active */
	}
	@media (max-width: 600px) {
		a {
			font-size: 12px;
		}
		span {
			display: none;
		}
	}
	@media (max-width: 384px) {
		img {
			height: 32px;
			margin-left: 0;
		}
	}
</style>
