<script>
	export let nextQuestion;
	export let isAnswered;
	function toggleAnswered() {
		isAnswered = false;
	}
</script>

<button on:click={(toggleAnswered, nextQuestion)}>wrong Answer</button>

<style>
	button {
		color: red;
	}
</style>
