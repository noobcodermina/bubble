<script lang="ts">
	import '../app.css';
	import Header from '../lib/components/Header.svelte';
	import type { LayoutProps } from './$types';

	let { children }: LayoutProps = $props();
</script>

<svelte:head>
	<title>bubble - track water intake</title>
	<meta name="description" content="This is a super simple way to track your water intake" />
</svelte:head>

<div class="wrapper">
	<Header />
	{@render children()}
</div>

<style>
	.wrapper {
		width: 100%;
		max-width: 500px;

		margin: auto;
	}
</style>
