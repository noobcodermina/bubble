<script lang="ts">
	import '../app.css';
	import Header from '../lib/components/Header.svelte';
	import type { LayoutProps } from './$types';

	let { children }: LayoutProps = $props();
</script>

<Header />
{@render children()}
