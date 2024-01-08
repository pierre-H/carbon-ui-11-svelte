<script lang="ts" context="module">
	import '@carbon/styles/scss/components/aspect-ratio/_index.scss';
	import type { HTMLAttributes } from 'svelte/elements';

	export type Ratio = '1x1' | '2x3' | '3x2' | '3x4' | '4x3' | '1x2' | '2x1' | '9x16' | '16x9';
</script>

<script lang="ts">
	let {
		as = 'div',
		ratio = '1x1',
		...restProps
	} = $props<HTMLAttributes<EventTarget> & { as?: string; ratio: Ratio }>();
</script>

<svelte:element this={as} {...restProps} class="cds--aspect-ratio cds--aspect-ratio--{ratio}">
	<slot />
</svelte:element>
