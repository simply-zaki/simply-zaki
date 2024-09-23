<section id="about">
	<img draggable="false" src="/cat.svg" alt="icon" class="floating_cat" />
	<main>
		<h1>Hello, im <span class="name">simply zaki</span></h1>
		<p>
			A full stack web developer who started in 2022, specializing in making user friendly websites and web apps, I create minimal easy to use sites that are helpful and make life easy without being confusing.
		</p>
	</main>
</section>

<style>
	h1 {
		font-size: 48px;
		line-height: 1.2;
		margin-bottom: 24px;
	}
	section {
		display: flex;
		justify-content: space-evenly;
		align-items: center;
		padding-top: 128px;
		margin-bottom: 135px;
	}
	main {
		width: 50%;
	}
	.floating_cat {
		height: 384px;
		cursor: grab;
		animation: float 3s ease-in-out infinite;
	}
	@keyframes float {
		0% {
			transform: translateY(0);
		}
		50% {
			transform: translateY(-10px);
		}
		100% {
			transform: translateY(0);
		}
	}
	@media (max-width: 1230px) {
		.floating_cat {
			height: 256px;
		}
		h1 {
			font-size: 32px;
		}
	}
	@media (max-width: 750px) {
		section {
			flex-direction: column;
			text-align: center;
			padding-top: 96px;
		}
		main {
			width: 100%;
		}
	}
	.name {
		display: inline-block;
		transition: all 0.3s ease;
	}

	.name:hover {
		font-family: 'Comic Sans MS', 'Comic Sans', cursive;
		font-size: 0.95em;
		font-weight: bold;
	}
</style>
