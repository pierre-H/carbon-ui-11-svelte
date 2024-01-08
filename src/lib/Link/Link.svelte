<script lang="ts" context="module">
	import '@carbon/styles/scss/components/link/_index.scss';
	import type { SvelteComponent } from 'svelte';
	import type { HTMLAnchorAttributes } from 'svelte/elements';

	export type LinkProps = HTMLAnchorAttributes & {
		disabled?: boolean;
		inline?: boolean;
		visited?: boolean;
		icon?: SvelteComponent;
		size: 'sm' | 'md' | 'lg';
	};
</script>

<script lang="ts">
	let {
		class: anchorClass = '',
		disabled = false,
		inline = false,
		visited = false,
		icon,
		size = 'md',
		children,
		...restProps
	} = $props<LinkProps>();
</script>

{#if disabled}
	<p
		class="cds--link cds--link--disabled {anchorClass}"
		class:cds--link--disabled={disabled}
		class:cds--link--inline={inline}
		class:cds--link--visited={visited}
		class:cds--link--sm={size === 'sm'}
		class:cds--link--sm={size === 'md'}
		class:cds--link--lg={size === 'lg'}
	>
		{#if children}
			{@render children()}
		{/if}
		{#if !inline && icon}
			<div class="cds--link__icon">
				<svelte:component this={icon} />
			</div>
		{/if}
	</p>
{:else}
	<a
		class="cds--link {anchorClass}"
		class:cds--link--disabled={disabled}
		class:cds--link--inline={inline}
		class:cds--link--visited={visited}
		class:cds--link--sm={size === 'sm'}
		class:cds--link--lg={size === 'lg'}
		{...restProps}
	>
		{#if children}
			{@render children()}
		{/if}
		{#if !inline && icon}
			{#if !inline && icon}
				<div class="cds--link__icon">
					<svelte:component this={icon} />
				</div>
			{/if}
		{/if}
	</a>
{/if}
