<script>
	import Title from "$lib/Title.svelte"
</script>

<Title id="skills" text="Skills" />

<ul>
	<li>
		<span>
			<img src="/dev.svg" alt="ss" />
			<h3>Complete website</h3>
		</span>
		I can build a complete website and take care of everything like frontend, backend, deployment, SEO... from start to finish.
	</li>
	<li>
		<span>
			<img src="/user_friendly.svg" alt="ss" />
			<h3>User friendly websites</h3>
		</span>
		I make websites easy to use, user friendly but complex in features from design to functionality, ensuring a seamless experience.
	</li>
	<li>
		<span>
			<img src="/3d.svg" alt="ss" />
			<h3>3D integration</h3>
		</span>
		I can add 3D elements to your website, such as simple 3D icons or character poses, enhancing visual engagement and interactivity.
	</li>
	<li>
		<span>
			<img src="/language.svg" alt="ss" />
			<h3>Language skills</h3>
		</span>
		I speak Arabic and English, providing clear communication and understanding in both languages.
	</li>
</ul>

<style>
	ul {
		display: grid;
		grid-template-columns: 320px 320px;
		grid-template-rows: 190px 190px;
		align-items: flex-start;
		margin-bottom: 100px;
		gap: 16px;
		height: auto;
		width: auto;
	}

	li {
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		border-radius: 16px;
		font-size: 16px;
		list-style: none;
		border: 1px solid var(--border);
		padding: 16px;
		height: 100%;
		transition: transform 0.3s ease, box-shadow 0.3s ease, filter 0.3s ease;
		cursor: pointer;
		position: relative; /* Ensure the ::before pseudo-element positions correctly */
	}

	img {
		height: 48px;
	}

	span {
		display: flex;
		align-items: center;
		margin-bottom: 8px;
		gap: 8px;
	}

	li:hover {
		transform: scale(1.05);
		box-shadow: 0 0 15px rgba(255, 255, 255, 0.3); /* Softer, more diffused glow */
	}

	li:hover::before {
		content: "";
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		border-radius: 16px;
		box-shadow: 0 0 20px rgba(255, 255, 255, 0.15); /* Very subtle, soft glow */
		z-index: -1;
		pointer-events: none;
	}

	ul:hover li:not(:hover) {
		filter: brightness(0.75);
	}

	@media (max-width: 670px) {
		ul {
			display: flex;
			flex-direction: column;
			align-items: center;
			width: 90vw;
		}
		li {
			font-size: 12px;
		}
		img {
			height: 32px;
		}
	}
</style>



