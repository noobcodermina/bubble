<script>
	import { onMount } from 'svelte';
	import Bubble from '../assets/Bubble.svelte';

	let headerStats = $state();
	let liters = $state(0);
	onMount(() => {
		headerStats = JSON.parse(localStorage.getItem('stats') ?? '[]');

		for (let i = 0; i < headerStats.length; i++) {
			liters += headerStats[i].glasses;
		}
	});
</script>

<header class="flex-between">
	<div class="logo flex-center">
		<Bubble />
		<p>bubble</p>
	</div>
	<p class="liter-day-sum second-font">
		{#if headerStats}
			{headerStats.length}d / {liters}L
		{/if}
	</p>
</header>

<style>
	header {
		width: 100%;
		.logo {
			color: var(--accent_100);
			font-weight: var(--bold);
			gap: var(--spacing-md);
		}
		.liter-day-sum {
			font-size: var(--text-sm);
		}
	}
</style>
