<script lang="ts" context="module">
	import '@carbon/styles/scss/components/loading/_index.scss';
	import type { HTMLAttributes } from 'svelte/elements';
</script>

<script lang="ts">
	let {
		description = 'Loading',
		class: loadingClass = '',
		active = true,
		small = false,
		withOverlay = false,
		...restProps
	} = $props<
		HTMLAttributes<HTMLDivElement> & {
			description?: string;
			active?: boolean;
			small?: boolean;
			withOverlay?: boolean;
		}
	>();
</script>

{#snippet loader()}
	<div
		aria-atomic="true"
		aria-live={active ? 'assertive' : 'off'}
		class="cds--loading {loadingClass}"
		class:cds--loading--stop={active === false}
		class:cds--loading--small={small}
		{...restProps}
	>
		<svg class="cds--loading__svg" viewBox="0 0 100 100"
			><title>{description}</title>
			{#if small}
				<circle class="cds--loading__background" cx="50%" cy="50%" r="44"></circle>
			{/if}
			<circle class="cds--loading__stroke" cx="50%" cy="50%" r="44"></circle>
		</svg>
	</div>
{/snippet}

{#if withOverlay}
	<div class="cds--loading-overlay">
		{@render loader()}
	</div>
{:else}
	{@render loader()}
{/if}
