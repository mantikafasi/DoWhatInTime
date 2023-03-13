<script>
	import Header from "../components/Header.svelte";
	import "./styles.css";
</script>

<div class="app">
	<Header />

	<main>
		<slot />
	</main>

	<footer>
		<p>Made by <a href="https://github.com/mantikafasi">manti</a></p>
	</footer>
</div>

<style>
	:global(:root.dark) {
		--header-background-color: #3f3f3f;
		--invert-svg: invert(100%);
		--border-color: white;
		--background-color: #1e1e1e;
		--color-bg-1: #3f3f3f;
		background: #1e1e1e;
		color: #fff;
	}

	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
