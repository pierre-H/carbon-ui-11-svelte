<script lang="ts">
	import type { HTMLDivAttributes } from 'svelte/elements';

	interface $$Props extends HTMLDivAttributes {
		stacked?: boolean;
	}

	export let stacked: boolean = false;
</script>

<div
	{...$$restProps}
	class="cds--btn-set {$$restProps.class ?? ''}"
	class:cds--btn-set--stacked={stacked}
>
	<slot />
</div>
