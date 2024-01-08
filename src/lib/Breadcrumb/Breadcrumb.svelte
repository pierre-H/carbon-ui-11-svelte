<script lang="ts" context="module">
	import '@carbon/styles/scss/components/breadcrumb/_index.scss';
</script>

<script lang="ts">
	import BreadcrumbSkeleton from './BreadcrumbSkeleton.svelte';
	import type { HTMLAttributes } from 'svelte/elements';

	let {
		noTrailingSlash = false,
		skeleton = false,
		class: breadcrumbClass = '',
		children,
		...restProps
	} = $props<
		HTMLAttributes<HTMLOListElement> & { noTrailingSlash?: boolean; skeleton?: boolean }
	>();
</script>

{#if skeleton}
	<BreadcrumbSkeleton {noTrailingSlash} />
{:else}
	<ol
		{...restProps}
		class="cds--breadcrumb {breadcrumbClass}"
		class:cds--breadcrumb--no-trailing-slash={noTrailingSlash}
	>
		{#if children}
			{@render children()}
		{/if}
	</ol>
{/if}
