<script lang="ts">
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import type { Snippet } from 'svelte';

	interface btnProps extends HTMLButtonAttributes {
		children: Snippet;
	}

	let { children, ...rest }: btnProps = $props();
</script>

<button {...rest}>{@render children()}</button>

<style>
	button {
		padding: var(--spacing-sm);
		border: 2px solid var(--accent_80);
		color: var(--text);
		width: 50px;
		background-color: var(--bg);
		border-radius: 0.5rem;
		font-weight: var(--bold);
	}
</style>
