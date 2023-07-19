<script lang="ts">
	import type { HTMLAnchorAttributes } from 'svelte/elements';

	interface $$Props extends HTMLButtonAttributes {}

	export let href: string;
</script>

<a
	{...$$restProps}
	{href}
	class="cds--link {$$restProps.class ?? ''}"
	on:click
	on:focus
	on:mouseover
	on:mouseenter
	on:mouseleave
>
	<slot />
</a>
