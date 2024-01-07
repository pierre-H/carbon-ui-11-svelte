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

	let {
		kind = 'primary',
		size,
		skeleton,
		ref,
		icon,
		children,
		href,
		selected,
		expressive,
		class: buttonClass,
		...restProps
	} = $props<
		HTMLButtonAttributes & {
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
	>();

	let sizeClass = $derived(size ? `cds--btn--${size} cds--layout--size-${size} ` : '');

	let tag = $state('button');

	$effect(() => {
		if (href !== undefined) {
			tag = 'a';
		} else if (skeleton) {
			tag = 'div';
		} else {
			tag = 'button';
		}
	});

	let hasIcon = $derived(icon != null);
	let iconOnly = $derived(!skeleton && hasIcon && !children);
</script>

<svelte:element
	this={tag}
	{...restProps}
	bind:this={ref}
	class="cds--btn {sizeClass} cds--btn--{kind} {buttonClass ?? ''}"
	class:cds--skeleton={skeleton}
	class:cds--btn--icon-only={iconOnly}
	class:cds--btn--selected={selected}
	class:cds--btn--expressive={expressive}
	role={restProps.role ?? 'button'}
	tabindex={restProps.tabindex ?? 0}
>
	{#if !skeleton}
		{#if children}
			{@render children()}
		{/if}
		{#if hasIcon}
			<svelte:component this={icon} class="cds--btn__icon" />
		{/if}
	{/if}
</svelte:element>
