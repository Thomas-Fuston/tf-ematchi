<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import Square from './Square.svelte';

	export let grid: string[];
	export let found: string[];

	const dispatch = createEventDispatcher();

	let a:number;
	let b:number;
	let reset_timeout: number;

</script>

<div class="grid">
	{#each grid as emoji, i}
		<Square
				on:click={()=> {
					if (a > -1 && b > -1) {
						clearTimeout(reset_timeout);
						a = i;
						b = -1;
					} else if (a > -1) {
						b = i;
						if (grid[a] === grid[b]) {
							found = [...found, grid[a]];
							dispatch('found', { emoji: grid[a] });
						} else {
							reset_timeout = setTimeout(() => {
								a = b = -1;
							}, 1000)
						}
					} else {
							a =i;
					}
				}}
			{emoji}
			selected={a === i || b === i}
			found={found.includes(emoji)}
			group={grid.indexOf(emoji) === i ? 'a' : 'b'}
		/>
	{/each}
</div>

<style>
	.grid {
		display: grid;
		grid-template-columns: repeat(var(--size), 1fr);
		grid-template-rows: repeat(var(--size), 1fr);
		grid-gap: 0.5em;
		height: 100%;
		perspective: 100vw;
	}
</style>
