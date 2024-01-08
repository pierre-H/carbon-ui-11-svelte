<script lang="ts">
	import type { HTMLAnchorAttributes } from 'svelte/elements';
	import Link from '../Link/Link.svelte';

	let {
		disabled,
		clicked,
		light,
		class: tileClass = '',
		onclick,
		...restProps
	} = $props<HTMLAnchorAttributes & { disabled?: boolean; light?: boolean; clicked?: boolean }>();
</script>

<Link
	{...restProps}
	{disabled}
	class="cds--tile cds--tile--clickable {clicked && 'cds--tile--is-clicked'} {light &&
		'cds--tile--light'} {tileClass}"
	onclick={(e) => {
		clicked = !clicked;
		if (onclick) {
			onclick(e);
		}
	}}
	on:keydown={({ key }) => {
		if (key === ' ' || key === 'Enter') {
			clicked = !clicked;
		}
	}}
>
	<slot />
</Link>
