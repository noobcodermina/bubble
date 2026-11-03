<script>
	import Bubble from '../lib/assets/Bubble.svelte';
	import Button from '../lib/components/Button.svelte';
	let glassCounter = $state(0);

	$effect(() => {
		console.log(glassCounter);
	});
</script>

<div class="stats">
	<div class="date-and-serving flex-between">
		<p class="second-font">12.02.2026.</p>
		<p class="second-font">s::0.2l</p>
	</div>

	<div class="bubble-row flex-between">
		<Bubble />
		<Bubble />
		<Bubble />
		<Bubble />
		<Bubble />
		<Bubble />
		<Bubble />
		<Bubble />
		<Bubble />
		<Bubble />
	</div>

	<div class="button-row">
		<Button
			onclick={() => {
				glassCounter -= 1;

				if (glassCounter < 0) {
					glassCounter = 0;
				}
			}}>-</Button
		>
		<Button
			onclick={() => {
				glassCounter += 1;

				if (glassCounter > 10) {
					glassCounter = 10;
				}
			}}>+</Button
		>
		<Button>Done</Button>
	</div>
</div>

<style>
	.stats {
		margin-top: calc(var(--spacing-xl) * 2);
		.date-and-serving {
			font-size: var(--text-sm);
		}

		.bubble-row {
			margin-top: var(--spacing-lg);
			:global(svg) {
				stroke: var(--secondary);
			}
		}
	}
</style>
