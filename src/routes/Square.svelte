<script lang="ts">
	import { get_twemoji_url } from './utils';
	import { send } from './transitions';

	export let emoji: string;
	export let selected: boolean;
	export let found: boolean;
	export let group: 'a' | 'b';
</script>

<div class="square" class:flipped={selected || found}>
	<button on:click />

	<div class="background" class:found/>

	{#if !found}
		<img alt={emoji} src={get_twemoji_url(emoji)} out:send={{ key: `${emoji}:${group}` }} />
	{/if}
</div>

<style>
	.square {
		display: flex;
		justify-content: center;
		align-items: center;
		transform-style: preserve-3d;
		transition: transform 0.4s;
	}

	.background {
		background: #fff;
		border: 0.5em solid #eee;
		transform: rotateY(180deg);
		backface-visibility: hidden;
		width: 100%;
		height: 100%;
		position: absolute;
		border-radius: 1em;
	}

	.flipped {
		transform: rotateY(180deg);
	}

	button {
		position: absolute;
		height: 100%;
		width: 100%;
		cursor: pointer;
		backface-visibility: hidden;
		background: #eee;
		border: 0;
		font-size: inherit;
		border-radius: 1em;
	}

	img {
		width: 5em;
		height: 5em;
		pointer-events: none;
		transform: rotateY(180deg);
		backface-visibility: hidden;
	}
</style>
