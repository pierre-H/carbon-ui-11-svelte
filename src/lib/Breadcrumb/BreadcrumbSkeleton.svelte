<script lang="ts">
	import type { HTMLAttributes } from 'svelte/elements';

	let {
		noTrailingSlash,
		class: skeletonClass = '',
		...restProps
	} = $props<HTMLAttributes<HTMLDivElement> & { noTrailingSlash?: boolean }>();
</script>

<div
	{...restProps}
	class="cds--breadcrumb cds--skeleton {skeletonClass}"
	class:cds--breadcrumb--no-trailing-slash={noTrailingSlash}
>
	<div class="cds--breadcrumb-item"><span class="cds--link">&nbsp;</span></div>
	<div class="cds--breadcrumb-item"><span class="cds--link">&nbsp;</span></div>
	<div class="cds--breadcrumb-item"><span class="cds--link">&nbsp;</span></div>
</div>
