<script>
	export let nextQuestion;
	export let scorePoint;
	export let isAnswered;
	scorePoint();
	function toggleAnswered() {
		isAnswered = false;
	}
</script>

<button class="question" on:click={(scorePoint, toggleAnswered, nextQuestion)}
	>Correct Answer</button
>

<style>
	button {
		color: cornflowerblue;
	}

	.question {
		justify-self: center;
		grid-column-start: 1;
		grid-column-end: 4;
		grid-row-start: 3;
	}
</style>
