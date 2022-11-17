<script>
	import Questions from "./Questions.svelte";
	let difficultyUser = "";
	let categoryUser = "";
</script>

<main>
	<h1>Trivia Questions</h1>
	<div id="selectOptions">
		<label>
			Select a difficulty or leave blank:
			<select bind:value={difficultyUser}>
				<option value="" />
				<option value="easy">Easy</option>
				<option value="medium">Medium</option>
				<option value="hard">Hard</option>
			</select>
		</label>
		<label>
			Select a category or leave blank:
			<select bind:value={categoryUser}>
				<option value="" />
				<option value="27">Animals</option>
				<option value="24">Politics</option>
				<option value="25">Art</option>
				<option value="21">Sports</option>
				<option value="28">Vehicles</option>
				<option value="20">Mythology</option>
			</select>
		</label>
	</div>
	<Questions category={categoryUser} difficulty={difficultyUser}  />
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	#selectOptions {
		margin-bottom: 2rem;
		display: flex;
		flex-direction: row;
		justify-content: center;
	}

	select { 
		margin: 1rem;
	}

	h1 {
		color: #000000;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>