<script>
	export let category;
	export let difficulty;

	let baseUrl = "https://opentdb.com/api.php?amount=1&type=multiple";

	const getData = async () => {
		if (category === "" && difficulty === "") {
			let response = await fetch(baseUrl);
			let data = await response.json();
			return data;
		} else if (category != "" && difficulty === "") {
			let newCategory = parseInt(category);
			let responseOne = await fetch(baseUrl + `&category=${newCategory}`);
			let dataOne = await responseOne.json();
			return dataOne;
		} else if (category === "" && difficulty != "") {
			let responseTwo = await fetch(
				baseUrl + `&difficulty=${difficulty}`
			);
			let dataTwo = await responseTwo.json();
			return dataTwo;
		} else if (category != "" && difficulty != "") {
			let newCategoryTwo = parseInt(category);
			let responseThree = await fetch(
				baseUrl +
					`&category=${newCategoryTwo}` +
					`&difficulty=${difficulty}`
			);
			let dataThree = await responseThree.json();
			return dataThree;
		}
	};

	let score = 0;

	const findScore = () => {
		let correctAnswer = document.getElementById('answer').selectedIndex

		if(correctAnswer === 1){
			score++
		} else {
			alert('Wrong Answer')
		}
	};
	let promise = getData();
</script>

<main>
	<form on:submit|preventDefault={findScore}>
		{#await promise}
			<p>Getting your questions...</p>
		{:then value}
			<h2>Current Question</h2>
				<p>{value.results[0].question}</p>
				<select id="answer">
					<option></option>
					<option>{value.results[0].correct_answer}</option>
					{#each value.results[0].incorrect_answers as wrong}
						<option>{wrong}</option>
					{/each}
				</select>
		{:catch error}
			<!-- promise was rejected -->
			<p>Something went wrong: {error.message}</p>
		{/await}

		<p>Score: You have {score} correct</p>

		<div id="subAnswers">
			<button type="submit">Submit Answer</button>
		</div>
	</form>

	<button
		on:click={() => {
			promise = getData();
		}}>Next Question</button
	>
</main>

<style>
	#subAnswers {
		margin-top: 2rem;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>