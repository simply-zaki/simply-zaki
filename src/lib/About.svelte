<section id="about">
	<img draggable="false" src="/cat.svg" alt="icon" />
	<span>
		<h1>Hello, im simply zaki</h1>
		<p>A full stack web developer specializing in making user friendly websites and web apps. I create minimal easy to use sites that are helpful and make life easy without being confusing</p>
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
	img {
		height: 384px;
		cursor: grab;
	}
	@media (max-width: 1230px) {
		img{
			height: 256px;
		}
		h1{
			font-size: 32px;
		}
	}
	@media (max-width: 750px) {
		section{
			flex-direction: column;
			text-align: center;
			padding-top: 96px;
		}
	}
</style>
