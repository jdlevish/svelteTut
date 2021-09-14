<script>
	export let nextQuestion;
	export let scorePoint;
	export let isAnswered;
	scorePoint();
	function toggleAnswered() {
		isAnswered = false;
	}
</script>

<button on:click={(scorePoint, toggleAnswered, nextQuestion)}
	>Correct Answer</button
>

<style>
	button {
		color: cornflowerblue;
	}
</style>
