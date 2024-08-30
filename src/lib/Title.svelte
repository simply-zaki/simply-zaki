<script>
    export let text = "hello"
	export let id = "id"
</script>

<h1 id={id}>{text}</h1>

<style>
    	h1 {
		scroll-margin-top: 100px;
		margin-bottom: 32px;
		text-align: center;
        border-bottom: 3px solid white;
		padding-bottom: 5px;
	}
	@media (max-width:912px){
		h1{
			font-size: 24px;
		}
	}
</style>