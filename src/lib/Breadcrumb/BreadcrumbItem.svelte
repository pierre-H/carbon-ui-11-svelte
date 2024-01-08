<script lang="ts">
	import Link from '../Link/Link.svelte';
	import type { HTMLAnchorAttributes, HTMLLiAttributes } from 'svelte/elements';

	let {
		href,
		target,
		download,
		rel,
		media,
		ping,
		current = false,
		class: itemClass = '',
		children,
		...restProps
	} = $props<
		HTMLAnchorAttributes &
			HTMLLiAttributes & {
				current?: boolean;
			}
	>();
</script>

<li
	{...restProps}
	class="cds--breadcrumb-item {itemClass}"
	class:cds--breadcrumb-item--current={current}
>
	{#if children}
		{#if href}
			<Link {href} {target} {download} {rel} {media} {ping} {children} />
		{:else}
			{@render children()}
		{/if}
	{/if}
</li>
