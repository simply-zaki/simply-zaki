<section id="about">
	<img draggable="false" src="/cat.svg" alt="icon" class="floating_cat" />
	<span>
		<h1>Hello, im <span class="name">simply zaki</span></h1>
		<p>
			A full stack web developer<img src="/dev.svg" alt="icon" class="icon" />specializing in making user friendly<img src="/user_friendly.svg" alt="icon" class="icon" />websites and web apps<svg class="icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><line x1="2" y1="12" x2="22" y2="12"></line><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"></path></svg>.
		</p>
		<p>I create minimal easy to use sites that are helpful and make life easy without being confusing<svg class="icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path  d="M14 9V5a3 3 0 0 0-3-3l-4 9v11h11.28a2 2 0 0 0 2-1.7l1.38-9a2 2 0 0 0-2-2.3zM7 22H4a2 2 0 0 1-2-2v-7a2 2 0 0 1 2-2h3"></path></svg></p>
	</span>
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
		margin-bottom: 100px;
	}
	span {
		width: 50%;
	}
	.floating_cat{
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
		span {
			width: 100%;
		}
	}
	.name {
		display: inline-block;
		transition: all 0.3s ease;
	}

	.name:hover {
		font-family: 'Comic Sans MS', 'Comic Sans', cursive;
		font-size: 0.95em; /* Slightly reduce font size */
		font-weight: bold; /* Make it bold to compensate for size reduction */
	}
	.icon {
		width: 24px;
		height: 24px;
		margin-right: 4px;
		margin-left: 4px;
		vertical-align: middle;
		display: inline-block;
		position: relative;
		top: -1px;
	}
	@keyframes float {
		0% {
			transform: translateY(0px);
		}
		50% {
			transform: translateY(-10px);
		}
		100% {
			transform: translateY(0px);
		}
	}
</style>
