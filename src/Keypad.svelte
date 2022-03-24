<script>
	import { createEventDispatcher } from 'svelte';

	export let value = '';

	const dispatch = createEventDispatcher();

	const select = num => () => value += num;
	const clear  = () => value = '';
	const submit = () => dispatch('submit');
    const keyPad=['1','2','3','4','5','6','7','8','9']
</script>

<div class="justify-content">

<div class="keypad-operands">

    {#each Array(9) as _, i}
    <button on:click={select(i+1)}>{i+1}</button>
    {/each}

	<button disabled={!value} on:click={clear}>clear</button>
	<button on:click={select(0)}>0</button>
	<button disabled={!value} on:click={submit}>=</button>
</div>
<!-- key pad is add -->
<div class="keypad-operator">
	<button on:click={select('/')}>/</button>
	<button on:click={select('*')}>*</button>
	<button on:click={select('-')}>-</button>
	<button on:click={select('+')}>+</button>
</div>
</div>
<style>
	.keypad-operands {
		display: grid;
		grid-template-columns: repeat(3, 5em);
		grid-template-rows: repeat(4, 3em);
		grid-gap: 0.5em
	}
	.keypad-operator {
		display: grid;
		grid-template-columns: repeat(1, 5em);
		grid-template-rows: repeat(4, 3em);
		grid-gap: 0.5em;
        margin-left: 10px;
	}
	button {
		margin: 0
	}
    .justify-content{
        display: flex;
        justify-content: center;
    }
</style>