<script>
	import Header from '$lib/Header.svelte';
	import About from '$lib/About.svelte';
	import Projects from '$lib/Projects.svelte';
	import Technologies from '$lib/Technologies.svelte';
	import Skills from '$lib/Skills.svelte';
	import Footer from '$lib/Footer.svelte';
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';
	let loaded = false;
	onMount(() => {
		loaded = true;
	});
</script>

{#if loaded === true}
	<Header />
	<main transition:fade={{ duration: 800, delay: 1400 }}>
		<About />

		<Projects />

		<Technologies />

		<Skills />
	</main>
	<Footer />
{/if}

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 32px;
	}
</style>
