<script context="module">
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/search/movie?api_key=${process.env.TMDB_API_KEY}&language=en-US&query=${params.id}&page=1&include_adult=false`
		);
		const data = await res.json();
		if (res.status === 200) {
			return {
				props: {
					searchedMovie: data.results
				}
			};
		}
	}
</script>

<script>
	import MovieCard from '../../components/MovieCard.svelte';
	export let searchedMovie;
</script>

<div class="searched-movie">
	{#each searchedMovie as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.searched-movie {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
		grid-column-gap: 1rem;
		grid-row-gap: 2rem;
	}
</style>
