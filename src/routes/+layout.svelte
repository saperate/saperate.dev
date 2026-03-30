<script lang="ts">
	import Header from './Header.svelte';
	import './layout.css';

	let { children } = $props();
	import { dev } from '$app/environment';
	import { injectAnalytics } from '@vercel/analytics/sveltekit';

	injectAnalytics({ mode: dev ? 'development' : 'production' });


	function getRandomColor() {
		return "#" + ((1 << 24) * Math.random() | 0).toString(16).padStart(6, "0");
	}

	const changecss = async () => {
		document.body.style.setProperty("--color-bg-0", getRandomColor())
		document.body.style.setProperty("--color-bg-1", getRandomColor())
		document.body.style.setProperty("--color-bg-2", getRandomColor())

		document.body.style.setProperty("--color-text", getRandomColor())
		document.body.style.setProperty("--color-theme-1", getRandomColor())
		document.body.style.setProperty("--color-theme-2", getRandomColor())
	};
</script>

<div class="app">
	<Header />

	<main>
		{@render children()}
	</main>

	<button on:click={changecss}>
		Randomize colors!
	</button>
	<footer>
		<p>
			All rights reserved - @ {new Date().getFullYear()} Saperate
		</p>
	</footer>
</div>

<style>
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
