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
	>Correct</button
>

<style>
	button {
		color: black;
		line-height: 1rem;
	}

	.question {
		justify-self: center;
		grid-column: 2 / span 2;
		/* grid-column-end: 4; */
		grid-row-start: 2;
	}
</style>
