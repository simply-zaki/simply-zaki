<section id="about">
	<span>
		<h1>Hello, im simply zaki</h1>
		<p>A full stack web developer specializing in making user friendly websites and web apps. I create minimal easy to use sites that are helpful and make life easy without being confusing</p>
	</span>

	<img draggable="false" src="/cat.svg" alt="icon" />
</section>

<style>
	h1 {
		font-size: 96px;
		line-height: 1;
		margin-bottom: 24px;
	}
	p {
		font-size: 24px;
	}
	section {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 96px 64px 16px 64px;
		margin-bottom: 16px;
	}
	span {
		width: 50%;
	}
	img {
		height: 500px;
		cursor: grab;
	}
	@media (max-width: 1225px) {
		img{
			height: 384px;
		}
		h1{
			font-size: 64px;
		}
		p{
			font-size: 16px;	
		}
	}
	@media (max-width: 912px) {
		img{
			height: 256px;
		}
		h1{
			font-size: 48px;
		}
		p{
			font-size: 12px;	
		}
	}
	@media (max-width: 768px) {
		*{
			text-align: center;
		}
		section{
			flex-direction: column;
		}
		span{
			order: 3;
			width: 100%;
		}
		section{
			padding-top: 64px;
		}
	}
	@media (max-width: 400px) {
		img{
			height: 200px;
		}
		h1{
			font-size: 32px;
		}
	}
</style>
