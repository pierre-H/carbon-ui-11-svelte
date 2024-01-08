<script lang="ts" context="module">
	import '@carbon/styles/scss/components/form/_index.scss';
</script>

<script lang="ts">
	import type { HTMLAttributes } from 'svelte/elements';

	let { class: divClass = '', children, ...restProps } = $props<HTMLAttributes<HTMLDivElement>>();
</script>

<div {...restProps} class="cds--form-requirement {divClass}">
	{#if children}
		{@render children()}
	{/if}
</div>
