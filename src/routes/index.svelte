<script context="module">
	export async function load({ fetch }) {
		const url = `https://api.themoviedb.org/3/movie/popular?api_key=${
			import.meta.env.VITE_API
		}&language=en-US&page=1`;
		const response = await fetch(url);
		const data = await response.json();
		return {
			status: response.status,
			props: {
				popular: response.ok && data.results
			}
		};
	}
</script>

<script>
	// @ts-nocheck
	import PopularMovies from '../components/PopularMovies.svelte';
	import SearchMovies from '../components/SearchMovies.svelte';
	export let popular;
	import { fly } from 'svelte/transition';
</script>

<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
	<SearchMovies />
	<PopularMovies {popular} />
</section>
