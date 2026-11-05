<script>
	import { onMount } from 'svelte';
	import Bubble from '../lib/assets/Bubble.svelte';
	import Button from '../lib/components/Button.svelte';
	let glassCounter = $state(0);

	//date stuff
	let date = $state(new Date());

	let day = $state(date.getDate());
	let month = $state(date.getMonth() + 1);
	let fullYear = $state(date.getFullYear());

	let year = Array.from(String(fullYear));

	//kada se ucita sajt uzimamo podatke (da ih mozemo prikazati na sajtu)
	let getStats = $state();
	let statsArr = [];
	let id = $state('');
	onMount(() => {
		id = crypto.randomUUID();
		getStats = JSON.parse(localStorage.getItem('stats') ?? '[]');
		statsArr.push(...getStats);

		//uzimamo localglasses

		let local = localStorage.getItem('localGlasses');
		glassCounter = Number(local);
	});
	let dayStats = $derived({
		date: `${day}/${month}/${year[2]}${year[3]}`,
		glasses: glassCounter,
		id: id
	});

	$effect(() => {
		localStorage.setItem('localGlasses', String(glassCounter));
	});
</script>

<div class="stats">
	<!-- ovo sranje je koji je datum i koliki je serving, dan te jebo -->
	<div class="date-and-serving flex-between">
		<p class="second-font">{day}/{month}/{year[2]}{year[3]}</p>
		<p class="second-font">serving: 0.2l</p>
	</div>
	<!-- ova kurcina ovdje su baloni koji MIJENJAJU JEBENU BOJU KAD COUNTER SKACE... -->
	<div class="bubble-row flex-between">
		<Bubble
			onclick={() => {
				glassCounter = 1;
			}}
			style={glassCounter > 0 ? 'stroke:#c3cbfb' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 2;
			}}
			style={glassCounter > 1 ? 'stroke:#c3cbfb' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 3;
			}}
			style={glassCounter > 2 ? 'stroke:#a1b0f5' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 4;
			}}
			style={glassCounter > 3 ? 'stroke:#a1b0f5' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 5;
			}}
			style={glassCounter > 4 ? 'stroke:#8ca5ee' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 6;
			}}
			style={glassCounter > 5 ? 'stroke:#8ca5ee' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 7;
			}}
			style={glassCounter > 6 ? 'stroke:#8ca5ee' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 8;
			}}
			style={glassCounter > 7 ? 'stroke:#6787e7' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 9;
			}}
			style={glassCounter > 8 ? 'stroke:#6787e7' : ''}
		/>
		<Bubble
			onclick={() => {
				glassCounter = 10;
			}}
			style={glassCounter > 9 ? 'stroke:#4169e1' : ''}
		/>
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
		<Button
			onclick={() => {
				statsArr.push(dayStats);
				localStorage.setItem('stats', JSON.stringify(statsArr));
				glassCounter = 0;

				window.location.reload();
			}}>Save</Button
		>
	</div>
</div>
<p class="heatmap-title">Heatmap colors based on daily intake</p>
<div class="heatmap-examples flex-center second-font">
	<div class="second-font flex-center">0</div>
	<div class="second-font flex-center bg-stage-one">1-2</div>
	<div class="second-font flex-center bg-stage-two">3-4</div>
	<div class="second-font flex-center bg-stage-three">5-7</div>
	<div class="second-font flex-center bg-stage-four">8-9</div>
	<div class="second-font flex-center bg-stage-five">10</div>
</div>
<p class="heatmap-title">Heatmap:</p>
<div class="heatmap flex-center">
	{#each getStats as data (data.id)}
		<div
			class="flex-between"
			class:bg-stage-one={data.glasses < 3 && data.glasses > 0}
			class:bg-stage-two={data.glasses > 2 && data.glasses < 5}
			class:bg-stage-three={data.glasses > 4 && data.glasses < 9}
			class:bg-stage-four={data.glasses > 7 && data.glasses < 10}
			class:bg-stage-five={data.glasses == 10}
		>
			<p>{data.glasses}s/{(data.glasses * 0.2).toFixed(2)}l</p>
			<p>{data.date}</p>
		</div>
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
		flex-wrap: wrap;
		flex-direction: column-reverse;
		:global(div) {
			width: 100%;
			padding: var(--spacing-sm);
			font-size: var(--text-sm);
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
