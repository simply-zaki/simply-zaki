<script>
	import Header from '$lib/Header.svelte';
	import About from '$lib/About.svelte';
	import Projects from '$lib/Projects.svelte';
	import Tools_languages from '$lib/Tools_languages.svelte';
	import Skills from '$lib/Skills.svelte';
</script>

<Header />
<main>
	<About />

	<Projects />

	<Tools_languages />

	<Skills />
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>
