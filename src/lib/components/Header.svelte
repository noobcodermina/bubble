<script>
	import Bubble from '../assets/Bubble.svelte';
</script>

<header class="flex-between">
	<div class="logo flex-center">
		<Bubble />
		<p>bubble</p>
	</div>
	<p class="liter-day-sum second-font">30d / 60L</p>
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
