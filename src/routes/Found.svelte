<script lang="ts">
	import { receive } from './transitions';
	import { get_twemoji_url } from './utils';

	export let found: string[];
</script>

<div class="found">
	{#each found as emoji, i}
		<div class="pair">
			<img alt={emoji} src={get_twemoji_url(emoji)} in:receive={{ key: `${emoji}:a` }} />
			<img alt={emoji} src={get_twemoji_url(emoji)} in:receive={{ key: `${emoji}:b` }} />
		</div>
	{/each}
</div>

<style>
	.found {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.5em;
		height: 100%;
		filter: drop-shadow(0.2em 0.2em 0.5em rgba(0, 0, 0, 0.3));
	}

	.pair {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 6em;
		height: 6em;
		background: white;
		border-radius: 50%;
	}

	img {
		position: absolute;
		width: 3em;
		height: 3em;
	}
</style>
