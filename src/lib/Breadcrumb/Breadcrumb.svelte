<script lang="ts" context="module">
	import '@carbon/styles/scss/components/breadcrumb/_index.scss';
</script>

<script lang="ts">
	import BreadcrumbSkeleton from './BreadcrumbSkeleton.svelte';

	export let noTrailingSlash: boolean = false;
	export let skeleton: boolean = false;
</script>

{#if skeleton}
	<BreadcrumbSkeleton {noTrailingSlash} />
{:else}
	<ol
		{...$$restProps}
		class="cds--breadcrumb {$$restProps.class ?? ''}"
		class:cds--breadcrumb--no-trailing-slash={noTrailingSlash}
	>
		<slot />
	</ol>
{/if}
