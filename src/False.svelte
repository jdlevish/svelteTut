<script>
	export let nextQuestion;
	export let isAnswered;
	export let correctAnswer;
	function toggleAnswered() {
		isAnswered = false;
	}
</script>

<button on:click={(toggleAnswered, nextQuestion)}>wrong Answer</button>
<h3>The Correct Answer was : {@html correctAnswer}</h3>

<style>
	button {
		color: red;
	}
	h3 {
		color: red;
	}
</style>
