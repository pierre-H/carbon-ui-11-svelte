<script lang="ts">
	import type { HTMLAttributes } from 'svelte/elements';

	let {
		stacked,
		class: buttonSetClass,
		children,
		...restProps
	} = $props<HTMLAttributes<HTMLDivElement> & { stacked?: boolean }>();
</script>

<div
	{...restProps}
	class="cds--btn-set {buttonSetClass ?? ''}"
	class:cds--btn-set--stacked={stacked}
>
	{#if children}
		{@render children()}
	{/if}
</div>
