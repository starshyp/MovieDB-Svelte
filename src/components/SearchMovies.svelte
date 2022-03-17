<script>
	let inputValue = '';
	let active = false;
	import { goto } from '$app/navigation';
	import { fly } from 'svelte/transition';

	function cancelInactive() {
		if (inputValue) {
			active = true;
		} else {
			active = false;
		}
	}

	function submitSearch() {
		goto('/search/' + inputValue);
	}
</script>

<div class="form">
	<form on:submit|preventDefault={submitSearch} class="search">
		{#if !active}
			<label
				in:fly={{ y: -10, duration: 500 }}
				out:fly={{ y: -10, duration: 500 }}
				for="search_movie">Search Movie</label
			>
		{/if}
		<input
			on:blur={cancelInactive}
			on:focus={() => (active = true)}
			bind:value={inputValue}
			name="search_movie"
			type="text"
		/>
		<button>Search</button>
	</form>
</div>

<style>
	.form {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}
	.search {
		position: relative;
		width: 30%;
		margin: 1rem;
	}
	button {
		font-size: 0.7rem;
		padding: 0rem 1rem;
		background: rgb(96, 110, 201);
		color: white;
		font-weight: bold;
		border: none;
		position: absolute;
		bottom: 50%;
		right: 0;
		transform: translate(0, 50%);
		height: 100%;
		border-top-right-radius: 0.625rem;
		border-bottom-right-radius: 0.625rem;
		cursor: pointer;
	}
	input {
		width: 100%;
		border: 2px solid #494949;
		border-radius: 1rem;
		color: #494949;
		font-size: 0.8rem;
		font-family: 'Poppins', sans-serif;
		transition: background 0.75s ease-out;
		color: #000;
		padding: 1rem 1rem;
		width: 100%;
	}
	label {
		position: absolute;
		font-size: 0.8rem;
		top: 50%;
		left: 0;
		transform: translate(0, -50%);
		pointer-events: none;
		color: #000;
		padding: 0rem 1rem;
	}
</style>
