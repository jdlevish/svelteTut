<script>
	export let nextQuestion;
	export let isAnswered;
	export let correctAnswer;
	function toggleAnswered() {
		isAnswered = false;
	}
</script>

<button class="question" on:click={(toggleAnswered, nextQuestion)}
	>wrong Answer</button
>
<h3>The Correct Answer was : {@html correctAnswer}</h3>

<style>
	button {
		color: red;
	}
	h3 {
		color: red;
	}
	.question {
		justify-self: center;
		grid-column-start: 1;
		grid-column-end: 4;
		grid-row-start: 3;
	}
</style>
