<script>
	export let quiz;
	export let activeQuestion;
	export let scorePoint;
	export let nextQuestion;
	import Spell from "./SpellQuestion.svelte";
	import { fade } from "svelte/transition";
	console.log(quiz);
</script>

{#each quiz as question, index}
	{#if index === activeQuestion}
		<div transition:fade class="question">
			<Spell {nextQuestion} {scorePoint} {question} />
		</div>
	{/if}
{/each}

<style>
	.question {
		justify-self: center;
		grid-column-start: 2;
		grid-column-end: 4;
		grid-row-start: 1;
		margin-top: 15vh;
	}
</style>
