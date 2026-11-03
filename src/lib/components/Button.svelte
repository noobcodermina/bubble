<script lang="ts">
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import type { Snippet } from 'svelte';

	interface btnProps extends HTMLButtonAttributes {
		children: Snippet;
	}

	let { children, ...rest }: btnProps = $props();
</script>

<button {...rest}>{@render children()}</button>
