

<script>
	import Slider from "../components/Slider.svelte";
	import MovieListPopular from "../components/MovieListPopular.svelte";
	import MovieListNew from "../components/MovieListNew.svelte";

</script>

<style lang="scss">
	.lista-movies{
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		grid-gap: 10px;
		margin: 20px;
		padding-top: 40px;
		padding-bottom: 40px;
	}
</style>

<svelte:head>
	<title>Inicio</title>
</svelte:head>

<Slider/>

<div class="lista-movies">
	<MovieListPopular/>
	<MovieListNew/>
</div>
