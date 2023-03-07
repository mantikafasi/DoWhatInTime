<script>
    import DarkModeButton from "./DarkModeButton.svelte";

</script>
<header>
	<div class="corner">
		
		<DarkModeButton/>
	</div>

	<nav>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L1,2 C1.5,3 1.5,3 2,3 L2,0 Z" />
		</svg>
		<span class = "headerText">
			DO WHAT IN TIME
		</span>
		
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L0,3 C0.5,3 0.5,3 1,2 L2,0 Z" />
		</svg>
	</nav>
</header>

<style>
	.corner {
		position: absolute;
		top: 0;
		right: 0;
		padding: 0.5em;
		z-index: 1
	}
	
	.headerText{
		font-size: 1.5em;
		font-weight: bold;
		background-color: var(--header-background-color);
		text-align: center;
		padding-top: 0.5em;
		
	}

	header {
		
		display: flex;
		justify-content: space-between;
	}


	nav {
		width: 100%;
		position: absolute;
		display: flex;
		justify-content: center;
		--background: rgba(255, 255, 255, 0.7);
	}

	svg {
		width: 2em;
		height: 3em;
		display: block;
	}

	path {
		fill: var(--header-background-color);
	}

</style>
