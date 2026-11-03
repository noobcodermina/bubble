<script>
	import Bubble from '../lib/assets/Bubble.svelte';
	import Button from '../lib/components/Button.svelte';
	let glassCounter = $state(0);

	let mockData = $state([
		{ id: 0, date: '23.12.2026.', glasses: 5 },
		{ id: 1, date: '23.12.2026.', glasses: 5 },
		{ id: 2, date: '23.12.2026.', glasses: 5 },
		{ id: 3, date: '23.12.2026.', glasses: 5 },
		{ id: 4, date: '23.12.2026.', glasses: 5 },
		{ id: 5, date: '23.12.2026.', glasses: 5 },
		{ id: 6, date: '23.12.2026.', glasses: 5 },
		{ id: 7, date: '23.12.2026.', glasses: 5 },
		{ id: 8, date: '23.12.2026.', glasses: 5 }
	]);

	$effect(() => {
		console.log(glassCounter);
	});
</script>

<div class="stats">
	<div class="date-and-serving flex-between">
		<p class="second-font">12.02.2026.</p>
		<p class="second-font">serving: 0.2l</p>
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

	<div class="button-row flex-between">
		<div class="add-remove-buttons">
			<Button
				onclick={() => {
					glassCounter -= 1;

					if (glassCounter < 0) {
						glassCounter = 0;
					}
				}}
			>
				-
			</Button>
			<Button
				onclick={() => {
					glassCounter += 1;

					if (glassCounter > 10) {
						glassCounter = 10;
					}
				}}>+</Button
			>
		</div>
		<Button>Save</Button>
	</div>
</div>
<p class="heatmap-title">Heatmap colors based on daily intake</p>
<div class="heatmap-examples flex-center second-font">
	<div class="second-font flex-center">0</div>
	<div class="second-font flex-center bg-stage-one">1-2</div>
	<div class="second-font flex-center bg-stage-two">2-4</div>
	<div class="second-font flex-center bg-stage-three">4-6</div>
	<div class="second-font flex-center bg-stage-four">6-9</div>
	<div class="second-font flex-center bg-stage-five">10</div>
</div>
<p class="heatmap-title">Heatmap:</p>
<div class="heatmap flex-center">
	{#each mockData as data (data.id)}
		<div class:bg-stage-one={data.glasses < 2} class:bg-stage-two={data.glasses == 5}></div>
	{/each}
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
		.button-row {
			margin-top: var(--spacing-lg);
		}
	}
	.heatmap-title {
		margin-top: var(--spacing-xl);
		margin-bottom: var(--spacing-sm);
	}
	.heatmap {
		justify-content: flex-start;
		gap: var(--spacing-sm);

		:global(div) {
			width: 20px;
			height: 20px;
			border-radius: 0.25rem;
			border: 2px solid var(--secondary);
		}
	}

	.heatmap-examples {
		justify-content: flex-start;
		gap: var(--spacing-sm);

		div {
			width: 40px;
			height: 40px;
			border-radius: 0.25rem;
			border: 2px solid var(--secondary);
			font-size: var(--text-sm);
		}
	}
</style>
