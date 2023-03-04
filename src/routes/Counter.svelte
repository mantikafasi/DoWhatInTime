<script lang="ts">
	import { spring } from 'svelte/motion';
	export let counterName = 'Days';
	export let value = 0;
	

	const displayed_count = spring();
	$: displayed_count.set(value);
	$: offset = $displayed_count%1;


</script>

<div class="counter">
	<span>
		{counterName}
	</span>
	<button on:click={() => (value += 1)} aria-label="Increase the counter by one">
		<svg aria-hidden="true" viewBox="0 0 1 1">
			<path d="M0,0.5 L1,0.5 M0.5,0 L0.5,1" />
		</svg>
	</button>

	<div class="counter-viewport">
		<div class="counter-digits" style="transform: translate(0, {100 * offset}%)">
			<strong class="hidden" aria-hidden="true">{Math.floor($displayed_count + 1)}</strong>
			<strong>{Math.floor($displayed_count)}</strong>
		</div>
	</div>

	<button on:click={() => {
		if (value > 0)
			value -= 1;
		}} aria-label="Decrase the counter by one">
		<svg aria-hidden="true" viewBox="0 0 1 1">
			
			<path d="M0,0.5 L1,0.5" />
		</svg>
	</button>
</div>

<style>
	span { 
		display: block;
		font-size: 1.5rem;
		font-weight: bold;
		text-align: center;
		margin-bottom: 5%;
	}
	.counter {
		
		display: flex;
		border: 1px solid rgba(0, 0, 0, 0.1);
		margin: 1rem 0;
		align-items: center;
		display: inline-block
	}

	.counter button {
		width: 2em;
		padding: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		border: 0;
		background-color: transparent;
		touch-action: manipulation;
		font-size: 2rem;
		transform: translate(50%,0);
		margin-bottom: 4%;
	}

	.counter button:hover {
		background-color: var(--color-bg-1);
	}

	svg {
		width: 25%;
		height: 25%;
		margin-bottom: 0.1rem;
		margin-top: 0.1rem;
	}

	path {
		vector-effect: non-scaling-stroke;
		stroke-width: 2px;
		stroke: #444;
	}

	.counter-viewport {
		width: 8em;
		height: 2em;
		overflow: hidden;
		text-align: center;
		position: relative;
	}

	.counter-viewport strong {
		position: absolute;
		display: flex;
		width: 100%;
		height: 100%;
		font-weight: 400;
		color: var(--color-theme-1);
		font-size: 2rem;
		align-items: center;
		justify-content: center;
	}

	.counter-digits {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	.hidden {
		top: -100%;
		user-select: none;
	}
</style>
