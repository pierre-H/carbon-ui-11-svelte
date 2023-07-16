<script lang="ts" context="module">
	export type ButtonType =
		| 'primary'
		| 'secondary'
		| 'tertiary'
		| 'danger'
		| 'danger--tertiary'
		| 'danger--ghost'
		| 'ghost';

	export type ButtonSize = 'sm' | 'md' | 'lg' | 'xl' | '2xl';

	import '@carbon/styles/scss/components/button/_index.scss';
</script>

<script lang="ts">
	import type { HTMLButtonAttributes, HTMLAnchorAttributes } from 'svelte/elements';

	interface $$Props extends HTMLButtonAttributes {
		kind?: ButtonType;
		size?: ButtonSize;
		ref?: HTMLButtonElement | HTMLAnchorElement;
		icon?: ConstructorOfATypedSvelteComponent;
		selected?: boolean;
		expressive?: boolean;
		href?: HTMLAnchorAttributes['href'];
		target?: HTMLAnchorAttributes['target'];
		download?: HTMLAnchorAttributes['download'];
		media?: HTMLAnchorAttributes['media'];
		ping?: HTMLAnchorAttributes['ping'];
		rel?: HTMLAnchorAttributes['rel'];
		referrerpolicy?: HTMLAnchorAttributes['referrerpolicy'];
		skeleton?: boolean;
	}

	export let kind: ButtonType = 'primary';

	export let size: ButtonSize | undefined = undefined;

	$: sizeClass = size ? `cds--btn--${size} cds--layout--size-${size} ` : '';

	export let skeleton: boolean = false;

	let tag = 'button';

	$: if (href !== undefined) {
		tag = 'a';
	} else if (skeleton) {
		tag = 'div';
	} else {
		tag = 'button';
	}

	export let ref: HTMLButtonElement | HTMLAnchorElement | undefined = undefined;

	export let icon: ConstructorOfATypedSvelteComponent | undefined = undefined;

	$: hasIcon = icon != null || $$slots.icon;
	$: iconOnly = !skeleton && hasIcon && $$slots['default'] == undefined;

	export let selected: boolean = false;
	export let expressive: boolean = false;

	export let href: HTMLAnchorAttributes['href'] | undefined = undefined;
</script>

<svelte:element
	this={tag}
	{...$$restProps}
	bind:this={ref}
	class="cds--btn {sizeClass} cds--btn--{kind} {$$restProps.class ?? ''}"
	class:cds--skeleton={skeleton}
	class:cds--btn--icon-only={iconOnly}
	class:cds--btn--selected={selected}
	class:cds--btn--expressive={expressive}
	on:click
	on:focus
	on:mouseover
	on:mouseenter
	on:mouseleave
	role={$$restProps.role ?? 'button'}
	tabindex={$$restProps.tabindex ?? 0}
>
	{#if !skeleton}
		<slot />
		{#if hasIcon}
			<slot name="icon">
				<svelte:component this={icon} class="cds--btn__icon" />
			</slot>
		{/if}
	{/if}
</svelte:element>
