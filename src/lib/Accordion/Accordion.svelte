<script lang="ts">
	import { writable } from 'svelte/store';
	import { setContext } from 'svelte';

	export let align: 'start' | 'end' = 'end';

	export let disabled: boolean = false;
	export let skeleton: boolean = false;

	export let size: 'sm' | 'md' | 'lg' | undefined = undefined;

	$: sizeClass = size ? `cds--accordion--${size} cds--layout--size-${size}` : '';

	export let flush: boolean = false;

	const accordionContext = writable<{
		disabled: boolean;
		skeleton: boolean;
	}>({ disabled, skeleton });

	$: accordionContext.update(() => ({
		skeleton,
		disabled
	}));

	setContext('cds-accordion', accordionContext);
</script>

<ul
	{...$$restProps}
	class="cds--accordion cds--accordion--{align} {sizeClass} {$$restProps.class ?? ''}"
	class:cds--accordion--flush={flush}
	class:cds--skeleton={skeleton}
>
	<slot />
</ul>
