<script>
	import Header from '$lib/Header.svelte';
	import About from '$lib/About.svelte';
	import Projects from '$lib/Projects.svelte';
</script>

<Header />
<main>
	<About />

	<div class="line"></div>

	<Projects/>
</main>

<style>
	.line {
		margin-bottom: 16px;
		border-bottom: 1px solid var(--border);
		width: 90vw;
	}
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>
