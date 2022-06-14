<script context="module">
	/** @type {import('./__types/[id]').Load} */
	export async function load({ fetch, params }) {
		const url = `https://api.themoviedb.org/3/search/movie?api_key=${
			import.meta.env.VITE_API
		}&language=en-US&query=${params.id}&page=1&include_adult=false`;
		const response = await fetch(url);
		const seachedMovie = await response.json();
		return {
			status: response.status,
			props: {
				searchedMovie: response.ok && seachedMovie.results
			}
		};
	}
</script>

<script>
	// @ts-nocheck

	import SearchMovies from '../../components/SearchMovies.svelte';
	import MovieCard from '../../components/MovieCard.svelte';
	export let searchedMovie;
</script>

<div class="searched-movies">
	{#each searchedMovie as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.searched-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		grid-column-gap: 1rem;
		grid-row-gap: 2rem;
		height: 20vh;
	}
</style>
