<script lang="ts" context="module">
	import '@carbon/styles/scss/components/aspect-ratio/_index.scss';
</script>

<script lang="ts">
	export let as: string = 'div';

	export let ratio: '1x1' | '2x3' | '3x2' | '3x4' | '4x3' | '1x2' | '2x1' | '9x16' | '16x9' = '1x1';
</script>

<svelte:element this={as} {...$$restProps} class="cds--aspect-ratio cds--aspect-ratio--{ratio}">
	<slot />
</svelte:element>
