<script>
	export let word;
	export let nextQuestion;
	console.log(word.word);
	setTimeout(function () {
		nextQuestion();
	}, 4000);
</script>

<div class="word">{word.word}</div>

<style>
	.word {
		justify-self: center;
		grid-column: 2 / span 2;
		/* grid-column-end: 3; */
		grid-row-start: 2;
		margin-top: 5vh;
		border: 6px solid white;
		padding: 10px 60px 10px 60px;
		font-family: "Source Sans Pro", sans-serif;
		font-weight: 900;
		font-size: 4.5rem;
		color: white;
	}
</style>
