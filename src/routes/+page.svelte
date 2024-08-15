<script>
	import Header from '$lib/Header.svelte';
	import About from '$lib/About.svelte';
	import Projects from '$lib/Projects.svelte';
	import Tools_languages from '$lib/Tools_languages.svelte';
</script>

<Header />
<main>
	<About />

	<Projects />

	<Tools_languages />
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>
