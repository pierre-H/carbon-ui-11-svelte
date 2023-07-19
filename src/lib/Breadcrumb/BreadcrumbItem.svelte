<script lang="ts">
	import Link from '../Link/Link.svelte';
	import type { HTMLAnchorAttributes } from 'svelte/elements';

	export let href: HTMLAnchorAttributes['href'] = undefined;
	export let target: HTMLAnchorAttributes['target'] = undefined;
	export let download: HTMLAnchorAttributes['download'] = undefined;
	export let rel: HTMLAnchorAttributes['rel'] = undefined;
	export let media: HTMLAnchorAttributes['media'] = undefined;
	export let ping: HTMLAnchorAttributes['ping'] = undefined;

	export let current: boolean = false;
</script>

<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
<li
	{...$$restProps}
	class="cds--breadcrumb-item {$$restProps.class ?? ''}"
	class:cds--breadcrumb-item--current={current}
	on:click
	on:focus
	on:mouseover
	on:mouseenter
	on:mouseleave
>
	{#if href}
		<Link {href} {target} {download} {rel} {media} {ping}><slot /></Link>
	{:else}
		<slot />
	{/if}
</li>
