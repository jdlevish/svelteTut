<script>
	export let word;
	export let nextQuestion;
	console.log(word.word);
	setTimeout(function () {
		nextQuestion();
	}, 7000);
</script>

<div class="word">{word.word}</div>

<style>
	.word {
		border: 6px solid purple;
		padding: 10px 60px 10px 60px;
		font-family: "Source Sans Pro", sans-serif;
		font-weight: 900;
		font-size: 4.5rem;
		color: purple;
	}
</style>
